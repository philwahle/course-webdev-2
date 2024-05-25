<script setup lang="ts">
import { ref } from 'vue'
const text = ref('')

const emit = defineEmits(['add'])

const add = () => {
    emit('add', {
        name: text.value,
        done: false
    })
    text.value = ''
}
</script>

<template>
    <form @submit.prevent="add">
        <label for="todo">Aufgabe</label>
        <input type="text" required v-model="text" id="todo">
        <button type="submit">Add</button>
    </form>
</template>
<style scoped>

form {
    display: flex;
    gap: 1rem;
}

input:focus {
    outline: none;
    box-shadow: 0 0 0 2px white,
                 0 0 0 4px #2a4365;
}
</style>