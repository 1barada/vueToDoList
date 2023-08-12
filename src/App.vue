<script setup lang="ts">
import { onMounted, ref, watch } from 'vue';
import TaskList from './components/TaskList.vue';
import type Task from './models/Task';
import CreateTaskForm from './components/CreateTaskForm.vue';

const tasks = ref<Task[]>([]);

onMounted(() => {
  const storageData = localStorage.getItem('tasks');
  if (storageData) {
    tasks.value = JSON.parse(storageData); 
  }
});

watch(tasks, () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value));
}, {deep: true});

function createTask(newTask: Task) {
  tasks.value.push(newTask);
}

function deleteTask(id: number) {
  tasks.value = tasks.value.filter(task => task.id !== id);
}
</script>

<template>
  <div>
    <CreateTaskForm @createTask="createTask"/> 
    <TaskList :tasks="tasks" @deleteTask="deleteTask"/>
  </div>
</template>

<style scoped>

</style> 
