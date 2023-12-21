<script setup>
import { ref } from 'vue'

const props = defineProps({ list: Object })
</script>

<template>
  <h3>{{ props.list.title }}</h3>
</template>
