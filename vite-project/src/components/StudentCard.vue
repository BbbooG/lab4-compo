<template>
  <div class="students">
    <span>Name: {{ student.name }}</span>
    <p>Surname: {{ student.surname }}</p>
    <p>GPA: {{ student.gpa }}</p>
  </div>
</template>

<script setup lang="ts">
import type { studentInfo } from '@/student'
import { PropTypes } from 'vue'
const props = defineProps({
  student: {
    type: Object as PropTypes<studentInfo>,
    required: true
  }
})
</script>

<style scoped>
.students {
  padding: 20px;
  width: 250px;
  cursor: pointer;
  border: 1px solid #b3cff1;
  margin-bottom: 18px;margin-top: 20px;
  margin-left: 30%;
  color: #57f4ff;
}
</style>
