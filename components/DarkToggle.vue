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
  @apply bg-white text-gray-800;
}
html.dark body {
  @apply bg-gray-800 text-white;
}
</style>
