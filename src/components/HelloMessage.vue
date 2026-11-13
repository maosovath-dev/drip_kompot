<script setup>
defineProps({
  text: {
    type: String,
    default: 'Hello'
  }
})
</script>

<template>
  <h1 class="title">{{ text }}</h1>
</template>

<style scoped>
.title {
  font-size: 3rem;
  color: #032ea1;
}
</style>
