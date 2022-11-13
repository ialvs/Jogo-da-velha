<script setup lang="ts">
import { reactive } from 'vue'

defineProps(['turn'])

let symbol = reactive({ emoji: '⬜' ,changeable: true})

defineEmits(['next-turn'])

const changeSymbol = function (turn: boolean) {

   if (symbol.changeable) {
        if (turn) {
            symbol.emoji = '❌'
        } else {
            symbol.emoji = '⭕'
        }
        symbol.changeable = false
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