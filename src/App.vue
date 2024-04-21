<script setup lang="ts">
// Import the ref function from Vue
import { ref } from 'vue'

// Import the MyList component
import MyList from './components/MyList.vue'
import MyInput from './components/MyInput.vue'

// Define the reactive variables of a list of items
const items = ref(['a', 'b', 'c']);
const items2 = ref(['d', 'e', 'f']);

const addItem = (item: string, list: 'list1' | 'list2') => {
  if (list === 'list1')
    items.value.push(item);
  else if (list === 'list2')
    items2.value.push(item);
}

const addItem2 = (item: string) => {
  items2.value.push(item);
}

</script>

<template>
  <div>
    <div>
      <!-- call a different function that adds to a different list -->
      <my-list :items="items2" title="Fist List" />
      <my-input @add="addItem2" />
    </div>

    <div>
      <!-- an alternative is pass the name of the list to the event -->
      <my-list :items="items" title="Second List" />
      <my-input @add="(e: string) => addItem(e, 'list1')" />
    </div>
  </div>
</template>
