<template>
  <div class="organize">
    <p>{{ event.category }}</p>
    <p>{{ event.organizer }}</p>
  </div>
</template>

<script setup lang="ts">
import { type EventItem } from '@/type'
import { PropTypes } from 'vue'

const props = defineProps({
  event: {
    type: Object as PropTypes<EventItem>,
    require: true
  }
})
</script>

<style scoped>
.organize {
  padding: 20px;
  width: 250px;
  cursor: pointer;
  border: 1px solid #b3cff1;
  margin-bottom: 18px;
  margin-top: 20px;
  text-align: center;
  color: #57f4ff;
}
</style>
