<script setup>
const {
  params: { topic },
} = useRoute()

const posts = await queryContent('blog', `${topic.toLowerCase().replace(' ', '-')}`)
  .only(['_path', 'title', 'description', 'date', 'cover_image'])
  .sort({ date: -1 })
  .find()
// const { data: posts } = useAsyncData(
//   'posts-by-topic',
//   async () => {
//     return await blogQuery
//   },
//   { initialCache: false },
// )

const config = useRuntimeConfig()
useHead({
  title: `${topic} | ${config.public.appName}`,
  meta: [{ name: 'description', content: `${config.public.appName}'s ${topic} posts` }],
})
</script>

<template>
  <div class="blogTopic">
    <h1 class="title my-10 text-center capitalize">
      <span v-if="topic">"{{ topic.replace('-', ' ') }}"</span>
    </h1>

    <section class="posts pb-10">
      <ul v-if="posts.length" class="flex items-center justify-center gap-2">
        <template v-for="(p, i) in posts" :key="`post-${i}`">
          <li class="p-4 border">
            <NuxtLink :to="p._path" class="font-semibold">
              {{ p.title }}
            </NuxtLink>
          </li>
        </template>
      </ul>
      <div v-else class="text-center">
        No posts found
      </div>
    </section>
  </div>
</template>
