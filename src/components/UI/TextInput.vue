<script setup lang="ts">
const props = defineProps<{
    modelValue: string
}>();

const emit = defineEmits(['update:modelValue'])

const updateValue = (event) => {
    emit('update:modelValue', event.target.value)
}
</script>

<template>
    <input type="text" :value="modelValue" @input="updateValue"/>
</template>

<style scoped>
input {
    border: 2px solid bisque;
    border-radius: 8px;
    padding: 4px 10px;
}
input:focus-visible {
    border: 2px solid rgb(233, 203, 166);
}
</style> 
