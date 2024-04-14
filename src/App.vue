<script setup lang="ts">
// Import the ref function from Vue
import { ref } from 'vue'

// Import the MyList component
import MyList from './components/MyList.vue'

// Define the reactive variables of a list of items
const items = ref(['a', 'b', 'c']);
const items2 = ref(['d', 'e', 'f']);

// Define the reactive variable of the input text
const text = ref('');

// Define the function to add a new item to the list
const add = () => {

  // Add the value of the text variable to the items list
  items.value.push(text.value);

  // Clear the value of the text variable
  text.value = '';
}
</script>

<template>
  <div>
    <!-- Use the MyList component with the items and items2 lists -->
    <!-- v-bind:items and :items are equivalent syntax for passing props to a component. :items is a shorthand syntax for v-bind:items -->
    <my-list :items="items" />
    <my-list v-bind:items="items2" title="List 2" />

    <!-- Use the input text and button to add a new item to the list -->
    <!-- Use the v-model directive to bind the text variable to the input element -->
    <input type="text" v-model="text">

    <!-- {{ text }} is used to display the value of the text variable -->
    <p>{{ text }} </p>

    <!-- Use the @click directive to call the add function when the button is clicked -->
    <button type="button" @click="add">Add</button>
  </div>
</template>
