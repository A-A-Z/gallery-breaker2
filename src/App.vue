<script setup lang="ts">
import { ref } from 'vue'
import Nav from './components/Nav.vue'
import Results from './components/Results.vue'
import type { GalleryIndex } from './types'

const selected = ref(7)

const handleSelect = (value: number) => {
  selected.value = value
}
</script>

<template>
  <main>
    <Nav
      :selected="selected"
      @select="handleSelect"
    />
    <Results :selected="String(selected) as GalleryIndex" />
  </main>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
