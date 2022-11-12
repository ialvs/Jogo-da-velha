<script setup lang="ts">
import { reactive } from 'vue'

defineProps(['turn'])

let symbol = reactive({ emoji: '⬜' })

defineEmits(['next-turn'])

const changeSymbol = function (turn: boolean) {

    if (turn) {
        symbol.emoji = '❌'
    } else {
        symbol.emoji = '⭕'
    }
}

</script>


<template>

    <div>
        <div @click="$emit('next-turn'), changeSymbol(turn)">{{ symbol.emoji }}</div>
    </div>

</template>


<style scoped>

</style>