<script setup lang="ts">

import { ref, computed } from 'vue'

let xWins = ref(0)
let oWins = ref(0)
let playerXTurn: any = ref(true)


const squares = ref(
    ['⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜']
)

const winner = computed(() => checkForWinner(squares.value.flat()))
const draw = computed(() => checkForDraw(squares.value))

function checkForDraw(squares: Array<string>) {

    const drawState = squares.filter(square => square == '⬜')

    if (drawState.length === 0 && (winner.value == null)) {
        return true
    } else {
        return false
    }
}

function checkForWinner(squares: Array<string>) {
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
            squares[a] &&
            squares[a] === squares[b] &&
            squares[a] === squares[c]
        ) {
            return squares[a]
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

function reset() {
    squares.value = ['⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜']
    playerXTurn = true
}

function endGame() {


    if (!playerXTurn && draw.value === false) {
        xWins.value++
    } else {
        if (draw.value === false) {
            oWins.value++
        }
    }

    playerXTurn = true
    reset()
}

</script>


<template>

    <div class="center">

        <h1># Jogo da Velha #</h1>

        <h2 class="center2">Placar
            <span>❌: {{ xWins }}</span> <span>| </span>
            <span>⭕: {{ oWins }}</span>
        </h2> <br>

        <span v-if="playerXTurn && draw === false">Vez do jogador X</span>
        <span v-else-if="draw === false">Vez do jogador O</span>
        <span v-if="draw">Empate!</span>
        <br>
        <div class="container">
            <div class="square unselectable" v-for="(square, index) in squares" :key="index" @click="newMove(index)">
                {{ square }}
            </div>
            <br>
            <button @click="reset">Reset</button>

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

.center2 {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
}

.square {
    border: 0.5px solid;
}

div.square:hover {
    background-color: gray;
}
</style>