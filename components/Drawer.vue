<script setup>
const props = defineProps(['isOpen', 'css', 'showRight'])
defineEmits(['close'])

watch(
  () => props.isOpen,
  (isOpen) => {
    const bodyEl = document.querySelector('body')
    if (isOpen) {
      // Disable scroll
      bodyEl.style.overflow = 'hidden'
    }
    else {
      // Enable scroll
      bodyEl.style.overflow = 'auto'
    }
  },
)
</script>

<template>
  <Teleport to="body">
    <div v-if="isOpen" class="drawer-container fixed z-30 w-full min-h-screen inset-0 flex">
      <div ref="overlay" class="overlay fixed w-full h-full bg-black bg-opacity-80 overflow-y-auto" />

      <div ref="drawer" class="relative" :class="css">
        <slot />
      </div>

      <button class="close-btn absolute top-4 text-white opacity-80 hover:opacity-100 flex flex-col items-center" :class="showRight ? 'left-4' : 'right-4'" @click="$emit('close')">
        <div class="i-carbon:close" />
        <span class="text-sm">(Esc)</span>
      </button>
    </div>
  </Teleport>
</template>

<style scoped>
.drawer-container .overlay {
  backdrop-filter: saturate(100%) blur(10px);
  /* @apply fixed w-full h-full bg-black bg-opacity-80 overflow-y-auto; */
}
</style>
