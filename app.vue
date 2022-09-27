<script setup>
import './assets/css/main.css'

const config = useRuntimeConfig()
useHead({
  title: config.public.appName,
  meta: [{ name: 'p:domain_verify', content: '6ad70d8e7ecb0a518d089fb53a18d7f7' }],
  // link: [
  //   {
  //     rel: 'icon', type: 'image/png', href: '/nuxt.png',
  //   },
  // ],
})
</script>

<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>

<style>
html, body , #__nuxt{
  min-height: 100vh;
  margin: 0;
  padding: 0;
}

/* html.dark {
  background: #222;
  color: white;
} */
</style>
