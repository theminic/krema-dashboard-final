<template>
  <div class="flex items-center justify-center min-h-screen bg-gray-900 text-white">
    <form @submit.prevent="login" class="bg-gray-800 p-6 rounded shadow-md w-full max-w-md">
      <h1 class="text-2xl font-bold mb-6">Prijava u sustav</h1>

      <input v-model="email" type="email" placeholder="Email" class="w-full mb-4 p-2 bg-gray-700 rounded" />
      <input v-model="password" type="password" placeholder="Lozinka" class="w-full mb-4 p-2 bg-gray-700 rounded" />
      <button type="submit" class="w-full bg-indigo-600 py-2 rounded hover:bg-indigo-500">Prijavi se</button>

      <p v-if="error" class="mt-4 text-red-400">{{ error }}</p>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const email = ref('')
const password = ref('')
const error = ref('')

function login() {
  axios.post('/api/login', {
    email: email.value,
    password: password.value
  }).then(res => {
    localStorage.setItem('token', res.data.token)
    window.location.href = '/dashboard'
  }).catch(() => {
    error.value = 'Neispravni podaci'
  })
}
</script>
