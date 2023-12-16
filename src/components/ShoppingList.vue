<script setup>
import { ref } from 'vue';
import Items from './Items.vue'

const lists = ref([]);

fetch("http://localhost:3000/lists/", {
    method: "GET",
    headers: { "Content-Type": "application/json" },
})
.then((res) => res.json())
.then((data) => (lists.value = data));

</script>

<template>

    <div v-for="list in lists" :key="list.id">
    {{ list.title }}
    <ul>
       <!--  <Items
        v-for="item in lists" 
        :key="item.id"
        :item="item.item-name"
        /> -->
        <li v-for="item in lists" :key="item.id">
            {{ item.items.item-name }}
            {{ console.log(item.item-name) }}
            
        </li>
    </ul>
    </div>

</template>