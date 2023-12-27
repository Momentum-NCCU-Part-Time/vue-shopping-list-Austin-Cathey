<script setup>
import { ref } from 'vue'

/* const purchased = ref(false) */
const props = defineProps({ list: Object })

const togglePurchased = (items) => {
  items.purchased = !items.purchased
}
</script>

<template>
  <h3>{{ props.list.title }}</h3>
  <ul>
    <li
      v-for="items in props.list.items"
      @click="togglePurchased(items)"
      :key="list.items.id"
      :class="{ strikeout: items.purchased }"
    >
      {{ items.itemName }}
      <!--       <input v-model="purchased" type="checkbox" /> -->
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
