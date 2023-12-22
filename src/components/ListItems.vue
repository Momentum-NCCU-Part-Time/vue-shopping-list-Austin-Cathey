<script setup>
import { ref } from 'vue'

const props = defineProps({ list: Object })
</script>

<template>
  <h3>{{ props.list.title }}</h3>
  <ul>
    <li v-for="items in props.list.items" key="list.items.id">
      {{ items.itemName }}
    </li>
  </ul>
</template>
