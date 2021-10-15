<template>
  <div id="app">
    <div class="wrapper clearfix">

      <player
        :activePlayer='activePlayer'
        :scorePlayers='scorePlayers'
        :currentScore='currentScore'
        :isWinner='isWinner'
      />
      <controls
        @newGame='handleNewClick'
        @rollDice='handleRollClick'
        @holdScore='handleHoldClick'
        :finalScore='finalScore'
        @handleFinalInput='handleFinalInput'
        :isPlaying='isPlaying'
      />
      <dices
        :dices='dices'
      />
      <popup
        :isOpenPopup='isOpenPopup'
        @confirmRule='handleConfirmClick'
      />

    </div>
  </div>
</template>

<script>
import Player from './components/Players.vue'
import Dices from './components/Dices.vue'
import Controls from './components/Controls.vue'
import Popup from './components/PopupRule.vue'

export default {
  name: "app",
  data() {
    return {
      isPlaying: false,
      isOpenPopup: false,
      activePlayer: 0,
      scorePlayers: [
        0, 0
      ],
      currentScore: 0,
      dices: [1, 1],
      finalScore: 100
    }
  },
  components: {
    Player,
    Dices,
    Controls,
    Popup
  },
  computed: {
    isWinner() {
      let { scorePlayers, finalScore } = this;

      if(scorePlayers[0] >= finalScore || scorePlayers[1] >= finalScore) {
        this.isPlaying = false;
        return true;
      }
      return false;
    }
  },
  methods: {
    nextPlayer() {
      this.activePlayer = this.activePlayer == 0 ? 1 : 0;
      this.currentScore = 0;
    },
    handleNewClick() {
      this.isOpenPopup = true;
    },
    handleConfirmClick() {
      this.isOpenPopup = false;
      this.isPlaying = true;
      this.activePlayer = 0;
      this.scorePlayers = [0, 0];
      this.currentScore = 0;
      this.dices = [1, 1];
    },
    handleRollClick() {
      if(this.isPlaying) {
        let dice1 = Math.floor(Math.random() * 6) + 1;
        let dice2 = Math.floor(Math.random() * 6) + 1;

        this.dices = [dice1, dice2];

        if(dice1 == 1 || dice2 == 1) {
          let activePlayer = this.activePlayer;
          setTimeout(() => {
            alert(`Player ${activePlayer + 1} have rolled in dice 1. Next player turn !!!`);
          }, 500);
          this.nextPlayer();
        } else {
          this.currentScore += dice1 + dice2;
        }
      } else {
        alert('Click new game first !!!')
      }
    },
    handleHoldClick() {
      if(this.isPlaying) {
        let {scorePlayers, activePlayer, currentScore} = this;
        let oldScore = scorePlayers[activePlayer];
        // let cloneScore = [...scorePlayers];

        // cloneScore[activePlayer] = oldScore + currentScore;
        // this.scorePlayers = cloneScore;
        this.$set(this.scorePlayers, activePlayer, oldScore + currentScore);

        if(!this.isWinner) {
          this.nextPlayer();
        }
      } else {
        alert('Click new game first !!!')
      }
    },
    handleFinalInput(e) {
      this.finalScore = e.target.value;
    }
  }
};
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;

}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('./assets/back.jpg');
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}
</style>
