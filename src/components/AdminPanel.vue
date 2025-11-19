<template>
  <div>
    <h1 class="text-2xl font-semibold mb-6">Admin Panel</h1>

    <!-- Dodaj zaposlenika -->
    <div class="mb-8 bg-gray-800 p-6 rounded shadow">
      <h2 class="text-xl font-bold mb-4">Dodaj zaposlenika</h2>
      <form @submit.prevent="addStaff">
        <input v-model="staff.name" placeholder="Ime" class="p-2 bg-gray-700 rounded text-white w-full mb-2" />
        <input v-model="staff.email" placeholder="Email" class="p-2 bg-gray-700 rounded text-white w-full mb-2" />
        <input v-model="staff.password" type="password" placeholder="Lozinka" class="p-2 bg-gray-700 rounded text-white w-full mb-2" />
        <button class="bg-indigo-600 px-4 py-2 rounded hover:bg-indigo-500">Dodaj</button>
      </form>
    </div>

    <!-- Dodaj tretman -->
    <div class="bg-gray-800 p-6 rounded shadow">
      <h2 class="text-xl font-bold mb-4">Dodaj tretman</h2>
      <form @submit.prevent="addTreatment">
        <input v-model="treatment.name" placeholder="Naziv tretmana" class="p-2 bg-gray-700 rounded text-white w-full mb-2" />
        <input v-model="treatment.price" type="number" placeholder="Cijena" class="p-2 bg-gray-700 rounded text-white w-full mb-2" />
        <input v-model="treatment.margin" type="number" placeholder="Zarada salona" class="p-2 bg-gray-700 rounded text-white w-full mb-2" />
        <input v-model="treatment.employee_cut" type="number" placeholder="Zarada zaposlenika" class="p-2 bg-gray-700 rounded text-white w-full mb-2" />
        <button class="bg-indigo-600 px-4 py-2 rounded hover:bg-indigo-500">Dodaj</button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const staff = ref({
  name: '',
  email: '',
  password: ''
})

const treatment = ref({
  name: '',
  price: '',
  margin: '',
  employee_cut: ''
})

function addStaff() {
  axios.post('/api/staff', staff.value).then(() => {
    alert('Zaposlenik dodan')
    staff.value = { name: '', email: '', password: '' }
  })
}

function addTreatment() {
  axios.post('/api/treatments', treatment.value).then(() => {
    alert('Tretman dodan')
    treatment.value = { name: '', price: '', margin: '', employee_cut: '' }
  })
}
</script>
