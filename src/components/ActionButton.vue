<script lang="ts">
import {defineComponent, PropType} from "vue";

export default defineComponent({
    props: {
        buttonValue: {
            type : Number as PropType<number>,
            required: true
        }
    },
    emits: ['add']
})

</script>

<template>
    <button @click="$emit('add', buttonValue)" >{{ buttonValue }}</button>
</template>

<style scoped>

</style>