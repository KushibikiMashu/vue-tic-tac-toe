<template>
<div class="game">
  <div class="game-board">
    <board />
  </div>
  <div class="game-info">
    <div>status</div>
    <ol>todo</ol>
  </div>
</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Board from './Board.vue'

export default defineComponent({
  name: 'Game',
  components: { Board }
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
