<script setup lang="ts">
import { ref } from 'vue'
import { Item } from './../types.ts'

const text = ref('')

const emit = defineEmits<{
    (e: 'add', value: Item): void
    (e: 'remove', value: number): void
}>()

const submit = () => {
    emit('add', {
        value: text.value,
        done: false
    })
    text.value = ''
}
</script>

<template>
    <form @submit.prevent="submit">
        <label for="add-todo" class="sr-only">
            Füge eine neue Aufgabe hinzu
        </label>
        <div class="form-row">
            <input type="text" id="add-todo" required v-model="text" placeholder="Aufgabe hinzufügen">
            <button type="submit">Hinzufügen</button>
        </div>
    </form>
</template>