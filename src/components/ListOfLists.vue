<script setup>
import { ref } from 'vue'
import Lists from './Lists.vue'
import Items from './Items.vue'
import NewList from './NewList.vue'
import NewItem from './NewItem.vue'

const lists = ref([])
const purchased = ref(false)

fetch('http://localhost:3000/lists/', {
  method: 'GET',
  headers: { 'Content-Type': 'application/json' }
})
  .then((res) => res.json())
  .then((data) => (lists.value = data))
</script>

<template>
  <div>
    <NewList />
    <div v-for="list in lists" :key="list.id">
      <Lists :list="list" />
      <ul>
        <li v-for="items in list.items" key="list.items.id">
          {{ items.itemName }}
        </li>
      </ul>
      <!-- <Items :key="list.items.id" :item="list.items" /> -->
      <!-- <NewItem :itemProp="item" :list="list" /> -->
    </div>
  </div>
</template>
