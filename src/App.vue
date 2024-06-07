<script setup lang="ts">
// Import the ref function from Vue
import { ref } from 'vue'

// Import the MyList component
import MyList from './components/MyList.vue'
import MyInput from './components/MyInput.vue'
import { Item } from './types';

const items = ref<Item[]>([
  { name: 'Einkaufen', done: false },
  { name: 'Aufräumen', done: true },
  { name: 'Lernen', done: false }
]);



const addItem = (item: Item) => {
  items.value.push(item);
}

const heading = ref<HTMLHeadingElement | null>(null);
const removeItem = (index: number) => {
  items.value.splice(index, 1);

  if(!heading.value) return;
  heading.value.focus()

  // document.getElementById('heading')?.focus();
}
</script>

<template>
  <div>
    <h1 ref="heading" id="heading" tabindex="-1">Meine Aufgabenliste</h1>

    <div>
      <my-list :items="items" @remove="removeItem" />
      <my-input @add="addItem" />
    </div>
  </div>
</template>
