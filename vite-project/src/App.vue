<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { useMessageStore } from './stores/message'
import { storeToRefs } from 'pinia'

const store = useMessageStore()
const { message } = storeToRefs(store)
</script>

<template>
  <header class="max-h-screen leading-normal flex flex-col justify-center bg-yellow-400">
    <div id="flashMessage" v-if="message" class="bg-yellow-100 transition duration-3000">
      <h4>{{ message }}</h4>
    </div>
    <nav class="p-5 text-white">
      <div class="container mx-auto">
        <div class="flex justify-between space-x-4">
          <RouterLink :to="{ name: 'event-list' }" class="hover:text-gray-500">Home</RouterLink>
          <RouterLink :to="{ name: 'about' }" class="hover:text-gray-500">About</RouterLink>
          <RouterLink :to="{ name: 'Organize' }" class="hover:text-gray-500">Organizer</RouterLink>
          <RouterLink :to="{ name: 'students' }" class="hover:text-gray-500">Students</RouterLink>
        </div>
      </div>
    </nav>
  </header>

  <RouterView />
</template>

<style>
@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }
}
</style>