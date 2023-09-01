<script setup lang="ts">

import {ref} from 'vue'
import ActionButton from "./components/ActionButton.vue"
import {useRefHistory, useStorage, useFetch, useImage} from "@vueuse/core"
import {computed, watch} from "@vue/runtime-core";
import * as url from "url";

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

const newCount = ref(count.value)

const minValue = 100
const maxValue = 599

const baseUrl = ref('https://http.cat/images/')
const inputHttpCode = ref(count.value)

const urlSrcImg = computed(() => `${baseUrl}${inputHttpCode.value}.jpg`)

const { data } = useFetch(urlSrcImg)


function updateCount() {
  const updatedCount = count.value + newCount.value
  if (updatedCount >= minValue && updatedCount <= maxValue) {
    count.value = updatedCount
    commit()
  }
}

function clearCounter() {
  count.value = 200
  commit()
  newCount.value = null
  clear()
}

</script>

<template>

  <main>
    <div>
      <img alt="" :src="data">
    </div>
    <div>
      <h1 text-pink-600 uppercase text-4xl>Counter : <span text-black text-2xl>{{ count }}</span></h1>
    </div>
    <div>
      <input type="number" v-model="newCount"/>
      <button @click="updateCount" :disabled="!newCount">Update Count</button>
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

    <ul list-none>
      <li v-for="i in history" :key="i">{{ i.snapshot }}</li>
    </ul>

  </main>

</template>

<style scoped>

</style>
