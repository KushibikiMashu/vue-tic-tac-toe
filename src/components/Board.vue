<template>
  <div>
<div class="status">{{ status }}{{ xIsNext ? 'X' : 'O' }}</div>
<div class="board-row">
  <square :value="squares[0]" :onclick="() => handleClick(0)" />
  <square :value="squares[1]" :onclick="() => handleClick(1)" />
  <square :value="squares[2]" :onclick="() => handleClick(2)" />
</div>
<div class="board-row">
  <square :value="squares[3]" :onclick="() => handleClick(3)" />
  <square :value="squares[4]" :onclick="() => handleClick(4)" />
  <square :value="squares[5]" :onclick="() => handleClick(5)" />
</div>
<div class="board-row">
  <square :value="squares[6]" :onclick="() => handleClick(6)" />
  <square :value="squares[7]" :onclick="() => handleClick(7)" />
  <square :value="squares[8]" :onclick="() => handleClick(8)" />
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
      status: 'Next player: ',
      squares: Array(9).fill(null),
      xIsNext: true
    }
  },
  methods: {
    handleClick (i: number) {
      this.squares[i] = this.xIsNext ? 'X' : 'O'
      this.xIsNext = !this.xIsNext
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
