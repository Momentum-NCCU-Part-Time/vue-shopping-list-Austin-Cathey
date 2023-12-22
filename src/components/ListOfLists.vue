<script setup>
import { ref } from 'vue'
import ListItems from './ListItems.vue'
import Items from './Items.vue'
import NewList from './NewList.vue'
import NewItem from './NewItem.vue'

const lists = ref([])
const purchased = ref(false)
const newItem = ref('')

fetch('http://localhost:3000/lists/', {
  method: 'GET',
  headers: { 'Content-Type': 'application/json' }
})
  .then((res) => res.json())
  .then((data) => (lists.value = data))

const addNewItem = (list) => {
  fetch('http://localhost:3000/lists/' + list.id, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: list.title,
      items: [
        ...list.items,
        {
          id: list.items.length + 1,
          itemName: newItem.value,
          purchased: false
        }
      ],
      updatedAt: new Date()
    })
  })
    .then((res) => res.json())
    .then((r) => {
      /* resetItem() */
    })
}
</script>

<template>
  <div>
    <NewList />
    <div v-for="list in lists" :key="list.id">
      <ListItems :list="list" />
      <form class="itemForm" @submit.prevent="addNewItem(list)">
        <input v-model="newItem" type="text" placeholder="Add Item" />
        <button type="submit">Add</button>
      </form>
    </div>
  </div>
</template>
