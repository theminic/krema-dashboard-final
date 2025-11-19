<template>
  <div>
    <h1 class="text-2xl font-semibold mb-6">Statistike i analitika</h1>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
      <div class="bg-gray-800 p-4 rounded-lg">
        <p class="text-gray-400">Ukupna zarada</p>
        <h2 class="text-2xl font-bold">€12,530</h2>
      </div>
      <div class="bg-gray-800 p-4 rounded-lg">
        <p class="text-gray-400">Broj tretmana</p>
        <h2 class="text-2xl font-bold">214</h2>
      </div>
      <div class="bg-gray-800 p-4 rounded-lg">
        <p class="text-gray-400">Prosječna ocjena</p>
        <h2 class="text-2xl font-bold">4.7 ★</h2>
      </div>
    </div>

    <div class="bg-gray-800 p-6 rounded-lg">
      <canvas id="treatmentChart" height="100"></canvas>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import Chart from 'chart.js/auto'

onMounted(() => {
  const ctx = document.getElementById('treatmentChart')
  new Chart(ctx, {
    type: 'line',
    data: {
      labels: ['Pon', 'Uto', 'Sri', 'Čet', 'Pet', 'Sub', 'Ned'],
      datasets: [{
        label: 'Broj tretmana',
        data: [12, 19, 14, 8, 16, 11, 9],
        borderWidth: 2,
      }]
    },
    options: {
      responsive: true,
      scales: {
        y: {
          beginAtZero: true
        }
      }
    }
  })
})
</script>
