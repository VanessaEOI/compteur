<script lang="ts">

import ActionButton from "./components/ActionButton.vue";

export default {
    components: {ActionButton},
    data() {
        return {
            count: 0
        }
    },
    methods: {
        addOrSubstract(value) {
            this.count += (value)
        }
    }
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