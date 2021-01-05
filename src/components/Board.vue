<template>
  <div>
<div class="status">status</div>
<div class="board-row">
  <square />
  <square />
  <square />
</div>
<div class="board-row">
  <square />
  <square />
  <square />
</div>
<div class="board-row">
  <square />
  <square />
  <square />
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
      status: 'Next player: X'
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
