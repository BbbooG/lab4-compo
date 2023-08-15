<template>
  <RouterLink :to="{ name: 'event-detail', params: { id: event?.id } }" class="event-link">
    <div class="event-class">
      <div class="p-5 w-64 m-5 cursor-pointer border border-gray-600 mb-5">
        <span> @{{ event?.time }} on {{ event?.date }}</span>
        <h4 class="mt-2">{{ event?.title }}</h4>
      </div>
    </div>
  </RouterLink>
</template>

<script setup lang="ts">
import { type EventItem } from '@/type'
import type{ PropType } from 'vue'
const props = defineProps({
  event: {
    type: Object as PropType<EventItem>,
    requier: true
  }
})
</script>