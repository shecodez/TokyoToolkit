<script setup>
// import useSupabase from '@/use/supabase';

const state = reactive({
  loading: false,
  email: '',
  sent: false,
  error: '',
})
// const { supabase } = useSupabase();
async function joinNewsletter() {
  // console.log('join Newsletter', state.email)
  //   try {
  //     state.loading = true;
  //     let { data, error, status } = await supabase.from('subscribers').upsert({
  //       email: state.email,
  //     });
  //     if (error && status !== 406) throw error;
  //     if (data) {
  //       state.sent = true;
  //       console.log('subscribed to newsletter', data);
  //     }
  //   } catch (e: any) {
  //     state.error = e.error_description || e.message;
  //   } finally {
  //     state.loading = false;
  //   }
}
</script>

<template>
  <form @submit.prevent="joinNewsletter">
    <div v-if="state.error" class="error-alert p-2 flex items-center my-1">
      🛑 {{ state.error }}
    </div>
    <div v-if="state.sent" class="success-alert p-2 flex items-center my-1">
      ✔️ We added you. Thanks!
    </div>

    <div class="form-control">
      <label for="email" class="text-xs font-simibold uppercase pb-2">Join our Community</label>
      <div class="flex items-center relative">
        <input
          v-model="state.email"
          name="email"
          required
          type="email"
          placeholder="your@email.com"
          class="w-full p-2 bg-transparent border pr-10"
        >
        <button class="absolute right-0 p-3 hover:text-teal-500" :class="state.loading && 'loading'">
          <div class="i-carbon:arrow-right" />
          <span class="sr-only">Subscribe</span>
        </button>
      </div>
      <p class="by-clicking dark:text-gray-400 mt-2 text-xs">
        By clicking
        <span class="i-carbon:arrow-right inline-block w-3 h-3" /> you agree to our
        <NuxtLink to="/legal/privacy">
          Privacy Policy
        </NuxtLink>
        and
        <NuxtLink to="/legal/terms">
          Terms of Use
        </NuxtLink>. We promise, no green eggs and spam from us. 😉
      </p>
    </div>
  </form>
</template>

<style scoped>
a {
  font-family: 'Marcellus SC', Georgia, serif;
  color: rgb(20, 184, 166);
  cursor: pointer;
  /* @apply text-teal-500 hover:text-teal-700 cursor-pointer; */
}
a:hover {
  color: rgb(15, 118, 110)
}

/* .by-clicking span svg {
  display: inline-block;
  width: 12px;
  height: 12px;
} */

.success-alert {
  border-left-width: 4px;
  border-left-style: solid;
  border-color: rgb(22, 163, 74);
  background-color: rgba(74, 222, 128, 0.2);
  color: rgb(22, 163, 74);
  /* @apply border-l-4 border-green-600 bg-green-400 bg-opacity-20 text-green-600; */
}
.error-alert {
  border-left-width: 4px;
  border-left-style: solid;
  border-color: rgb(220, 38, 38);
  background-color: rgba(248, 113, 113, 0.2);
  color: rgb(220, 38, 38);
  /* @apply border-l-4 border-red-600 bg-red-400 bg-opacity-20 text-red-600; */
}
</style>
