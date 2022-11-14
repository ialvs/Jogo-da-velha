<script setup lang="ts">

import { reactive, ref } from 'vue'
import { computed } from 'vue'

const xWins = reactive({ count: 0 })
const oWins = reactive({ count: 0 })
let playerXTurn: any = ref(true)


const squares = reactive({
    positions:['⬜','⬜','⬜','⬜','⬜','⬜','⬜','⬜','⬜'],
    emoji: '⬜',
    changeable: true
})


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
            <div class="square unselectable" v-for="(square, index) in squares.positions" :key="index" @click="">
                {{ square }}
            </div>

        </div>
    </div>


</template>

<!-- v-if="symbol.changeable" @click="$emit('next-turn'), changeSymbol(props.turn)">{{ symbol.emoji }} -->
<!-- <div class="square" v-else>{{ symbol.emoji }}</div> -->

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