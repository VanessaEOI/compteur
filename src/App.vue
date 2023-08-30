<script setup lang="ts">

import ActionButton from "./components/ActionButton.vue";
import {ref} from 'vue'
import {useRefHistory, useStorage} from "@vueuse/core";

const count = ref(0)
const {history, undo, redo, canUndo, canRedo} = useRefHistory(count, {capacity: 10})

useStorage('count', count)

const dataButtons = ref([
  {id: 1, label: '-1', value: -1},
  {id: 2, label: '-5', value: -5},
  {id: 3, label: '+ 1', value: 1},
  {id: 4, label: '+ 5', value: 5},
])

</script>

<template>

<header flex-row>
  <h1 text-pink-600 uppercase text-8xl >Compteur</h1>
  <label>Le compteur affiche : {{ count }}</label>
</header>

<main flex-row>
  <div flex>
    <ActionButton v-for="dataButton in dataButtons"
                  :value-button="dataButton.value"
                  :key="dataButton.id"
                  v-model="count"/>
  </div>
  <div>
    <button :disabled="!canUndo" @click="undo()">Undo</button>
    <button :disabled="!canRedo" @click="redo()">Redo</button>
  </div>

  <ul v-for="i in history" :key="i">
    <li>Valeur du compteur : {{ i.snapshot }}</li>
  </ul>
</main>

</template>

<style scoped>

</style>
