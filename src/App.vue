<script lang="ts">

import ActionButton from "./components/ActionButton.vue"
import {defineComponent, ref} from "vue"


export default defineComponent ({
    components: {ActionButton},
    setup() {
        const count = ref(0)
        function addOrSubstract(buttonValue) {
            count.value += buttonValue
        }
        return {
            count,
            addOrSubstract
        }
    }
})

</script>

<template>

    <h1>Compteur</h1>

    <label>Le compteur affiche : {{ count }}</label>

    <div>
        <ActionButton :buttonValue="-5" @add="addOrSubstract" />
        <ActionButton :buttonValue="-1" @add="addOrSubstract" />
        <ActionButton :buttonValue="1" @add="addOrSubstract" />
        <ActionButton :buttonValue="5" @add="addOrSubstract" />
    </div>

</template>

<style scoped>

</style>