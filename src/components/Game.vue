<template>
  <div class="game">
    <div>
      <board
        :squares="currentSquares"
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
        <li v-for="(step, i) in history" :key="i">
          <button @click="jumpTo(i)">
            <span :class="{'game-stepButton-bold': i === stepNumber}">
              {{ isDesc ? getDescButtonBody(i) : getAscButtonBody(i) }}
            </span>
          </button>
<!--          <span v-if="step.location.row && step.location.column">（{{ step.location.row }}, {{ step.location.column }}）</span>-->
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
import { defineComponent, reactive, ref, computed } from 'vue'
import Board from './Board.vue'

export default defineComponent({
  name: 'Game',
  components: { Board },
  setup () {
    const history = reactive([{
      squares: Array(9).fill(null),
      location: {
        row: null,
        column: null
      }
    }])
    const stepNumber = ref(0)
    const xIsNext = ref(true)
    const isDesc = ref(true)
    const winnerCells = ref(null)

    const currentSquares = computed(() => {
      return history[stepNumber.value].squares
    })

    const calculateWinner = (squares) => {
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
          winnerCells.value = lines[i]
          return squares[a]
        }
      }

      return null
    }

    const current = history[history.length - 1]

    const handleClick = (i) => {
      // 勝者が決まったらマークは追加できない
      if (winnerCells.value) {
        return
      }

      const squares = current.squares

      if (calculateWinner(squares) || squares[i]) {
        return
      }

      squares[i] = xIsNext.value ? 'X' : 'O'
      const location = {
        row: Math.floor(i / 3) + 1,
        column: i % 3 + 1
      }
      const newHistory = { squares, location }
      isDesc.value ? history.push(newHistory) : history.unshift(newHistory)
      stepNumber.value += 1
      xIsNext.value = !xIsNext.value
    }

    // status
    const winner = computed(() => calculateWinner(current.squares))
    const status = computed(() => {
      if (winner.value) {
        return 'Winner: ' + winner.value
      } else if (history.length === 10 && winnerCells.value === null) {
        return 'No winner'
      }

      return `Next player: ${xIsNext.value ? 'X' : 'O'}`
    })

    const jumpTo = (step) => {
      stepNumber.value = step
      xIsNext.value = (step % 2) === 0
    }

    const toggle = () => {
      isDesc.value = !isDesc.value
      stepNumber.value = history.length - 1 - stepNumber.value
      history.value = history.reverse()
    }

    const getAscButtonBody = (i) => {
      const length = history.length - 1

      return i === length ? 'Go to game start' : `Go to move #${length - i}`
    }

    const getDescButtonBody = (i) => {
      return i ? `Go to move #${i}` : 'Go to game start'
    }

    return {
      history,
      currentSquares,
      stepNumber,
      status,
      isDesc,
      winnerCells,
      handleClick,
      jumpTo,
      toggle,
      getAscButtonBody,
      getDescButtonBody
    }
  }
})
</script>

<style scoped>
.game {
  display: flex;
  flex-direction: row;
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
