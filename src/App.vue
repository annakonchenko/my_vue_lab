<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="max-w-4xl mx-auto">
      <nav class="p-4 bg-gray-100 rounded-b-lg shadow-md">
        <RouterLink to="/" class="mr-4 text-blue-600 hover:text-blue-800">Home</RouterLink>
<RouterLink to="/about" class="mr-4 text-blue-600 hover:text-blue-800">About</RouterLink>
<RouterLink to="/contact" class="text-blue-600 hover:text-blue-800">Contact</RouterLink>
      </nav>
    </div>
  </header>

  <main class="max-w-4xl mx-auto mt-5">
    <RouterView />
  </main>
</template>s