<template>
  <nav>
    <h1>Tic-Tac-Toe by Vue.js</h1>
    <p>
      <a href="https://github.com/KushibikiMashu/vue-tic-tac-toe">GitHub</a>
      {{ ' ' }}
      <a href="https://twitter.com/Panda_Program">Twitter</a>
    </p>
  </nav>
  <main id="app">
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
