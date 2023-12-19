<script setup>
import { ref } from 'vue'
const newItem = ref("");
const props =
defineProps
({list: Object});

const addNewItem = () => {
  fetch("http://localhost:3000/lists/" + props.id, {
    method: "PATCH",
    headers: {"Content-Type": "application/json"},
    body:JSON.stringify({ itemName: newItem.value, purchased: "false" }),
  })
  .then((res) => res.json())
  .then((item) => {
    /* emit("itemAdded", item) */
    resetItem()
  });
};

const resetItem = () => {
    newItem.value=""
};
</script>

<template>
    <form class="itemForm" @submit.prevent="addNewItem">
 <input v-model="newItem" type="text" placeholder="Add Item" />
<button type="submit">Add</button>
</form>
</template>