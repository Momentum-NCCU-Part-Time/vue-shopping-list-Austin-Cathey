<script setup>
import { ref } from 'vue'
const newItem = ref('')
const newItemQnty = ref('')
const addingItem = ref(false)

const props = defineProps({ list: Object })
const emit = defineEmits(['itemAdded'])

const addNewItem = () => {
  fetch('http://localhost:3000/shoppinglists/' + props.list._id + '/items', {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: [
        ...props.list.items,
        {
          name: newItem.value,
          quantity: newItemQnty.value,
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

const addItem = (e) => {
  addingItem.value = e
}

const resetItem = () => {
  newItem.value = ''
  newItemQnty.value = ''
}
</script>

<template>
  <div>
    <form v-if="addingItem" class="itemForm" @submit.prevent="addNewItem">
      <input v-model="newItem" class="newForm" type="text" placeholder="Add Item" />
      <br />
      <input v-model="newItemQnty" class="newForm" type="number" placeholder="Amount of" />
      <button class="newItemBtn" type="submit">Add</button>
    </form>
    <button v-if="addingItem" @click="addItem(false)" class="newItemBtn">Cancel Item</button>
    <button v-else @click="addItem(true)" class="newItemBtn">Add Item</button>
  </div>
</template>
