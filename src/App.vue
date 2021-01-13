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
