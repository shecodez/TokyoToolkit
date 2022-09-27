<script setup>
const {
  params: { tag },
} = useRoute()

const filter = tag.split(',')
const blogQuery = queryContent('blog')
  .only(['_path', 'title', 'description', 'date', 'cover_image'])
  .where({ tags: { $contains: filter } })
  // .sort({ date: -1 })
  .find() // ; <ContentList :query="blogQuery">
const { data: posts } = await useAsyncData('posts-by-tag', async () => {
  return await blogQuery
})

const config = useRuntimeConfig()
useHead({
  title: `${tag} | ${config.public.appName}`,
  meta: [{ name: 'description', content: `${config.public.appName}'s ${tag} posts` }],
})
</script>

<template>
  <div class="blogTag">
    <h1 class="title my-10 text-center">
      Posts with <span v-if="tag">"{{ filter.toString() }}"</span> Tag
    </h1>
    <section class="posts pb-10">
      <ul class="flex items-center justify-center gap-2">
        <template v-for="(p, i) in posts" v-if="posts.length" :key="`post-${i}`">
          <li class="p-4 border">
            <NuxtLink :to="p._path" class="font-semibold">
              {{ p.title }}
            </NuxtLink>
          </li>
        </template>
      </ul>
    </section>
  </div>
</template>
