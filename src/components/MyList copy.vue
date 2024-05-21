<script setup lang="ts">
import { Item } from './../types.ts'
import TrashIcon from './../assets/trash.svg'

const items = defineModel<Item[]>()

const emit = defineEmits<{
    (e: 'remove', value: number): void
    (e: 'checked', value: Item): void
    (e: 'unchecked', value: Item): void
}>()

const removeItem = (index: number) => {
    emit('remove', index)
}

const checkedItem = (item: Item) => {
    emit('checked', item)
}

const uncheckedItem = (item: Item) => {
    emit('unchecked', item)
}


const onChange = (item: Item) => {
    if (item.done) {
        checkedItem(item)
    } else {
        uncheckedItem(item)
    }
}
</script>

<template>
    <ul role="list" v-if="items">
        <li v-for="(item, idx) in items" :key="idx">
            <div class="list-item">
                <div class="">
                    <input type="checkbox" :id="`item-${idx}`" v-model="item.done" @change="onChange(item)">
                    <label :for="`item-${idx}`">{{ item.value }}</label>
                </div>
                <button type="button" class="btn-icon" @click="removeItem(idx)">
                    <span class="sr-only">Lösche {{ item.value }}</span>
                    <img :src="TrashIcon" alt="" class="size-6" />
                </button>
            </div>
        </li>
    </ul>
</template>
