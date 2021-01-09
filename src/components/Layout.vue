<template>
  <nav>
    <h1>Tic-Tac-Toe by Vue.js</h1>
    <p>
      <a href="https://github.com/KushibikiMashu/vue-tic-tac-toe">GitHub</a>
      {{ ' ' }}
      <a href="https://twitter.com/Panda_Program">Twitter</a>
    </p>
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
