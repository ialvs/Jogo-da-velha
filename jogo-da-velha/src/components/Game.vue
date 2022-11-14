<script setup lang="ts">

import Square from './Square.vue'

import { reactive, ref } from 'vue'
import { computed } from 'vue';


const xWins = reactive({ count: 0 })
const oWins = reactive({ count: 0 })
let playerXTurn:any = ref(true)

const squares = ref([
    ['', '', ''],
    ['', '', ''],
    ['', '', '']
])

const calculateWinner = (squares: Array<string>) => {
    const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
    ]
    for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i]
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
            return squares[a]
        }
    }
    return null
}

const winner:any = computed (() => calculateWinner(squares.value.flat()))

const move = (x:number, y:number) => {
    
    if (winner.value) return
    
    if (playerXTurn) {
        squares.value[x][y] = '❌'    
    } else {
        squares.value[x][y] = '⭕' 
    }
    playerXTurn = '⭕' ? true : false 
    
}


</script>


<template>

    <div class="center">

        <h1># Jogo da Velha #</h1>

        <span>Placar <br>
            <span>❌: {{ xWins.count }}</span> <span>| </span>
            <span>⭕: {{ oWins.count }}</span>
        </span> <br>

        <span v-if="playerXTurn">Vez do jogador X</span>
        <span v-else>Vez do jogador O</span>

        <br>
        <div class="container">
            <Square @next-turn="" class="00 unselectable" :turn="playerXTurn" :x="0" :y="0" />
            <Square @next-turn="" class="01 unselectable" :turn="playerXTurn" :x="0" :y="1" />
            <Square @next-turn="" class="02 unselectable" :turn="playerXTurn" :x="0" :y="2" />
            <Square @next-turn="" class="10 unselectable" :turn="playerXTurn" :x="1" :y="0" />
            <Square @next-turn="" class="11 unselectable" :turn="playerXTurn" :x="1" :y="1" />
            <Square @next-turn="" class="12 unselectable" :turn="playerXTurn" :x="1" :y="2" />
            <Square @next-turn="" class="20 unselectable" :turn="playerXTurn" :x="2" :y="0" />
            <Square @next-turn="" class="21 unselectable" :turn="playerXTurn" :x="2" :y="1" />
            <Square @next-turn="" class="22 unselectable" :turn="playerXTurn" :x="2" :y="2" />
        </div>
    </div>


</template>


<style scoped>
.container {
    display: grid;
    grid-template-columns: repeat(3, 33.33%);
    font-size: xx-large;
    float: inline-start;
}

.unselectable {
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
}

.center {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
</style>