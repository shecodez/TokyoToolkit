<script setup>
import { FormKitSchema } from '@formkit/vue'
import { getNode } from '@formkit/core'
definePageMeta({
  layout: 'auth',
})

const { data: registerFormJson } = await useAsyncData('registerFormJson', () => {
  return queryContent('forms', 'register').findOne()
})

/*
<Formkit
  label="Username",
  validation="(500)postCheckUsernameExists"
  validation-visibility="live",
  :validation-rules="{ postCheckUsernameExists }"
  :validation-messages=" {
    postCheckUsernameExists: 'Sorry, that username is taken. Try "test123"'
  }"
*/
const postCheckUsernameExists = function ({ value }) {
  return new Promise((resolve) => {
    setTimeout(() => resolve(value === 'test123'))
  })
}

const showHidePassword = () => {
  const node = getNode('registerpassword')
  node.props.suffixIcon = node.props.suffixIcon === 'eye' ? 'eyeClosed' : 'eye'
  node.props.type = node.props.type === 'password' ? 'text' : 'password'
}

const state = reactive({
  loading: false,

  showHidePassword,
  // postCheckUsernameExists,
  // postPasswordLessRegister
})

// If all inputs are valid it fires the @submit event
async function postRegisterForm(credentials, node) {
  state.loading = true
  try {
    // await register(credentials.username, credentials.email, credentials.password)
  }
  catch (error) {
    node.setErrors(error)
  }
  finally {
    state.loading = false
  }
}

const config = useRuntimeConfig()
useHead({
  title: `Register | ${config.public.appName}`,
})
</script>

<template>
  <div class="register-page">
    <FormKit id="registerform" type="form" :actions="false" @submit="postRegisterForm">
      <FormKitSchema :schema="registerFormJson.body" :data="state" />
    </FormKit>

    <p class="text-sm text-center mt-4">
      Have an account?
      <NuxtLink to="/auth/login" class="text-teal-500 hover:underline">
        Login
      </NuxtLink>
    </p>
  </div>
</template>
