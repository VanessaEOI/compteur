<script lang="ts">
export default {
    props: {
        value: Number
    },
    emits: ['add']
}
</script>

<template>
    <button @click="$emit('add', value)" >{{ value }}</button>
</template>

<style scoped>

</style>