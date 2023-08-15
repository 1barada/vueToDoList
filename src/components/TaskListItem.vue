<script setup lang="ts">
import type Task from '@/models/Task';
import { ref } from 'vue';
import Button from '@/components/UI/Button.vue';
import TextInput from '@/components/UI/TextInput.vue';


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
}

</script>

<template>
  <div v-if="editing" class="list_item">
    <TextInput type="text" v-model="newText" class="input"/>
    <div class="list_item_ui">
      <Button @click="saveChanges">save</Button>
    </div>
  </div>
  <div v-else class="list_item"> 
    <div class="list_item__text" :class="{strikethrough: task.done}">
      {{ task.text }}
    </div>
    <div class="list_item_ui">
      <Button @click="editTask" :disabled="task.done">edit</Button>
      <Button @click="deleteTask" :disabled="task.done">delete</Button>
      <input type="checkbox" v-model="task.done"/>
    </div>
  </div>
</template>

<style scoped>
.list_item {
  flex: 0 1 80%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  padding: 10px 5px;
}
.list_item:not(:last-child) {
  border-bottom: 2px solid bisque;
} 
.list_item_ui {
  display: flex;
  gap: 5px;
}
.list_item__text {
  word-break: break-all;
}
.strikethrough {
  text-decoration: line-through;
}
.input {
  flex-grow: 1;
}
</style> 
