<script setup lang="ts">
 const props = defineProps<{
   modelValue: Number,
   valueButton: Number
  }>()
 const emits = defineEmits(['update:modelValue'])

 function addOrSubstract() {
   emits('update:modelValue', props.modelValue + props.valueButton)
 }
</script>

<template>
    <button @click="addOrSubstract" >{{ valueButton }}</button>
</template>

<style scoped>

</style>