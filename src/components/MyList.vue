<script setup lang="ts">

// The interface to define the props of the MyList component
// an Interface is a way to define a type in TypeScript and it is used to define the props of the component
interface Props {
    title?: string;
    items: string[];
}

// Define the default values for the props of the MyList component
// The title prop is optional and has a default value of 'My List'
// The items prop is required and has no default value
// The defineProps function is used to define the props of the component
const { items } = withDefaults(defineProps<Props>(),{
    title: 'My List'
});
</script>

<template>
    <h2>{{ title }}</h2>
    <ul>
        <!-- Use the v-for directive to loop through the items list and display each item in a list item element -->
        <!-- The :key="idx" attribute is used to provide a unique key for each item in the list -->
        <li v-for="(item, idx) in items" :key="idx">{{ item }}</li>
    </ul>
</template>