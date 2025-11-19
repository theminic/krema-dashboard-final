<template>
  <div>
    <h1 class="text-2xl font-semibold mb-4">Kalendar termina</h1>
    <FullCalendar
      :plugins="calendarPlugins"
      :initialView="'dayGridMonth'"
      :events="appointments"
      :eventColor="'#6366F1'"
      class="bg-gray-800 text-white rounded shadow p-4"
    />
  </div>
</template>

<script setup>
import FullCalendar from '@fullcalendar/vue3'
import dayGridPlugin from '@fullcalendar/daygrid'
import interactionPlugin from '@fullcalendar/interaction'

const calendarPlugins = [dayGridPlugin, interactionPlugin]

const appointments = [
  {
    title: 'Tretman - Ana',
    start: '2025-11-19',
  },
  {
    title: 'Tretman - Ivan',
    start: '2025-11-20',
  }
]
</script>

<style scoped>
.fc {
  --fc-bg-event-opacity: 1;
}
</style>
