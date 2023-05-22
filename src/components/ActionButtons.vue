<script setup lang="ts">
  import { ref } from 'vue'

  const count = ref(0)

  function addOrSubstract(number) {
      count.value += (number)
  }

  function reset(){
      count.value = 0
  }

</script>

<template>
    <label>Le compteur affiche : {{ count }}</label>
    <div>
        <button class="m-1" type="button" @click="addOrSubstract(-5)">- 5</button>
        <button class="m-1" type="button" @click="addOrSubstract(-1)">- 1</button>
        <button class="m-1" type="button" @click="reset">0</button>
        <button class="m-1" type="button" @click="addOrSubstract(1)">1</button>
        <button class="m-1" type="button" @click="addOrSubstract(5)">5</button>
    </div>

</template>

<style scoped>

</style>