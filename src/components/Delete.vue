<script setup>
import { ref } from 'vue'

const deleting = ref(false)
const props = defineProps({ list: Object })
const emit = defineEmits(['listDeleted'])

const deleteList = (list) => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'DELETE'
  })
    .then((res) => res.json())
    .then((deletedList) => {
      emit('listDeleted', deletedList)
    })
}

function confirmDelete(e) {
  deleting.value = e
}
</script>

<template>
  <form>
    <button v-if="deleting" @click="confirmDelete(false)" class="deleteButton">Keep List</button>
    <button v-else @click="confirmDelete(true)" class="deleteButton">Delete List</button>
    <form v-if="deleting" @click.prevent="deleteList(list)">
      <button type="submit" class="deleteButton">No really, delete list</button>
    </form>
  </form>
</template>
