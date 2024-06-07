<script setup lang="ts">

import { Item } from '../types';

// The interface to define the props of the MyList component
// an Interface is a way to define a type in TypeScript and it is used to define the props of the component
interface Props {
    title?: string;
    items: Item[];
}

// Define the default values for the props of the MyList component
// The title prop is optional and has a default value of 'My List'
// The items prop is required and has no default value
// The defineProps function is used to define the props of the component
withDefaults(defineProps<Props>(), {
    title: 'My List'
});

const emit = defineEmits<{
    (e: 'remove', value: number): void
}>()

const removeItem = (index: number) => {
    emit('remove', index)
}

</script>

<template>
    <ul>
        <!-- {{  items }} -->
        <li v-for="(item, idx) in items" :key="idx">
            <input type="checkbox" v-model="item.done" :id="item.name">
            <label :for="item.name" :class="{
                done: item.done
            }">{{ item.name }}
            </label>
            <button type="button" id="button" 
            :aria-label="'Lösche ' + item.name"
            @click="removeItem(idx)">
                Lösche
            </button>
        </li>
    </ul>
</template>



<style scoped>
.done {
    text-decoration: line-through;
    font-style: italic;
}
</style>