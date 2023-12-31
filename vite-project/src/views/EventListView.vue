<script setup lang="ts">
import EventCard from '../components/EventCard.vue'
import EventOrganizer from '../components/EventOrganizer.vue'
import type { EventItem } from '@/type'
import { computed, ref, watchEffect } from 'vue'
import type { Ref } from 'vue'
import EventService from '@/services/EventService'
import type { Axios, AxiosResponse } from 'axios'
import { useRouter } from 'vue-router'
import { onBeforeRouteUpdate } from 'vue-router'

const router = useRouter()
const events: Ref<Array<EventItem>> = ref([])
const totalEvent = ref<number>(0)
const eventsPerPage = ref(2) //initial value of events
const props = defineProps({
  page: {
    type: Number,
    required: true
  }
})
watchEffect(() => {
  EventService.getEvent(eventsPerPage.value, props.page).then(
    (response: AxiosResponse<EventItem[]>) => {
      events.value = response.data
    }
  )
  EventService.getEvent(eventsPerPage.value, props.page)
    .then((response: AxiosResponse<EventItem[]>) => {
      events.value = response.data
      totalEvent.value = response.headers['x-total-count']
    })
    .catch(() => {
      router.push({ name: 'NetworkError' })
    })
})
onBeforeRouteUpdate((to, from, next) => {
  const toPage = Number(to.query.page)
  EventService.getEvent(eventsPerPage.value, toPage)
    .then((response: AxiosResponse<EventItem[]>) => {
      events.value = response.data
      totalEvent.value = response.headers['x-total-count']
      next()
    })
    .catch(() => {
      next({ name: 'NetworkError' })
    })
})

const hasNextPages = computed(() => {
  //first calculate total page
  const totalPages = Math.ceil(totalEvent.value / eventsPerPage.value)
  return props.page.valueOf() < totalPages
})
</script>

<template>
  <main class="flex flex-col items-center">
    <div class="events-input">
      <label for="events-per-page">Events per page:</label>
      <input
        type="number"
        id="events-per-page"
        v-model.number="eventsPerPage"
        class="border border-gray-300 p-2 rounded m-3"
      />
    </div>
    <EventCard v-for="event in events" :key="event.id" :event="event"></EventCard>
    <div class="pagination">
      <RouterLink
        :to="{ name: 'event-list', query: { page: page - 1 } }"
        rel="prev"
        v-if="page != 1"
        id="page-prev"
        class="px-4 py-2 bg-yellow-500 text-white rounded hover:bg-yellow-600 m-5"
      >
        Prev page
      </RouterLink>
      <RouterLink
        :to="{ name: 'event-list', query: { page: page + 1 } }"
        rel="next"
        v-if="hasNextPages"
        id="page-next"
        class="px-4 py-2 bg-yellow-500 text-white rounded hover:bg-yellow-600 m-5"
      >
        Next page
      </RouterLink>
    </div>
    
  </main>
</template>
