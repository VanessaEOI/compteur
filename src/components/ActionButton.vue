<script setup lang="ts">
 defineProps<{
      valueButton: Number,
  }>()
</script>

<template>
    <button @click="$emit('add', valueButton)" >{{ valueButton }}</button>
</template>

<style scoped>

</style>