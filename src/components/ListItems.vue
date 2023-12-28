<script setup>
import { ref } from 'vue'

const props = defineProps({ list: Object })
const emit = defineEmits(['itemPurchased'])
const editing = ref(false)

const togglePurchased = (items) => {
  items.purchased = !items.purchased
}

const doEdit = (e) => {
  editing.value = e
}
/* const purchasedItem = (list) => {
  fetch('http://localhost:3000/lists/' + props.list.items.id, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: [
        ...props.list.items,
        {
          purchased = !purchased
        }
      ]
    })
  })
    .then((res) => res.json())
    .then((purchasedItem) => {
      emit('itemPurchased', purchasedItem)
      resetItem()
    })
} */
</script>

<template>
  <h3>{{ props.list.title }}</h3>
  <p>Total Items: {{ props.list.items.length }}</p>
  <button v-if="editing" @click="doEdit(false)">Cancel</button>
  <button v-else @click="doEdit(true)">Edit List</button>
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
