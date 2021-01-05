<template>
  <layout>
    <template v-slot:default>
      <game />
    </template>
  </layout>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Layout from './components/Layout.vue'
import Game from './components/Game.vue'

export default defineComponent({
  name: 'App',
  components: {
    Layout,
    Game
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
