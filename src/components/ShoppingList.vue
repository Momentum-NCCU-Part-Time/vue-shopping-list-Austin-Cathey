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
    <li v-for="item in list.items" :key="item.id">
            {{ item.id }}
            {{ console.log(item) }}
        </li>
    </div>
    <ul>
        <!-- <Items
        v-for="item in lists" 
        :key="item.id"
        :item=""
        />
        {{ console.log(item) }} -->
        
    </ul>
    

</template>