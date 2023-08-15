<script setup lang="ts">
import type Task from '@/models/Task';
import { ref } from 'vue';


const props = defineProps<{
  task: Task,
  editing: boolean
}>();

const newText = ref<string>(props.task.text);

const emit = defineEmits<{
  deleteTask: [id: number],
  editTask: [id: number],
  saveChanges: [id: number, newText: string]
}>();

function deleteTask() {
  emit('deleteTask', props.task.id);
}

function editTask() {
  emit('editTask', props.task.id);
}

function saveChanges() {
  newText.value = newText.value.trim();
  if (newText) {
    emit('saveChanges', props.task.id, newText.value);
  } else {
    emit('saveChanges', props.task.id, props.task.text);
  }

  newText.value = '';
}

</script>

<template>
  <div v-if="editing">
    <input type="text" v-model="newText" defa/>
    <button @click="saveChanges">save</button>
  </div>
  <div v-else>
    <p>{{ task.text }}</p>
    <button @click="editTask">edit</button>
    <button @click="deleteTask">delete</button>
    <input type="checkbox" v-model="task.done"/>
  </div>
</template>

<style scoped>

</style> 
