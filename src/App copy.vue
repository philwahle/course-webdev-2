<script setup lang="ts">
// Import the ref function from Vue
import { ref } from 'vue'

// Import the MyList component
import MyList from './components/MyList.vue'
import MyInput from './components/MyInput.vue'
import { Item } from './types.ts'

const items = ref<Item[]>([
  { value: 'Einkaufen', done: false },
  { value: 'Wäsche waschen', done: true },
  { value: 'Rechnungen bezahlen', done: false },
]);
const liveRegion = ref<HTMLElement | null>(null);
const heading = ref<HTMLHeadingElement | null>(null);

const addItem = (item: Item) => {
  items.value.push(item);

  if (!liveRegion.value) return;
  liveRegion.value.textContent = `Du hast ${item.value} hinzugefügt.`;
}

const removeItem = (index: number) => {
  console.log('removeItem', index);
  const item = items.value[index];
  items.value.splice(index, 1);

  if (!liveRegion.value) return;
  liveRegion.value.textContent = `Du hast ${item.value} entfernt.`;

  if (!heading.value) return;
  heading.value.focus();
}

const checkedItem = (item: Item) => {
  if (!liveRegion.value) return;
  liveRegion.value.textContent = `Du hast ${item.value} abgehakt.`;
}

const uncheckedItem = (item: Item) => {
  if (!liveRegion.value) return;
  liveRegion.value.textContent = `Du hast ${item.value} wieder aufgenommen.`;
}

</script>

<template>
  <section aria-labelledby="todo-heading">
    <h1 id="todo-heading" tabindex="-1" ref="heading">
      Meine Augaben Liste
    </h1>

    <!-- Live-Region für inhaltsabhängige Nachrichten -->
    <!-- class="sr-only" -->
    <div role="status" aria-live="polite" aria-atomic="true" class="status status-success">

      <img src="./assets/check.svg" alt="" class="size-6" />

      <div ref="liveRegion" />
      <!-- inhaltsabhängige Nachrichten werden hier angezeigt und vorgelesen -->
    </div>

    <div class="empty-state" v-if="!items.length">
      <p>
        Du hast keine Einträge in deiner To-Do-Liste. Füge jetzt einen hinzu!
      </p>
    </div>

    <my-list v-model="items" @remove="removeItem" @checked="checkedItem" @unchecked="uncheckedItem" />
    <my-input @add="addItem" />

  </section>
</template>
