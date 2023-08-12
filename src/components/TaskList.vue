<script setup lang="ts">
import type Task from '@/models/Task';
import TaskListItem from './TaskListItem.vue';

const emit = defineEmits<{
  deleteTask: [id: number]
}>();

defineProps<{
  tasks: Task[]
}>();

function deleteTask(id: number) {
  emit('deleteTask', id);
}
</script>

<template>
  <div v-for="task in tasks" :key="task.id">
    <TaskListItem :task="task" @deleteTask="deleteTask"/>
  </div>
</template>

<style scoped>

</style> 
