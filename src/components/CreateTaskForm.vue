<script setup lang="ts">
import type Task from '@/models/Task';
import { ref } from 'vue';

const emit = defineEmits<{
  createTask: [task: Task]
}>();

const text = ref<string>('');

function createTask() {
  if (!text.value.trim()) return;
  
  emit('createTask', {
    id: Date.now(),
    text: text.value,
    done: false
  });

  text.value = '';
}
</script>

<template>
  <div>
    <p>Create task</p>
    <input type="text" v-model="text">
    <button @click="createTask">add</button>
  </div>
</template>

<style scoped>

</style> 
