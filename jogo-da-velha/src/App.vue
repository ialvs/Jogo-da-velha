<script setup lang="ts">
import Game from './components/Game.vue'

</script>


<template>

  <div class="container">
    <div></div>
    <Game />
    <div></div>
  </div>

</template>


<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@300&display=swap');


.container{
  display: grid;
  grid-template-columns: 0.5fr 1fr 0.5fr;
  font-family: 'Rubik', sans-serif;
}

</style>
