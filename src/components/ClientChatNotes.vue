<template>
  <div class="mt-6 p-4 bg-gray-800 rounded shadow">
    <h2 class="text-xl font-bold mb-4">Interne bilješke</h2>

    <form @submit.prevent="sendNote" class="mb-4">
      <textarea v-model="newMessage" class="w-full p-2 rounded bg-gray-700 text-white" rows="3" placeholder="Unesi bilješku..."></textarea>
      <button type="submit" class="mt-2 bg-indigo-600 px-4 py-2 rounded hover:bg-indigo-500">Spremi bilješku</button>
    </form>

    <ul class="space-y-4">
      <li v-for="note in notes" :key="note.id" class="bg-gray-700 p-3 rounded">
        <p class="text-sm text-gray-300">{{ note.user.name }} – {{ formatDate(note.created_at) }}</p>
        <p class="mt-1">{{ note.message }}</p>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const props = defineProps({
  client: Object
})

const notes = ref([])
const newMessage = ref('')

function loadNotes() {
  axios.get(`/api/clients/${props.client.id}/chat-notes`).then(res => {
    notes.value = res.data
  })
}

function sendNote() {
  if (!newMessage.value) return

  axios.post(`/api/clients/${props.client.id}/chat-notes`, {
    message: newMessage.value
  }).then(res => {
    notes.value.unshift(res.data)
    newMessage.value = ''
  })
}

function formatDate(date) {
  return new Date(date).toLocaleString()
}

onMounted(loadNotes)
</script>
