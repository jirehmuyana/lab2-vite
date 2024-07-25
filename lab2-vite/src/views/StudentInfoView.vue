<script setup lang="ts">
import StudentInfoCard from '@/components/StudentInfoCard.vue'
import StudentInfoService from '@/services/StudentInfoService'
import type { Student } from '@/type'
import { ref, onMounted } from 'vue'

const students = ref<Student[]>([])

onMounted(() => {
  StudentInfoService.getStudents()
    .then((response) => {
      console.log('hi', response.data)
      students.value = response.data
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
})
</script>

<template>
  <h1>Student Information</h1>
  <!-- new element -->

  <div class="students">
    <StudentInfoCard v-for="student in students" :key="student.id" :student="student" />
  </div>
</template>

<style scoped>
.students {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
