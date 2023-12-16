<script setup>
import { ref } from 'vue';

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
        <li v-for="item in lists" :key="item.id">
            {{ list.items.item-name }}
            
        </li>
    </ul>
    </div>

</template>