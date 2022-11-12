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

.container{
  display: grid;
  grid-template-columns: 0.5fr 1fr 0.5fr;
}

</style>
