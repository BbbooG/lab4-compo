<script setup lang="ts">
import type { EventItem } from '@/type'
import type { PropType } from 'vue'
import { useRouter } from 'vue-router'
import { useMessageStore } from '@/stores/message'
const props = defineProps({
  event: {
    type: Object as PropType<EventItem>,
    require: true
  }
})
const router = useRouter()
const store = useMessageStore()
function edit() {
  store.updateMessage('Your editing is success: ' + props.event?.title)
  setTimeout(() => {
    store.resetMessage()
  }, 3000)
  router.push({
    name: 'event-detail',
    params: {
      id: props.event?.id
    }
  })
}
</script>


<template>
  <div class="mx-auto w-1/2 mt-10 flex flex-col items-center">
    <div class="p-5 border border-gray-600">
      <p>Edit the event here</p>
    </div>

    <button class="bg-yellow-500 text-white font-bold py-2 px-4 rounded mt-5" @click="edit">
      detail botton
    </button>
  </div>
</template>