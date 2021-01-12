<template>
  <button
    class="square"
    :class="{'square-win': isWinnerCell}"
    @click="handleClick"
  >
    {{ value }}
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Square',
  props: {
    value: String,
    index: Number,
    isWinnerCell: Boolean
  },
  emits: ['clickSquare'],
  methods: {
    handleClick () {
      this.$emit('clickSquare', this.index)
    }
  }
})
</script>

<style scoped>
.square {
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

.square:focus {
  outline: none;
  background: #ddd;
}

.square-win {
  background: red;
}
</style>
