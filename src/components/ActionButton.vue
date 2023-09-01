<script setup lang="ts">

const props = defineProps<{
  modelValue: Number,
  valueButton: Number
}>()
const emits = defineEmits(['update:modelValue'])

function addOrSubstract() {
  const newValue = props.modelValue + props.valueButton;
  emits('update:modelValue', newValue);
}
</script>

<template>
  <button @click="addOrSubstract">{{ valueButton }}</button>
</template>

<style scoped>

</style>