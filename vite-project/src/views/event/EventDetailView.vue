<script setup lang="ts">
import type { EventItem } from '@/type'
import type { PropType } from 'vue'

defineProps({
  event: {
    type: Object as PropType<EventItem>,
    require: true
  }
})
</script>

<template>
  <div class="mx-auto w-1/2 mt-10 flex flex-col items-center">
    <div class="p-5 w-64 cursor-pointer border border-gray-600 mb-2" v-if="event">
      <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
      <p>{{ event.description }}</p>
    </div>
  </div>
</template>