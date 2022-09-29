<script setup>
const config = useRuntimeConfig()
useHead({
  title: `FAQ | ${config.public.appName}`,
})
</script>

<template>
  <div class="container mx-auto py-12 flex-1">
    <h1 class="title mb-4">
      FAQ
    </h1>

    <client-only>
      <ContentDoc>
        <template #default="{ doc }">
          <section>
            <article class="px-4 lg:px-0 prose dark:prose-invert prose-sm lg:prose-lg">
              <ContentRenderer :value="doc" />
            </article>
          </section>
        </template>
        <template #not-found>
          <p>No content found.</p>
        </template>
      </ContentDoc>
    </client-only>
  </div>
</template>
