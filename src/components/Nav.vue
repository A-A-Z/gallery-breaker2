<script setup lang="ts">
import { computed } from 'vue'
import gallery from '../data/gallery.json'

const { selected } = defineProps({
  selected: Number
})

const emit = defineEmits<{(e: 'select', value: number): void }>()

const options = computed(() => Object.keys(gallery).map(option => Number(option)))

const onSelect = (value: number) => {
  emit('select', value)
}
</script>

<template>
  <nav>
    <ul role="menubar">
      <li
        v-for="option in options"
        key="entry"
      >
        <label>
          <input
            type="radio"
            role="menuitem"
            name="letters"
            :value="option"
            :checked="option === selected"
            @change="() => { onSelect(option) }"
          ><span>{{ option }} letters</span></input>
        </label>
      </li>
    </ul>
  </nav>
</template>

<style scoped>
nav {
  background-color: #242424;
  display: flex;
  justify-content: center;
  padding: 0.5rem;
  position: fixed;
  inset: 0 0 auto 0;
}

ul {
  display: flex;
  list-style-type: none;
  gap: 1rem;
  margin: 0;
  padding: 0;
}

label {
  cursor: pointer;
}

span {
  padding-inline: 0.5rem;
}
</style>
