<template>
  <div class="mt-6 p-4 bg-gray-800 rounded shadow">
    <h2 class="text-xl font-bold mb-2">Profil klijenta</h2>
    <p><strong>Ime:</strong> {{ client.name }}</p>
    <p><strong>Email:</strong> {{ client.email }}</p>

    <h3 class="mt-4 font-semibold">Zadnje ocjene</h3>
    <ul class="mt-2 space-y-2">
      <li v-for="(feedback, index) in feedbacks" :key="index" class="bg-gray-700 p-2 rounded">
        Ocjena: {{ feedback.rating }} ★<br />
        "{{ feedback.comment }}"
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

const feedbacks = ref([])

onMounted(() => {
  axios.get(`/api/clients/${props.client.id}/feedback`).then(res => {
    feedbacks.value = res.data.feedback
  })
})
</script>
