<template>
  <div>
    <div class="board-row" v-for="i in 3" :key="i">
      <square
        v-for="j in [i * 3 - 3, i * 3 - 2, i * 3 - 1]"
        :key="j"
        :value="squares[j]"
        :onclick="() => onclick(j)"
        :isWinnerCell="isWinnerCell(j)"
      />
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
  data () {
    return {
      rows: [0, 1, 2]
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
.board-row:after {
  clear: both;
  content: "";
  display: table;
}
</style>
