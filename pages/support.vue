<script setup>
const config = useRuntimeConfig()
useHead({
  title: `Support | ${config.public.appName}`,
})
</script>

<template>
  <div class=" px-4 lg:px-0 flex flex-col items-center my-10">
    <h1 class="title mb-10">
      Support
    </h1>
    <p class="pb-9">
      We'll figure out what to put here someday... until then here is Tokyo ToolKitsune
    </p>
    <img src="/TokyoToolKitsune.jpg" alt="Tokyo ToolKitsune">
  </div>
</template>
