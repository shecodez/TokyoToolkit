<script setup>
import { FormKitSchema } from '@formkit/vue'
import { getNode } from '@formkit/core'

const { data: contactFormJson } = await useAsyncData('contactFormJson', () => {
  return queryContent('forms', 'contact').findOne()
})

// TODO: optimize: this seems like a lot just to update the hint text on input...
const contactForm = ref({ message: '' })
const contactFormMessageLength = computed(() => contactForm.value.message.length || 0)
watch(contactFormMessageLength, (messageLength) => {
  getNode('contactmessage').props.help = `${messageLength} / 500`
})
// https://formkit.com/advanced/custom-inputs#displaying-values
function handleMessageInput() {
  // console.log('handleMessageInput called')
  // const node = getNode('contactmessage')
  // node.props.help = `${node.context.value.langth} / 500`
}

const state = reactive({
  loading: false,
  sent: false,
  error: null,
  bot: null,
  isBot: false,

  handleMessageInput,
})

// If all inputs are valid it fires the @submit event
async function postContactForm(formData, node) {
  state.loading = true

  try {
    if (formData.bot) {
      state.isBot = true
    }
    else {
    // await sendContactEmail(formData)
    }
  }
  catch (error) {
    node.setErrors(error)
    state.error = 'Error sending message, please try again later.'
  }
  finally {
    state.loading = false
    state.sent = true
  }
}

const config = useRuntimeConfig()
useHead({
  title: `Contact | ${config.public.appName}`,
})
</script>

<template>
  <div id="contact" class="contact p-10 lg:p-20 relative flex items-center">
    <div id="map-container" class="absolute inset-0 bg-gray-300 dark:bg-gray-800">
      <iframe
        width="100%"
        height="100%"
        frameborder="0"
        marginheight="0"
        marginwidth="0"
        title="map"
        scrolling="no"
        src="https://maps.google.com/maps?width=100%&amp;height=600&amp;hl=en&amp;q=Hachi%C5%8Dji+(shecodez)&amp;ie=UTF8&amp;t=&amp;z=15&amp;iwloc=B&amp;output=embed"
        style="filter: grayscale(1) contrast(1.2) opacity(0.4)"
      />
    </div>

    <div class="card md:w-2/3 lg:w-1/2 xl:w-1/3 xl:mr-28 mx-auto flex flex-col bg-white dark:bg-gray-800 p-8 relative z-10 shadow-md">
      <h2 class="rainbow-text text-3xl lg:text-5xl font-bold mb-6">
        Get in Touch
      </h2>
      <p>
        Have a question 🤔? Want to give us some feedback? Report a bug 🐞? et cetera. Please fill out this contact form
        or you can
        <a href="mailto:contact@tokyotoolkit.com" class="text-teal-500 hover:underline">contact@tokyotoolkit.com</a> via
        email. 🥰
      </p>

      <div v-if="state.isBot" class="alert bot-alert">
        🍯 Oh honey pot! We think not, you're a bot!
      </div>
      <div v-if="state.sent" class="alert" :class="state.error ? 'error-alert' : 'success-alert'">
        <span v-if="state.error">❗ {{ state.error }}</span>
        <span v-else>✔️ Message sent. Thanks!</span>
      </div>
      <FormKit v-else id="contactform" v-model="contactForm" type="form" :actions="false" form-class="mt-6" @submit="postContactForm">
        <FormKitSchema :schema="contactFormJson.body" :data="state" />
      </FormKit>
    </div>
  </div>
</template>

<style scoped>
div.contact {
  min-height: calc(100vh - 12vh);
}
</style>
