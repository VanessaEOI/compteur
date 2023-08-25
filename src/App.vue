<script setup lang="ts">

import ActionButton from "./components/ActionButton.vue";

import { ref } from 'vue'

const count = ref(0)
function addOrSubstract(valueButton) {
    count.value += valueButton
}

const dataButtons = ref([
  { id: 1, label: '-1', value: -1 },
  { id: 2, label: '-5', value: -5 },
  { id: 3, label: '+ 1', value: 1 },
  { id: 4, label: '+ 5', value: 5 },
])

</script>

<template>

    <h1>Compteur</h1>

    <label>Le compteur affiche : {{ count }}</label>

    <div>
        <ActionButton v-for="databutton in dataButtons" :key="databutton.id" :valueButton="databutton.value" @add="addOrSubstract" />
    </div>

</template>

<style scoped>

</style>
