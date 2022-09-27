<script setup>
const openSearch = ref(false)
function openModal() {
  openSearch.value = true
}
function closeModal() {
  openSearch.value = false
}

const filters = ['All', 'Blog', 'Shop']
const state = reactive({
  filter: 'All',
  query: '',
  results: [],

  loading: false,
  error: null,
})
</script>

<template>
  <client-only>
    <button title="Search" @click="openModal">
      <div class="i-carbon:search" />
    </button>

    <Modal
      :is-open="openSearch"
      css="w-11/12 md:max-w-lg mx-auto rounded shadow-lg bg-white dark:bg-gray-800"
      @close="closeModal"
    >
      <form class="search-form">
        <div class="flex rounded-t-lg focus-within:ring">
          <select v-model="state.filter" class="filter rounded-tl focus:outline-none p-3 bg-transparent">
            <template v-for="(f, i) in filters" :key="`search-filter-${i}`">
              <option :value="f">
                {{ f }}
              </option>
            </template>
          </select>

          <input v-model="state.query" type="text" placeholder="Search..." class="flex-1 focus:outline-none p-3 bg-transparent">

          <button type="button" class="px-3.5 bg-teal-500 rounded-tr">
            <div class="i-carbon:search" />
          </button>
        </div>
      </form>

      <div class="p-4 border-y border-dashed border-gray-500 border-opacity-50">
        <div v-if="state.results.length">
          {{ state.results }}
        </div>
        <div v-else class="py-6 text-center opacity-60">
          No recent searches
        </div>
      </div>

      <div class="flex items-center justify-between rounded-b-lg">
        <button class="p-2 bg-red-400 hover:bg-red-500 rounded-bl" @click="closeModal">
          <div class="i-carbon:close text-sm" />
        </button>
        <div class="text-xs font-bold text-right px-4">
          Hits: {{ state.results.length }}
        </div>
      </div>
    </Modal>
  </client-only>
</template>

<style scoped>
select.filter option {
  background-color: black;
  /* @apply bg-black; */
}
</style>
