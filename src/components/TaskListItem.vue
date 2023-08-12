<script setup lang="ts">
import type Task from '@/models/Task';

const props = defineProps<{
  task: Task
}>();

const emit = defineEmits<{
  deleteTask: [id: number]
}>();

function deleteTask() {
  emit('deleteTask', props.task.id);
}

</script>

<template>
  <div>
    <p>{{ task.text }}</p>
    <button @click="deleteTask">delete</button>
    <input type="checkbox" v-model="task.done"/>
  </div>
</template>

<style scoped>

</style> 
