<script setup lang="ts">

import ActionButton from "./components/ActionButton.vue";
import {ref} from 'vue'
import {useRefHistory, useStorage, useTemplateRefsList} from "@vueuse/core";
import {nextTick, watch} from "@vue/runtime-core";

const count = ref(0)
const refs = useTemplateRefsList<HTMLDivElement>()
const { history, undo, redo, canUndo, canRedo } = useRefHistory(count, { capacity: 10 })

watch(refs, async () => {
  await nextTick()
  console.log([...refs["value"]])
}, {
  deep: true,
  flush: 'post',
})

useStorage('count', count)

const dataButtons = ref([
  {id: 1, label: '-1', value: -1},
  {id: 2, label: '-5', value: -5},
  {id: 3, label: '+ 1', value: 1},
  {id: 4, label: '+ 5', value: 5},
])

</script>

<template>

  <h1>Compteur</h1>

  <label>Le compteur affiche : {{ count }}</label>

  <div>
    <ActionButton v-for="dataButton in dataButtons"
                  :value-button="dataButton.value"
                  :key="dataButton.id"
                  v-model="count"/>
  </div>
  <div>
    <button :disabled="!canUndo" @click="undo()">Undo</button>
    <button :disabled="!canRedo" @click="redo()">Redo</button>
  </div>

  <div v-for="i in history" :key="i.timestamp">
    <span>Valeur du compteur : {{ i.snapshot }} </span>
  </div>

</template>

<style scoped>

</style>
