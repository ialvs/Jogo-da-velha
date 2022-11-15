<script setup lang="ts">

import { ref, computed } from 'vue'

let xWins = ref(0)
let oWins = ref(0)
let playerXTurn: any = ref(true)


const squares = ref(
    ['⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜']
)



function checkForDraw(squares: Array<string>) {

    const drawState = squares.filter(square => square == '⬜')
    if (!drawState.includes('⬜') && (winner.value == null)) {
        return true
    } else {
        return false
    }
}


function checkForWinner(squares: Array<string>) {
    console.log("they reached me")

    for (let index = 0; index < squares.length; index++) {
        if (squares[index] == '⬜') {
            squares[index] = ''
        }
        
    }

    const winLines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
    ]

    for (let i = 0; i < winLines.length; i++) {
        const [a, b, c] = winLines[i]
        if (
            squares[a] &&
            squares[a] === squares[b] &&
            squares[a] === squares[c]
        ) {
            console.log("saí", squares[a], squares[b], squares[c])
            return squares[a]

        }
    }
    return null
}

const winner = computed(() => checkForWinner(squares.value.flat()))
const draw = computed(() => checkForDraw(squares.value.flat()))

function newMove(squarePosition: number) {
    //console.log("quando entra = ",squares.value[squarePosition])
    //console.log(winner.value)
    //console.log("pré teste 1", winner.value)


    /*if (winner.value === '❌' || winner.value === '⭕') {
        console.log('inside if winner value: ' + winner.value)
        endGame()
        return
    }*/
    //console.log("pós teste 1", winner.value)

    if (squares.value[squarePosition] == '⬜') {
        if (playerXTurn) {
            squares.value[squarePosition] = '❌'
        } else {
            squares.value[squarePosition] = '⭕'
        }
        playerXTurn = !playerXTurn
    }
    //console.log("quando sai = ",squares.value[squarePosition])

    //console.log("pré teste 2", winner.value)


    if (winner.value != '⬜' && winner.value != null) {
        console.log('inside if winner value: ' + winner.value)
        endGame()
        return
    }

    //console.log("pós teste 2", winner.value)

    console.log(squares.value)
    //console.log(squares.value.flat())
    //console.log(winner.value)
}

function reset() {
    squares.value = ['⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜', '⬜']
    playerXTurn = true
}

function endGame() {

    if (draw.value === false) {
        if (!playerXTurn) {
            xWins.value++
        } else {
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