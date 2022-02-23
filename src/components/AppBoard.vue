<template>
  <div>
    <!-- <div>
      <h2>Current Player: {{ currentPlayer }}</h2>
    </div> -->
    <div id="app-board">
      <div v-for="(square, index) in squares" :key="index" :class="colorWinner(index) ? 'greenWinn': ''" >
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
      winningArr: [],
      style:  false,
      winner: null,
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
      if(this.winner) return ;
      Vue.set(this.squares, index, this.currentPlayer);
      this.winner = this.checkWinner();
      if(!this.winnner) this.isXTurn = !this.isXTurn;
      
    },
    colorWinner(index){
        if(this.winningArr.indexOf(index) > -1){
            return 'greenWinn' ;
        } else{
            return '';
        }
        
    },

    checkWinner(){
      const winner = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6]
      ];

      for (let i = 0; i < winner.length; i++) {
        if (!!this.squares[winner[i][0]] && !!this.squares[winner[i][1]] && !!this.squares[winner[i][2]] &&  this.squares[winner[i][0]] === this.squares[winner[i][1]]  && this.squares[winner[i][0]] === this.squares[winner[i][2]]){
          this.winningArr = [...winner[i]];
          return this.currentPlayer;
        } 
      }
      return null;
    }
    
  }
}
</script>

<style>
.greenWinn{
  color: greenyellow;
}
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
