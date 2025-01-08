<template>
    <input type="text" v-model="page.title">
    Temps écoulé : {{ time }}
    <button @click="reset">Reset</button>
</template>

<script setup>
import { ref, watchEffect } from 'vue'
import { useTimer } from '@/composable/useTimer.js'

const page = ref({
    title: ''
})
const {time, reset} = useTimer()

watchEffect(() => {
    document.title = page.value.title;
})

</script>

<style>

</style>
