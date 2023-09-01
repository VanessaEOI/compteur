<script setup lang="ts">

import {computed} from 'vue'
import ActionButton from "./components/ActionButton.vue"
import {useRefHistory, useStorage} from "@vueuse/core"
import FreeCountInput from "./components/FreeCountInput.vue";

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


const urlSrcImg = computed(() => `https://http.cat/images/${count.value}.jpg`)

function clearCounter() {
  count.value = 200
  commit()
  clear()
}

</script>

<template>

  <main>
    <div>
      <img alt="cat" :src="urlSrcImg" style="height: 400px">
    </div>
    <div>
      <h1 text-pink-600 uppercase text-4xl>Counter : <span text-black text-2xl>{{ count }}</span></h1>
    </div>
    <div>
      <FreeCountInput v-model="count"/>
    </div>
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

    <ul list-none style="position:absolute;">
      <li v-for="(entry, i) in history" :key="i">{{ entry.snapshot }}</li>
    </ul>

  </main>

</template>

