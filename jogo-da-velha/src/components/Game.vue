<script setup lang="ts">

import { reactive, ref, computed, onUpdated } from 'vue'

let xWins = ref(0)
let oWins = ref(0)
let playerXTurn: any = ref(true)


const squares = ref(
    ['⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜']
)


const winner = computed(() => checkForWinner(squares.value.flat()))

function checkForWinner(value: Array<string>) {
    const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
    ]

    for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i]
        if (
            value[a] &&
            value[a] === value[b] &&
            value[a] === value[c]
        ) {
            return value[a]
        }
    }
    return null
}

function newMove(squarePosition: number) {

    if (winner.value && winner.value != '⬜') {
        console.log('inside if winner value: ' + winner.value)
        endGame()
        return
    }

    if (squares.value[squarePosition] == '⬜') {
        if (playerXTurn) {
            squares.value[squarePosition] = '❌'
        } else {
            squares.value[squarePosition] = '⭕'
        }
        playerXTurn = !playerXTurn

    }

    if (winner.value && winner.value != '⬜') {
        console.log('inside if winner value: ' + winner.value)
        endGame()
        return
    }

}

function endGame() {
    squares.value = ['⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜']
    if (!playerXTurn) {
        xWins.value++
    } else {
        oWins.value++
    }
    playerXTurn = true
}

</script>


<template>

    <div class="center">

        <h1># Jogo da Velha #</h1>

        <span>Placar <br>
            <span>❌: {{ xWins }}</span> <span>| </span>
            <span>⭕: {{ oWins }}</span>
        </span> <br>

        <span v-if="playerXTurn">Vez do jogador X</span>
        <span v-else>Vez do jogador O</span>

        <br>
        <div class="container">
            <div class="square unselectable" v-for="(square, index) in squares" :key="index" @click="newMove(index)">
                {{ square }}
            </div>

        </div>
    </div>


</template>

<!-- v-if="symbol.changeable" @click="$emit('next-turn'), changeSymbol(props.turn)">{{ symbol.emoji }} -->
<!-- <div class="square" v-else>{{ symbol.emoji }}</div> -->

<!--
    function endGame(){
    squares.value = ['⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜']
    if(playerXTurn){
        xWins.value++
    }else {
        oWins.value++
    }
}
-->

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

.square {
    border: 0.5px solid;
}

div.square:hover {
    background-color: gray;
}
</style>