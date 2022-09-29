<script setup>
import tokyoImg from '@/assets/images/tokyo.png'

const timeline = [
  { time: '09/12/2022', text: 'Started building TokyoToolkit.com' },
  { time: '09/22/2022', text: 'Looking for the perfect house in Japan here\'s my wishlist (link to blog post)' },
]
</script>

<template>
  <div class="about relative flex items-center" :style="{ 'background-image': `url(${tokyoImg})`, 'background-position': 'center', 'background-size': 'cover' }">
    <!-- <img src="~/assets/images/tokyo.png" alt="tokyo" class="absolute inset-0"> -->
    <div class="card md:w-2/3 lg:w-1/2 xl:w-1/3 md:ml-20 lg:ml-40 bg-white dark:bg-gray-800 px-4 md:px-8 py-8 relative z-10">
      <article class="prose dark:prose-invert prose-sm lg:prose-lg">
        <h1>About</h1>
        <p>
          I designed TokyoToolkit.com to be a place for DIY interior / exterior design tutorials, workshops,
          documentaries, interviews, reviews, podcasts, toolkits, and exploration. A space for community, global communications,
          and all things Japan.
        </p>
        <p>
          For quite a while now my dream has been to buy an old traditional style house in Japan, preferably a
          fixer-upper, so I can restore it back to its former glory while simultaneously cramming in as many modern
          conveniences in it as I can. Finally I feel (and I hope the ‘Rona also feels) it’s time to stop dreaming and
          in the immortal words of Shia LeBeouf “<a href="https://youtu.be/ZXsQAXx_ao0" target="_blank">Just Do It</a>” (https://youtu.be/ZXsQAXx_ao0).
        </p>
        <p>
          So here’s to our little community! *Somebody pop the champagne* I hope by sharing my thoughts, and journey
          here, and highlighting others' thoughts and journeys, I can help YOU realize your dream of renovating a house,
          if not in japan, feels just like Japan full of wabi-sabi, and zen interior / exterior design aesthetics.
        </p>
      </article>
    </div>

    <section class="timeline absolute bottom-0 left-0 z-10 h-20 flex items-center w-full">
      <h2 class="text-2xl p-4">
        Timeline:
      </h2>
      <ul class="flex gap-4 divide-x">
        <template v-for="(t, i) in timeline" :key="`timeline-${i}`">
          <li class="text-xs px-4">
            <b>{{ t.time }}</b>
            <p>{{ t.text }}</p>
          </li>
        </template>
      </ul>
    </section>
  </div>
</template>

<style scoped>
div.about {
  min-height: calc(100vh - 12vh);
}

/*section.timeline {
   backdrop-filter: saturate(180%) blur(20px);
  @apply bg-white dark:bg-black bg-opacity-40 dark:bg-opacity-40;
}*/
</style>
