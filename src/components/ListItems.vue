<script setup>
import { ref } from 'vue'

const props = defineProps({ list: Object })
const editing = ref(false)

const togglePurchased = (items) => {
  items.purchased = !items.purchased
  purchasedItem(props.list)
}

const doEdit = (e) => {
  editing.value = e
}
const purchasedItem = (list) => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: [...props.list.items],
      updatedAt: new Date()
    })
  })
    .then((res) => res.json())
    .then((r) => {})
}
</script>

<template>
  <h3>{{ props.list.title }}: {{ props.list.items.length }} Items</h3>
  <!--  <p>Total Items: {{ props.list.items.length }}</p> -->
  <button v-if="editing" @click="doEdit(false)">Hide List</button>
  <button v-else @click="doEdit(true)">Show List</button>
  <ul v-if="editing">
    <li
      v-for="items in props.list.items"
      @click="togglePurchased(items)"
      :key="list.items.id"
      :class="{ strikeout: items.purchased }"
    >
      {{ items.itemName }}
      <input v-model="items.purchased" type="checkbox" />
    </li>
  </ul>
</template>

<style>
.strikeout {
  text-decoration: line-through;
  color: #b8c2cc;
}

.strikeout:hover {
  color: #8795a1;
}
</style>
