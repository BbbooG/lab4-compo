<template>
  <RouterLink :to="{ name: 'event-detail', params: { id: event?.id } }" class="event-link">
    <div class="event-class">
      <div class="event-card">
        <span> @{{ event?.time }} on {{ event?.date }}</span>
        <h4>{{ event?.title }}</h4>
      </div>
    </div>
  </RouterLink>
</template>

<script setup lang="ts">
import { type EventItem } from '@/type'
import { PropTypes } from 'vue'
const props = defineProps({
  event: {
    type: Object as PropTypes<EventItem>,
    requier: true
  }
})
</script>

<style scoped>
.event-card {
  padding: 20px;
  width: 250px;
  cursor: pointer;
  border: 1px solid #b3cff1;
  margin-bottom: 18px;
  margin-top: 20px;
}
.event-link {
  color: #b3cff1;
  text-decoration: none;
}
</style>
