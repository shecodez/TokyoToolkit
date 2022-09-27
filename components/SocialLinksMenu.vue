<script setup>
const socialIcons = [
  {
    icon: 'i-carbon:logo-discord',
    label: 'Discord',
    link: 'https://discord.gg/x2tr4fJu',
  },
  { icon: 'i-carbon:logo-instagram', label: 'Instagram', link: 'https://www.instagram.com/TokyoToolkit/' },
  { icon: 'i-carbon:logo-twitter', label: 'Twitter', link: 'https://twitter.com/TokyoToolkit' },
  { icon: 'i-carbon:logo-youtube', label: 'YouTube', link: 'https://www.youtube.com/channel/UCzV2BYxwNJlgc67Szapji0g' },
]
</script>

<template>
  <ul class="social-icons-menu invisible lg:visible">
    <li v-for="(n, i) in socialIcons" :key="`social-btn-${i}`">
      <a :href="n.link" target="_blank" class="social-icon-link h-7">
        <div :class="n.icon" />
        <span class="social-label">{{ n.label }}</span>
      </a>
    </li>
  </ul>
</template>

<style scoped>
.social-icons-menu {
  @apply fixed flex flex-col justify-center inset-y-0 left-6 gap-6 z-20;
}
.social-icon-link {
  @apply flex items-center gap-6 text-xl px-2 h-auto rounded aspect-square bg-white dark:bg-gray-800;
}
.social-icon-link svg {
  opacity: 0.7;
}
.social-icons-menu > li:hover > a.social-icon-link svg {
  opacity: 1;
}
span.social-label {
  opacity: 0;
  visibility: hidden;
  left: 50px;
  position: absolute;
  white-space: nowrap;
  transform: translateX(-10px);
  transition: 0.2s opacity, 0.2s visibility, 0.2s transform;
}

.social-icons-menu > li:hover span.social-label {
  opacity: 1 !important;
  visibility: visible;
  transform: translateX(10px);
  transition: 0.2s opacity, 0.2s visibility, 0.2s transform;
}
</style>
