<script setup>
import {ref} from 'vue'

const count = ref(0)

const increaseCounter = () =>{
    count.value += 1
}
</script>

<template>
    <button @click="increaseCounter()">Click {{ count }}</button>
</template>