<script setup lang="ts">
// Import the ref function from Vue
import { ref } from 'vue'

// Import the MyList component
import MyList from './components/MyList.vue'
import MyInput from './components/MyInput.vue'
import { Item } from './types';

const items = ref<Item[]>([]);

const addItem = (item: Item) => {
    items.value.push(item);
}

</script>

<template>
  <div>
    <div>
      <my-list :items="items" title="Fist List" />
      <my-input @add="addItem" />
    </div>

  </div>
</template>
