<script setup>
import { formatPrice } from '../../utils'

// products.json src: https://fakestoreapi.com/docs;
const { data: products } = await useAsyncData('products', () => {
  return queryContent('shop').find()
})

// create an array of categories from the products
const categories = products.value[0].body.reduce((acc, product) => {
  if (!acc.includes(product.category))
    acc.push(product.category)

  return acc
}, [])

const route = useRoute()
const router = useRouter()
const activeCategory = ref(route.query.category ? route.query.category : '')
function setCategory(category) {
  activeCategory.value = category
  if (category) {
    router.push({
      path: '/shop',
      query: {
        category: activeCategory.value,
      },
    })
  }
  else {
    // clear the query
    router.replace({ query: {} })
  }
}

watch(route, (route) => {
  if (activeCategory.value !== route.query.category)
    setCategory(route.query.category)
})

const filteredProducts = computed(() => {
  if (!activeCategory.value)
    return products.value[0].body

  return products.value[0].body.filter((product) => {
    return product.category.toLowerCase() === activeCategory.value.toLowerCase()
  })
})

const config = useRuntimeConfig()
useHead({
  title: `${activeCategory.value ? activeCategory.value : 'Shop'} | ${config.public.appName}`,
})
</script>

<template>
  <div class="shop">
    <h1 class="title mt-10 text-center">
      Shop
      <span v-if="activeCategory">"{{ activeCategory }}"</span>
    </h1>
    <div v-if="products" class="container px-4 lg:px-0 mx-auto">
      <section v-if="categories" class="pt-6">
        <div class="flex item-center gap-4 mb-4">
          <h3 class="text-lg">
            Filter Category
          </h3>
          <button
            v-if="activeCategory"

            class="flex items-center gap-2 px-2 py-1 bg-gray-300 dark:bg-gray-900 uppercase rounded-sm text-sm tracking-wide"
            @click="setCategory(null)"
          >
            clear <div class="i-carbon:close" />
          </button>
        </div>
        <div class="flex flex-wrap items-center gap-4 mb-4">
          <template v-for="(c, i) in categories" :key="`category-${i}`">
            <button
              class="px-3 py-1.5 rounded-sm text-sm capitalize flex-shrink-0"
              :class="c === activeCategory ? 'rainbow-bg' : 'bg-gray-300 dark:bg-gray-900'"
              @click="setCategory(c)"
            >
              <span class="tracking-wide">{{ c }}</span>
            </button>
          </template>
        </div>
      </section>
      <section
        v-if="filteredProducts"
        class="py-10 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8"
      >
        <template v-for="(p, i) in filteredProducts" :key="`product-${i}-${p.id}`">
          <NuxtLink :to="`/shop/${p.id}`" class="">
            <img :src="p.image" :alt="p.title" class="w-full h-[300px] object-contain object-center bg-white rounded">
            <div class="py-3">
              <h2 class="text-sm">
                {{ p.title }}
              </h2>
              <p class="font-bold mt-2">
                {{ formatPrice(p.price, 'USD') }}
              </p>
            </div>
          </NuxtLink>
        </template>
      </section>
    </div>
  </div>
</template>

