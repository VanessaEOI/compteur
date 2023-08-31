<script setup lang="ts">

import ActionButton from "./components/ActionButton.vue";
import {useRefHistory, useStorage} from "@vueuse/core";

const count = useStorage<number>('count', 200)

const {history, undo, redo, canUndo, canRedo, clear, commit} = useRefHistory(count, {capacity: 10})

const dataButtons = [
  {id: 1, label: '- 100', value: -100},
  {id: 2, label: '- 10', value: -10},
  {id: 3, label: '- 1', value: -1},
  {id: 4, label: '+ 1', value: 1},
  {id: 5, label: '+ 10', value: 10},
  {id: 6, label: '+ 100', value: 100},
]

function clearCounter() {
  count.value = 200
  commit()
  clear()
}

</script>

<template>

  <header>
    <h1 text-pink-600 uppercase text-4xl>Compteur : <span text-black text-2xl>{{ count }}</span></h1>
  </header>

  <main>
    <div>
      <ActionButton v-for="dataButton in dataButtons"
                    :value-button="dataButton.value"
                    :key="dataButton.id"
                    v-model="count"/>
    </div>
    <div>
      <button :disabled="!canUndo" @click="undo()">Undo</button>
      <button :disabled="!canRedo" @click="redo()">Redo</button>
      <button @click="clearCounter">Clear</button>
    </div>

    <ul list-none>
      <li v-for="i in history" :key="i">{{ i.snapshot }}</li>
    </ul>

  </main>

</template>

<style scoped>

</style>
