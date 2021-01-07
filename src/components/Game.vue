<template>
<div class="game">
  <div class="game-board">
    <board :squares="getCurrent" :onclick="(i) => handleClick(i)" />
  </div>
  <div class="game-info">
    <div>{{ getStatus }}</div>
<!--    <ol>todo</ol>-->
  </div>
</div>
</template>

<script>
import { defineComponent } from 'vue'
import Board from './Board.vue'

export default defineComponent({
  name: 'Game',
  components: { Board },
  data () {
    return {
      status: 'Next player: X',
      history: [{
        squares: Array(9).fill(null)
      }],
      xIsNext: true
    }
  },
  computed: {
    getStatus () {
      const current = this.history[this.history.length - 1]
      const winner = this.calculateWinner(current.squares)
      let status
      if (winner) {
        status = 'Winner: ' + winner
      } else {
        status = `Next player: ${this.xIsNext ? 'X' : 'O'}`
      }

      return status
    },
    getCurrent () {
      return this.history[this.history.length - 1].squares
    }
  },
  methods: {
    handleClick (i) {
      const current = this.history[this.history.length - 1]
      const squares = current.squares.slice()
      if (this.calculateWinner(squares) || squares[i]) {
        return
      }

      squares[i] = this.xIsNext ? 'X' : 'O'

      this.history = this.history.concat([{ squares }])
      this.xIsNext = !this.xIsNext
    },
    calculateWinner (squares) {
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
    }
  }
})
</script>

<style scoped>
.game {
  display: flex;
  flex-direction: row;
}

.game-board {

}

.game-info {
  margin-left: 20px;
}

ol, ul {
  padding-left: 30px;
}
</style>
