<script setup lang="ts">
const color = useColorMode()

function toggleDark() {
  color.preference = color.value === 'dark' ? 'light' : 'dark'
}
</script>

<template>
  <button class="!outline-none" @click="toggleDark">
    <div class="dark:i-carbon-sun i-carbon-moon" />
  </button>
</template>

<style>
body {
  background-color: white;
  color: #1f2937;
  /* @apply bg-white text-gray-800; */
}
html.dark body {
  background-color: #1f2937;
  color: white;
  /* @apply bg-gray-800 text-white; */
}
</style>
