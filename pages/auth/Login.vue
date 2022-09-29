<script setup>
import { FormKitSchema, clearErrors } from '@formkit/vue'
import { getNode, reset } from '@formkit/core'
definePageMeta({
  layout: 'auth',
})

const { data: loginFormJson } = await useAsyncData('loginFormJson', () => {
  return queryContent('forms', 'login').findOne()
})

const showHidePassword = () => {
  const node = getNode('loginpassword')
  node.props.suffixIcon = node.props.suffixIcon === 'eye' ? 'eyeClosed' : 'eye'
  node.props.type = node.props.type === 'password' ? 'text' : 'password'
}

const postForgotPassword = () => {
  clearErrors('loginform', true) // TODO: use: 🐛? it doesn't clear the form errors

  const node = getNode('loginemail')
  if (!node.context.state.valid) {
    reset('loginform') // TODO: remove: b/c resetting the form clears all form inputs
    node.setErrors({
      email: 'A valid email is required to reset your password.',
    })
  }
  else {
    // send email
    // console.log('Send Email', node.context.value)
    // try { } catch (error) { } finally { }
  }
}

// async function postPasswordlessLogin (email) {}

const state = reactive({
  loading: false,

  showHidePassword,
  postForgotPassword,
  // postPasswordLessLogin
})

function resetForgotPassErr() {
  getNode('loginemail').setErrors({ email: '' })
}

// If all inputs are valid it fires the @submit event
async function postLoginForm(credentials, node) {
  state.loading = true
  try {
    // await login(credentials.email, credentials.password)
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
  title: `Login | ${config.public.appName}`,
})
</script>

<template>
  <div class="login-page">
    <FormKit id="loginform" type="form" :actions="false" form-class="flex flex-col" @submit-raw="resetForgotPassErr" @submit="postLoginForm">
      <FormKitSchema :schema="loginFormJson.body" :data="state" />
    </FormKit>

    <p class="text-sm text-center mt-4">
      Need an account?
      <NuxtLink to="/auth/register" class="text-teal-500 hover:underline">
        Register
      </NuxtLink>
    </p>
  </div>
</template>

