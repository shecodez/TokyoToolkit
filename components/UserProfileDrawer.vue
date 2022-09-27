<script setup>
const openCartDrawer = ref(false)
function openDrawer() {
  openCartDrawer.value = true
}
function closeDrawer() {
  openCartDrawer.value = false
}

const state = reactive({
  loading: false,
  error: null,
})
</script>

<template>
  <client-only>
    <button title="profile" @click="openDrawer">
      <div class="i-carbon:user-avatar-filled" />
    </button>

    <Drawer
      :is-open="openCartDrawer"
      css="w-80 ml-auto shadow-lg bg-white dark:bg-black"
      :show-right="true"
      @close="closeDrawer"
    >
      <div class="p-4 border-y border-dashed border-gray-500 border-opacity-50">
        <h2 class="text-xl text-center">
          Profile
        </h2>
      </div>
    </Drawer>
  </client-only>
</template>

<style scoped></style>
