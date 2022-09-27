<script setup>
const openCartDrawer = ref(false)
function openDrawer() {
  openCartDrawer.value = true
}
function closeDrawer() {
  openCartDrawer.value = false
}

const state = reactive({
  cart: [],

  loading: false,
  error: null,
})
</script>

<template>
  <client-only>
    <button title="Shopping Cart" @click="openDrawer">
      <div class="i-carbon:shopping-cart" />
    </button>

    <Drawer
      :is-open="openCartDrawer"
      css="w-80 ml-auto shadow-lg bg-white dark:bg-black"
      :show-right="true"
      @close="closeDrawer"
    >
      <div class="p-4 border-y border-dashed border-gray-500 border-opacity-50">
        <h2 class="text-xl text-center">
          Shopping Cart
        </h2>
        <pre>{{ state.results }}</pre>
      </div>
    </Drawer>
  </client-only>
</template>

<style scoped></style>
