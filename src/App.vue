<script setup lang="ts">

import ActionButton from "./components/ActionButton.vue";

import { ref } from 'vue'

const count = ref(0)
function addOrSubstract(value) {
    count.value += value
}

</script>

<template>

    <h1>Compteur</h1>

    <label count="count" >Le compteur affiche : {{ count }}</label>

    <div>
        <ActionButton :value="-1" @add="addOrSubstract" />
        <ActionButton :value="-5" @add="addOrSubstract" />
        <ActionButton :value="1" @add="addOrSubstract" />
        <ActionButton :value="5" @add="addOrSubstract" />
    </div>

</template>

<style scoped>

</style>
