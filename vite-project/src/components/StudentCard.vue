<template>
  <div class="mx-auto w-1/2 mt-10 flex flex-col items-center">
    <div class="p-5 w-64 cursor-pointer border border-gray-600 mb-5">
      <p>Name: {{ student.name }}</p>
      <p>Surname: {{ student.surname }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { studentInfo } from '@/student'
import type{ PropType} from 'vue'
const props = defineProps({
  student: {
    type: Object as PropType<studentInfo>,
    required: true
  }
})
</script>

<style scoped></style>
