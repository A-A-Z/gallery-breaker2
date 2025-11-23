<script setup lang="ts">
import { computed } from 'vue'
import words from '../data/words.txt?raw'
import gallery from '../data/gallery.json'

// defineProps<{ msg: string }>()

// const count = ref(0)

const wordsArray = words.split('\n')
const letters = gallery['7']
console.log(letters, wordsArray[2], wordsArray.length)
const lettersCount = letters.length
// const hasMinLetters = lettersCount >= MIN_LETTERS

// const pattern = computed(() => {
//   // create a array of strings for regex ranges
//   const ranges = letters.map(group => `[${group.join('')}]`)
//   // join all ranges into a single RegExp value
//   return new RegExp(`^${ranges.join('')}$`)
// })
const ranges = letters.map(group => `[${group.join('')}]`)
  // join all ranges into a single RegExp value
const pattern = new RegExp(`^${ranges.join('')}$`)

const results = computed(() => {
  return wordsArray.filter(word => word.length !== lettersCount ? false : pattern.test(word))
})

console.log({ results })
</script>

<template>
  <h2>Results</h2>
  <ul>
    <li v-for="result in results" key="result">{{ result }}</li>
  </ul>
</template>

<style scoped>
ul {
  display: grid;
  list-style-type: none;
  gap: 1rem;
  grid-template-columns: repeat(6, max-content);
}

li {
  font-family: "Source Code Pro", monospace;
  font-optical-sizing: auto;
  font-weight: 600;
  font-size: 1.1rem;
  font-style: normal;
}
</style>
