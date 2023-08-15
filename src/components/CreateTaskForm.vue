<script setup lang="ts">
import type Task from '@/models/Task';
import { ref } from 'vue';
import Button from '@/components/UI/Button.vue';
import TextInput from '@/components/UI/TextInput.vue';

const emit = defineEmits<{
  createTask: [task: Task]
}>();

const text = ref<string>('');

function createTask() {
  if (!text.value.trim()) {
    text.value = '';  
    return;
  }
  
  emit('createTask', {
    id: Date.now(),
    text: text.value,
    done: false
  });

  text.value = '';
}
</script>

<template>
  <div class="form">
    <h3>Create task</h3>
    <TextInput v-model="text"/>
    <Button @click="createTask">add</Button>
  </div>
</template>

<style scoped>
.form {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
}
</style> 
