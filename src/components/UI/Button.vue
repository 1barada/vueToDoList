<script setup lang="ts">
defineProps<{
    disabled: {
        type: boolean,
        default: false,
        required: false
    }
}>();
</script>

<template>
    <button class="btn" :disabled="disabled">
        <slot/>
    </button>
</template>

<style scoped>
.btn {
    border: 2px solid bisque;
    padding: 5px 30px;
    text-transform: uppercase;
    font-size: 12px;
    border-radius: 8px;
}
.btn:hover {
    background-color: bisque;
}
.btn:active {
    border: 2px solid rgb(223, 196, 164);
    background-color: rgb(223, 196, 164);
}
.btn:disabled {
    border-color: rgb(190, 190, 190);
}
.btn:disabled {
    background-color: rgb(236, 236, 236);
}
</style> 
