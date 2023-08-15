<script setup lang="ts">
import type Task from '@/models/Task';
import TaskListItem from './TaskListItem.vue';

const emit = defineEmits<{
  deleteTask: [id: number],
  editTask: [id: number],
  saveChanges: [id: number, newText: string]
}>();

defineProps<{
  tasks: Task[],
  editing: number | undefined
}>();

function deleteTask(id: number) {
  emit('deleteTask', id);
}

function editTask(id: number) {
  emit('editTask', id);
}

function saveChanges(id: number, newText: string) {
  emit('saveChanges', id, newText);
}
</script>

<template>
  <div class="list">
    <TaskListItem 
      v-for="task in tasks" :key="task.id"
      :task="task" 
      :editing="editing ? editing === task.id : false" 
      @deleteTask="deleteTask"
      @editTask="editTask"
      @saveChanges="saveChanges"
    />
  </div>
</template>

<style scoped>
.list {
  flex: 0 1 100%;
  display: flex;
  flex-direction: column;
}
</style> 
