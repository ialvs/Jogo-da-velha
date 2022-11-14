<script setup lang="ts">
import { onMounted, onUpdated, reactive } from 'vue'

const props = defineProps({
    turn : Boolean,
    x : Number,
    y: Number
})

let symbol = reactive({ emoji: '⬜' ,changeable: true})

let propStringX:string = `${props.x}`
let propStringY:string = `${props.y}`

defineEmits(['next-turn',propStringX,propStringY])

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

onUpdated(() => {
  console.log(`${props.x} ${props.y}`)
})

</script>


<template>

    <div>
        <div class="square" v-if="symbol.changeable" @click="$emit('next-turn'), changeSymbol(props.turn)">{{ symbol.emoji }}</div>
        <div class="square" v-else>{{ symbol.emoji }}</div>
    </div>

</template>


<style scoped>
.square{ 
    border: 0.5px solid;
    
}

div.square:hover {
    background-color: gray;
}

</style>