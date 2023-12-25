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

const getLists = () => {
  fetch('http://localhost:3000/lists/', {
    method: 'GET',
    headers: { 'Content-Type': 'application/json' }
  })
    .then((res) => res.json())
    .then((data) => (lists.value = data))
}
</script>

<template>
  <div>
    <NewList @listAdded="getLists" />
    <div v-for="list in lists" :key="list.id">
      <ListItems :list="list" />
      <NewItem :list="list" @itemAdded="getLists" />
    </div>
  </div>
</template>
