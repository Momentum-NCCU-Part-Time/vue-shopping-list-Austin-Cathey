<script setup>
import { ref } from 'vue'
import Delete from './Delete.vue'

const props = defineProps({ list: Object })
const editing = ref(false)

const togglePurchased = (item) => {
  item.purchased = !item.purchased
  purchasedItem(props.list)
  console.log(item.purchased)
}

const doEdit = (e) => {
  editing.value = e
}
const purchasedItem = () => {
  fetch('http://localhost:3000/shoppinglists/' + props.list._id + '/items/', {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: [...props.list.items]
    })
  })
    .then((res) => res.json())
    .then((r) => {})
}
</script>

<template>
  <div>
    <h3 class="listTitle">
      {{ props.list.title }}:
      <em>{{ props.list.items.length }} Items</em>
    </h3>
    <div>
      <button v-if="editing" @click="doEdit(false)" class="showButton">Hide List</button>
      <button v-else @click="doEdit(true)" class="showButton">Show List</button>
      <div v-if="editing">
        <ul>
          <li
            v-for="item in props.list.items"
            @click="togglePurchased(item)"
            :key="props.list.items._id"
            :class="{
              strikeout: item.purchased
            }"
          >
            {{ item.quantity }}
            {{ item.name }}
            <input v-model="item.purchased" type="checkbox" />
          </li>
        </ul>
      </div>
    </div>
  </div>
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
