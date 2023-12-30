<script setup>
import { ref } from 'vue'
const newItem = ref('')

const props = defineProps({ list: Object })
const emit = defineEmits(['itemAdded'])

const addNewItem = (list) => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: [
        ...props.list.items,
        {
          id: props.list.items.length + 1,
          itemName: newItem.value,
          purchased: false
        }
      ],
      updatedAt: new Date()
    })
  })
    .then((res) => res.json())
    .then((addedItem) => {
      emit('itemAdded', addedItem)
      resetItem()
    })
}

const resetItem = () => {
  newItem.value = ''
}
</script>

<template>
  <form class="itemForm" @submit.prevent="addNewItem">
    <input v-model="newItem" type="text" placeholder="Add Item" />
    <button type="submit">Add</button>
  </form>
</template>
