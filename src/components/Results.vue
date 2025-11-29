<script setup lang="ts">
import { computed } from 'vue'
import words from '../data/words.txt?raw'
import gallery from '../data/gallery.json'
import type { GalleryIndex } from '../types'

interface ResultsProps {
  selected: GalleryIndex
}

const { selected } = defineProps<ResultsProps>()

const wordsArray = words.split('\n').map(word => word.trim())

const results = computed(() => {
  const letters = gallery[selected] ?? []
  const lettersCount = letters.length
  const ranges = letters.map(group => `[${group.join('')}]`)
  const pattern = new RegExp(`^${ranges.join('')}$`)
  return wordsArray.filter(word => word.length !== lettersCount ? false : pattern.test(word))
})
</script>

<template>
  <section>
    <h2>Results {{ selected }}</h2>
    <p>{{ results.length }} matches</p>
    <ul>
      <li v-for="result in results" key="result">{{ result }}</li>
    </ul>
  </section>
</template>

<style scoped>
h2 {
  font-size: 2.5rem;
  margin: 1rem 0 0 0;
  padding: 0;
}

p {
  margin: 0.5rem 0 1.5rem 0;
  padding: 0;
}

ul {
  display: grid;
  list-style-type: none;
  gap: 1rem;
  grid-template-columns: repeat(6, max-content);
  margin: 0;
  padding: 0;
}

li {
  font-family: "Source Code Pro", monospace;
  font-optical-sizing: auto;
  font-weight: 600;
  font-size: 1.1rem;
  font-style: normal;
}
</style>
