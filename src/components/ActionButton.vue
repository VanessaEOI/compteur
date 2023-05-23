<script setup lang="ts">
 defineProps<{
      value: number,
  }>()
</script>

<template>
    <button @click="$emit('add', value)" >{{ value }}</button>
</template>

<style scoped>

</style>