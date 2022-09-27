<script setup>
const props = defineProps(['isOpen', 'css'])
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
    <div v-if="isOpen" class="modal-container">
      <div ref="overlay" class="overlay" />

      <div ref="modal" class="relative" :class="css">
        <slot />
      </div>

      <button class="close-btn" @click="$emit('close')">
        <div class="i-carbon:close" />
        <span class="text-sm">(Esc)</span>
      </button>
    </div>
  </Teleport>
</template>

<style scoped>
.modal-container {
  @apply fixed z-30 w-full h-full inset-0 flex items-center justify-center;
}
.modal-container .overlay {
  backdrop-filter: saturate(100%) blur(10px);
  @apply fixed w-full h-full bg-black bg-opacity-80 overflow-y-auto;
}

.close-btn {
  @apply absolute top-4 right-4 text-white opacity-80 hover:opacity-100 flex flex-col items-center;
}
</style>
