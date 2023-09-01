<template>
  <input type="number" v-model="newCount" @keydown.enter="updateCount"/>
</template>
<script lang="ts" setup>
import {ref} from "vue";

const minValue = 100
const maxValue = 599

const emits = defineEmits(['update:modelValue'])

const newCount = ref<number | null>()

function updateCount() {
  if (!newCount.value)
    return

  if ((newCount.value >= minValue) && (newCount.value <= maxValue)) {
    emits('update:modelValue', newCount.value)
    newCount.value = null
  }
}

</script>