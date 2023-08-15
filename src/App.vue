<script setup lang="ts">
import { onMounted, ref, watch } from 'vue';
import TaskList from './components/TaskList.vue';
import type Task from './models/Task';
import CreateTaskForm from './components/CreateTaskForm.vue';

const tasks = ref<Task[]>([]);
const editing = ref<number>(); // the id of the task that currently editing

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

function editTask(id: number) {
  editing.value = id;
}

function saveChanges(id: number, newText: string) {
  const task = tasks.value.find(task => task.id === id);
  if (!task) {
    throw new Error('App.vue/saveChanges: no such task');
  }
  task.text = newText;
  editing.value = undefined;
}
</script>

<template>
  <div>
    <CreateTaskForm @createTask="createTask"/> 
    <TaskList 
      :tasks="tasks" 
      :editing="editing" 
      @deleteTask="deleteTask"
      @editTask="editTask"
      @saveChanges="saveChanges"
    />
  </div>
</template>

<style scoped>

</style> 
