<script setup>
import { ref } from 'vue';
import Items from './Items.vue'
import NewList from './NewList.vue';
import NewItem from './NewItem.vue';

const lists = ref([]);
const purchased = ref(false);

fetch("http://localhost:3000/lists/", {
    method: "GET",
    headers: { "Content-Type": "application/json" },
})
.then((res) => res.json())
.then((data) => (lists.value = data));

</script>

<template>
<NewList />
    <div v-for="list in lists" :key="list.id">
    {{ list.title }}
    <br/>
    
    <li v-for="item in list.items" :key="item.id">
            {{ item.itemName}}
           <input v-model="purchased" type="checkbox">
        </li>
        <NewItem 
    :list="lists" />
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