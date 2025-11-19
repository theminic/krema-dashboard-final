<template>
  <div>
    <h1 class="text-2xl font-semibold mb-4">Klijenti</h1>
    <input
      v-model="search"
      type="text"
      placeholder="Pretraži klijente..."
      class="mb-4 p-2 rounded bg-gray-700 text-white w-full"
    />
    <ul>
      <li
        v-for="client in filteredClients"
        :key="client.id"
        @click="selectClient(client)"
        class="cursor-pointer p-3 rounded bg-gray-800 mb-2 hover:bg-gray-700"
      >
        {{ client.name }} – {{ client.email }}
      </li>
    </ul>

    <ClientProfile v-if="selectedClient" :client="selectedClient" />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import ClientProfile from './ClientProfile.vue'

const search = ref('')
const selectedClient = ref(null)

const clients = ref([
  { id: 1, name: 'Ana K.', email: 'ana@example.com' },
  { id: 2, name: 'Ivan M.', email: 'ivan@example.com' }
])

const filteredClients = computed(() => {
  return clients.value.filter(client =>
    client.name.toLowerCase().includes(search.value.toLowerCase())
  )
})

function selectClient(client) {
  selectedClient.value = client
}
</script>
