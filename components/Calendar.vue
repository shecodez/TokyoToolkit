<script setup>
// const { $fullCalendar } = useNuxtApp();
// const FullCalendar = $fullCalendar();

defineProps(['calendarOptions'])
</script>

<template>
  <div>
    Calendar Component
  <!-- <FullCalendar :options="{ ...FullCalendar.options, ...calendarOptions }" /> -->
  </div>
</template>

<style>
/* .fc .fc-daygrid-day-frame {
  aspect-ratio: 1;
} */
@media only screen and (max-width: 600px) {
  .fc .fc-toolbar {
    flex-direction: column;
  }
}
.dark .fc .fc-popover {
  background-color: #000;
}
</style>
