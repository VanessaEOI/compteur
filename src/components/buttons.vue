<script setup lang="ts">
  import { ref } from 'vue'

  const count = ref(0)

  function minusFive() {
      count.value = - 5
  }

  function minusOne() {
      count.value = - 1
  }

  function reset() {
      count.value = 0
  }

  function plusOne() {
      count.value = + 1
  }

  function plusFive() {
      count.value = + 5
  }

</script>

<template>
    <label>Le compteur affiche : {{ count }}</label>
    <div>
        <button type="button" @click="minusFive()">- 5</button>
        <button type="button" @click="minusOne">- 1</button>
        <button type="button" @click="reset">0</button>
        <button type="button" @click="plusOne">1</button>
        <button type="button" @click="plusFive">5</button>
    </div>

</template>

<style scoped>

</style>