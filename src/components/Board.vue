<template>
  <div>
    <div class="board-row">
      <square :value="squares[0]" :onclick="() => onclick(0)" :isWinnerCell="isWinnerCell(0)"/>
      <square :value="squares[1]" :onclick="() => onclick(1)" :isWinnerCell="isWinnerCell(1)"/>
      <square :value="squares[2]" :onclick="() => onclick(2)" :isWinnerCell="isWinnerCell(2)"/>
    </div>
    <div class="board-row">
      <square :value="squares[3]" :onclick="() => onclick(3)" :isWinnerCell="isWinnerCell(3)"/>
      <square :value="squares[4]" :onclick="() => onclick(4)" :isWinnerCell="isWinnerCell(4)"/>
      <square :value="squares[5]" :onclick="() => onclick(5)" :isWinnerCell="isWinnerCell(5)"/>
    </div>
    <div class="board-row">
      <square :value="squares[6]" :onclick="() => onclick(6)" :isWinnerCell="isWinnerCell(6)"/>
      <square :value="squares[7]" :onclick="() => onclick(7)" :isWinnerCell="isWinnerCell(7)"/>
      <square :value="squares[8]" :onclick="() => onclick(8)" :isWinnerCell="isWinnerCell(8)"/>
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
  props: {
    squares: Array,
    onclick: Function,
    winnerCells: {
      type: Array,
      default: null
    }
  },
  methods: {
    isWinnerCell (i: number): boolean {
      if (!this.winnerCells) {
        return false
      }

      return this.winnerCells.includes(i)
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
