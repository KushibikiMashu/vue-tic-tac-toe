<template>
  <div class="game">
    <div class="game-board">
      <board
        :squares="current"
        :winnerCells="winnerCells"
        v-on:clickSquare="handleClick"
      />
    </div>
    <div class="game-info">
      <div>{{ status }}</div>
      <div>
        <button @click="toggle">{{ isDesc ? '降順' : '昇順' }}</button>
      </div>
      <ol>
        <li v-for="({ location }, move) in history" :key="move">
          <button @click="jumpTo(move)">
            <span :class="{'game-stepButton-bold': move === stepNumber}">
              {{ isDesc ? getDescButtonBody(move) : getAscButtonBody(move) }}
            </span>
          </button>
          <span v-if="location.row && location.column">（{{ location.row }}, {{ location.column }}）</span>
        </li>
      </ol>
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
      history: [{
        squares: Array(9).fill(null),
        location: { row: null, column: null }
      }],
      stepNumber: 0,
      xIsNext: true,
      isDesc: true,
      winnerCells: null
    }
  },
  computed: {
    status () {
      const current = this.history[this.history.length - 1]
      const winner = this.calculateWinner(current.squares)
      let status

      if (winner) {
        status = 'Winner: ' + winner
      } else if (this.history.length === 10 && this.winnerCells === null) {
        status = 'No winner'
      } else {
        status = `Next player: ${this.xIsNext ? 'X' : 'O'}`
      }

      return status
    },
    current () {
      return this.history[this.stepNumber].squares
    }
  },
  methods: {
    handleClick (i) {
      if (this.winnerCells) {
        return
      }

      const current = this.history[this.history.length - 1]
      const squares = current.squares.slice()
      if (this.calculateWinner(squares) || squares[i]) {
        return
      }

      squares[i] = this.xIsNext ? 'X' : 'O'
      const location = { row: Math.floor(i / 3) + 1, column: i % 3 + 1 }

      const newHistory = [{ squares, location }]
      this.history = this.isDesc ? this.history.concat(newHistory) : newHistory.concat(this.history)
      this.stepNumber += 1
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
          this.winnerCells = lines[i]
          return squares[a]
        }
      }

      return null
    },
    jumpTo (step) {
      this.stepNumber = step
      this.xIsNext = (step % 2) === 0
    },
    toggle () {
      this.isDesc = !this.isDesc
      this.stepNumber = this.history.length - 1 - this.stepNumber
      this.history = this.history.reverse()
    },
    getDescButtonBody (move) {
      return move ? `Go to move #${move}` : 'Go to game start'
    },
    getAscButtonBody (move) {
      const length = this.history.length - 1

      return move === length ? 'Go to game start' : `Go to move #${length - move}`
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

.game-stepButton-bold {
  font-weight: bold;
}
</style>
