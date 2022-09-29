<script setup>
const state = reactive({
  authenticated: false,

  loading: false,
  error: null,
})

const authProviders = [
  { icon: 'i-carbon:logo-google', label: 'Google' },
  { icon: 'i-carbon:logo-discord', label: 'Discord' },
  { icon: 'i-carbon:logo-twitter', label: 'Twitter' },
]
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <div class="absolute top-6 left-8 flex gap-2.5 items-center">
      <div class="i-carbon:tools-alt" />
      <NuxtLink to="/" class="site-logo rainbow-text font-black text-lg lg:text-2xl">
        Tokyo<span class="heading-font">Toolkit</span>
      </NuxtLink>
    </div>

    <main ref="main" class="min-h-screen flex items-center justify-center">
      <div class="flex w-11/12 md:w-2/3 lg:w-2/5 rounded overflow-hidden">
        <div class="hidden w-2/5 md:flex items-center justify-center bg-white bg-opacity-80 rounded-tl-8">
          <img src="/TokyoToolKitsune.jpg" alt="tokyo" class="rounded-full p-10">
        </div>
        <div class="flex-1 md:w-3/5 py-10 px-4 md:px-8 bg-black bg-opacity-40 rounded-tl-8 md:rounded-tl-none rounded-br-8">
          <section v-if="state.authenticated" class="flex flex-col items-center justify-center h-full">
            <h3>You are logged in as:</h3>
            <b class="pb-2">loggedInUser@Email.com</b>
            <br>
            <button class="py-1 px-2 bg-red-400 hover:bg-red-600 rounded">
              Logout
            </button>
          </section>
          <section v-else>
            <slot />
            <div class="other-auth-providers">
              <div class="divider uppercase py-4 text-center">
                or
              </div>
              <ul class="flex items-center justify-center gap-4">
                <template v-for="(p, i) in authProviders" :key="`authProvider-${i}`">
                  <button class="btn" :class="state.loading && 'loading'" :title="p.label">
                    <div :class="p.icon" />
                    <span class="sr-only">{{ p.label }}</span>
                  </button>
                </template>
              </ul>
            </div>
          </section>
        </div>
      </div>
    </main>
    <Footer />
    <SocialLinksMenu />
  </div>
</template>

<style>
  .mb-3 {
    margin-bottom: 0.75rem;
  }
  .my-3 {
    margin-top: 0.75rem;
    margin-bottom: 0.75rem;
  }
  .w-5 {
    width: 1.5rem;
  }
  .top-2 {
    top: 0.5rem;
  }
  .right-2 {
    right: 0.5rem;
  }
  .text-red-500 {
    color: rgb(239, 68, 68)
  }
  .self-end {
    align-self: flex-end;
  }
  .error-messages {
    padding: 0.5rem;
    border-left-width: 4px;
    border-left-style: solid;
    border-color: rgb(239, 68, 68);
    background-color: rgba(248, 113, 113, 0.2);
    color: rgb(239, 68, 68);
    /* @apply p-2 border-l-4 border-red-500 bg-red-400 bg-opacity-20 text-red-500; */
  }
  .formkit-message {
    color: rgb(239, 68, 68);
  }
  .formkit-suffix-icon svg,
  .formkit-prefix-icon svg {
    width: 24px;
    height: 24px;
  }
  </style>
