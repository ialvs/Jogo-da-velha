<script setup lang="ts">

import Square from './Square.vue'

import { reactive, ref } from 'vue'

const xWins = reactive({ count: 0 })
const oWins = reactive({ count: 0 })
let playerXTurn = ref(true)


</script>


<template>

    <div>
        <h1># Jogo da Velha #</h1>
        <span>Placar <br>
            <span>X: {{ xWins.count }}</span> <span> </span>
            <span>O: {{ oWins.count }}</span>
        </span> <br>
        <span v-if="playerXTurn">Vez do jogador X</span>
        <span v-else>Vez do jogador O</span>

        <br>
        <div class="container">
            <Square @next-turn="playerXTurn = !playerXTurn" class="00 unselectable" :turn="playerXTurn" />
            <Square @next-turn="playerXTurn = !playerXTurn" class="01 unselectable" :turn="playerXTurn" />
            <Square @next-turn="playerXTurn = !playerXTurn" class="02 unselectable" :turn="playerXTurn" />
            <Square @next-turn="playerXTurn = !playerXTurn" class="10 unselectable" :turn="playerXTurn" />
            <Square @next-turn="playerXTurn = !playerXTurn" class="11 unselectable" :turn="playerXTurn" />
            <Square @next-turn="playerXTurn = !playerXTurn" class="12 unselectable" :turn="playerXTurn" />
            <Square @next-turn="playerXTurn = !playerXTurn" class="20 unselectable" :turn="playerXTurn" />
            <Square @next-turn="playerXTurn = !playerXTurn" class="21 unselectable" :turn="playerXTurn" />
            <Square @next-turn="playerXTurn = !playerXTurn" class="22 unselectable" :turn="playerXTurn" />
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
</style>