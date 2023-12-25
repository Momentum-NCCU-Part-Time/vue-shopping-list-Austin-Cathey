<script setup>
import { ref } from 'vue'
const newList = ref('')

const emit = defineEmits(['listAdded'])

const addNewList = () => {
  fetch('http://localhost:3000/lists/', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ title: newList.value, items: [], updatedAt: new Date() })
  })
    .then((res) => res.json())
    .then((newList) => {
      emit('listAdded', newList)
      resetList()
    })
}

const resetList = () => {
  newList.value = ''
}
</script>

<template>
  <form class="newList" @submit.prevent="addNewList">
    <input v-model="newList" type="text" placeholder="New List Title" />
    <button type="submit">Add</button>
  </form>
</template>
