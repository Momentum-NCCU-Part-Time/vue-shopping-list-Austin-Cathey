<script setup>
import { ref } from 'vue'
const newItem = ref('')
const props = defineProps({ itemProp: Object, list: Object })
const existingItems = ref(props.list[items])
console.log(existingItems.value)
const addNewItem = () => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: props.list.items.push({
        id: props.itemProp.id,
        itemName: newItem.value,
        purchased: 'false'
      }),
      updatedAt: new Date()
    })
  })
    .then((res) => res.json())
    .then((item) => {
      console.log()
      /* emit("itemAdded", item) */
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
