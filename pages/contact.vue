<script setup>
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

    <div class="card lg:w-1/3 md:w-1/2 lg:mr-10 px-5 py-24 mx-auto flex flex-col">
      <h2 class="rainbow-text text-3xl lg:text-5xl font-bold mb-6">
        Get in Touch
      </h2>
      <p>
        Have a question 🤔? Want to give us some feedback? Report a bug 🐞? et cetera. Please fill out this contact form
        or you can
        <a href="mailto:contact@tokyotoolkit.com" class="text-teal-500 hover:underline">contact@tokyotoolkit.com</a> via
        email. 🥰
      </p>
      <ContactForm />
    </div>
  </div>
</template>

<style scoped>
div.contact {
  min-height: calc(100vh - 12.7vh);
}

.contact .card {
  @apply bg-white dark:bg-gray-800 p-8 relative z-10 shadow-md;
}
</style>
