<script setup lang="ts">
import { ref } from 'vue'
const text = ref('')

const emit = defineEmits(['add'])

const add = () => {
    emit('add', text.value)
    text.value = ''
}
</script>

<template>
    <div>
        <input type="text" required v-model="text">
        <button type="button" @click="add">Add</button>
    </div>
</template>