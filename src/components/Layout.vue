<template>
  <nav>
    <h1>Tic-Tac-Toe by Vue.js</h1>
  </nav>
  <main>
    <slot></slot>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Layout'
})
</script>

<style scoped>

</style>
