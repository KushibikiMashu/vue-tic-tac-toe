<template>
  <div>
    <div class="board-row">
      <square :value="squares[0]" :onclick="() => onclick(0)"/>
      <square :value="squares[1]" :onclick="() => onclick(1)"/>
      <square :value="squares[2]" :onclick="() => onclick(2)"/>
    </div>
    <div class="board-row">
      <square :value="squares[3]" :onclick="() => onclick(3)"/>
      <square :value="squares[4]" :onclick="() => onclick(4)"/>
      <square :value="squares[5]" :onclick="() => onclick(5)"/>
    </div>
    <div class="board-row">
      <square :value="squares[6]" :onclick="() => onclick(6)"/>
      <square :value="squares[7]" :onclick="() => onclick(7)"/>
      <square :value="squares[8]" :onclick="() => onclick(8)"/>
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
    onclick: Function
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
