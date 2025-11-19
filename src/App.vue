<template>
  <div class="min-h-screen flex">
    <aside class="w-64 bg-gray-800 p-4 hidden md:block">
      <h2 class="text-xl font-bold mb-6">Krema CRM</h2>
      <nav class="space-y-4">
        <a href="#" class="block hover:text-indigo-400">Dashboard</a>
        <a href="#" class="block hover:text-indigo-400">Klijenti</a>
        <a href="#" class="block hover:text-indigo-400">Tretmani</a>
        <a href="#" class="block hover:text-indigo-400">Statistike</a>
      </nav>
    </aside>
    <main class="flex-1 p-6">
      <router-view />
    </main>
  </div>
</template>
