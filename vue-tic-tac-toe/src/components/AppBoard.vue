<template>
  <div>
    <div>
      <h2>Current Player: {{ currentPlayer }}</h2>
    </div>
    <div id="app-board">
      <div v-for="(square, index) in squares" :key="index">
        <AppSquare v-bind:square="square" @squareClicked="makeMove(index)" />
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import AppSquare from './AppSquare.vue'

export default {
  components: { AppSquare },
  name: 'AppBoard',
  data() {
    return {
      squares: [],
      isXTurn: true
    }
  },
  computed: {
    currentPlayer() {
      return this.isXTurn ? 'X' : 'O';
    }
  },
  mounted() {
    this.newGame();
  },
  methods: {
    newGame() {
      this.squares = Array(9).fill(null);
      this.isXTurn = true;
    },

    makeMove(index) {
      Vue.set(this.squares, index, this.currentPlayer);
      this.isXTurn = !this.isXTurn;
    }
  }
}
</script>

<style>
#app-board {
  display: grid;
  grid-template-columns: 200px 200px 200px;
  grid-gap: 0px;
}

#app-square {
  border: 1px gray solid;
  height: 200px;
  font-size: 5em !important;
}
</style>
