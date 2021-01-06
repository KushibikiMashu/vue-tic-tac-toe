<template>
  <div>
    <div class="status">{{ status }}</div>
    <div class="board-row">
      <square :value="squares[0]" :onclick="() => handleClick(0)"/>
      <square :value="squares[1]" :onclick="() => handleClick(1)"/>
      <square :value="squares[2]" :onclick="() => handleClick(2)"/>
    </div>
    <div class="board-row">
      <square :value="squares[3]" :onclick="() => handleClick(3)"/>
      <square :value="squares[4]" :onclick="() => handleClick(4)"/>
      <square :value="squares[5]" :onclick="() => handleClick(5)"/>
    </div>
    <div class="board-row">
      <square :value="squares[6]" :onclick="() => handleClick(6)"/>
      <square :value="squares[7]" :onclick="() => handleClick(7)"/>
      <square :value="squares[8]" :onclick="() => handleClick(8)"/>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Square from './Square.vue'

export default defineComponent({
  name: 'Board',
  components: {
    Square
  },
  data () {
    return {
      status: 'Next player: X',
      squares: Array(9).fill(null),
      xIsNext: true
    }
  },
  methods: {
    handleClick (i: number) {
      if (this.calculateWinner(this.squares) || this.squares[i]) {
        return
      }

      this.squares[i] = this.xIsNext ? 'X' : 'O'
      this.xIsNext = !this.xIsNext
      this.updateStatus()
    },
    calculateWinner (squares: ('X' | 'O' | null)[]) {
      const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ]
      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i]
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
          return squares[a]
        }
      }
      return null
    },
    updateStatus () {
      const winner = this.calculateWinner(this.squares)
      let status
      if (winner) {
        status = 'Winner: ' + winner
      } else {
        status = `Next player: ${this.xIsNext ? 'X' : 'O'}`
      }

      this.status = status
    }
  }
})
</script>

<style scoped>
.status {
  margin-bottom: 10px;
}

.board-row:after {
  clear: both;
  content: "";
  display: table;
}
</style>
