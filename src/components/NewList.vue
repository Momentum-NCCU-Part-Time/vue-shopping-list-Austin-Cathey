<script setup>
import { ref } from 'vue'
import NewListItems from './NewListItems.vue'
const newList = ref('')

const addingList = ref(false)
const emit = defineEmits(['listAdded'])

const addNewList = () => {
  fetch('http://localhost:3000/shoppinglists/', {
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

const addList = (e) => {
  addingList.value = e
}

const resetList = () => {
  newList.value = ''
}
</script>

<template>
  <div>
    <button v-if="addingList" @click="addList(false)" class="newListBtn">Nevermind</button>
    <button v-else @click="addList(true)" class="newListsBtn">New List</button>
    <form v-if="addingList" class="newList" @submit.prevent="addNewList">
      <input v-model="newList" type="text" class="newForm" placeholder="New List Title" />
      <!-- <div>
      <NewListItems />
      <NewListItems />
      <NewListItems />
      <NewListItems />
      <NewListItems />
    </div> -->
      <button class="newListBtn" type="submit">Add</button>
    </form>
  </div>
</template>
