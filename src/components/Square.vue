<template>
  <button v-if="!isWinnerCell" class="square" @click="onclick">
    {{ value }}
  </button>
  <button v-else class="square-win" @click="onclick">
    {{ value }}
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Square',
  props: {
    value: String,
    onclick: Function,
    isWinnerCell: Boolean
  }
})
</script>

<style scoped>
.square,.square-win {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.square:focus, .square-win:focus {
  outline: none;
  background: #ddd;
}

.square-win {
  background: red;
}
</style>
