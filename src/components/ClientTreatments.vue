<template>
  <div class="mt-6 p-4 bg-gray-800 rounded shadow">
    <h2 class="text-xl font-bold mb-4">Tretmani i računi</h2>
    <ul class="space-y-4">
      <li
        v-for="(treatment, index) in treatments"
        :key="index"
        class="p-3 bg-gray-700 rounded"
      >
        <p><strong>Datum:</strong> {{ treatment.date }}</p>
        <p><strong>Tretman:</strong> {{ treatment.type }}</p>
        <p><strong>Zaposlenik:</strong> {{ treatment.employee }}</p>
        <p><strong>Cijena:</strong> €{{ treatment.price }}</p>
        <p>
          <strong>Račun:</strong>
          <span v-if="treatment.invoice">
            {{ treatment.invoice.number }}
          </span>
          <span v-else>
            <button
              @click="generateInvoice(treatment.id)"
              class="bg-indigo-600 px-3 py-1 text-sm rounded hover:bg-indigo-500"
            >
              Generiraj račun
            </button>
          </span>
        </p>
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

const treatments = ref([])

onMounted(() => {
  axios.get(`/api/clients/${props.client.id}/treatments`).then(res => {
    treatments.value = res.data
  })
})

function generateInvoice(treatmentId) {
  axios.post(`/api/treatments/${treatmentId}/generate-invoice`).then(res => {
    alert('Račun generiran!')
    treatments.value = treatments.value.map(t =>
      t.id === treatmentId ? { ...t, invoice: res.data.invoice } : t
    )
  })
}
</script>
