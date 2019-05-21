<template>
  <div class="whackamole">
    <h1 class="logo">Whack-a-mole!</h1>
    <button class="start-game" v-on:click="startGame">Start Game</button>
    <Board v-bind:board-props="boardProps"></Board>
    <GameScreen
      v-bind:mole-states="gameState.moleStates"
      v-bind:is-game-active="gameState.isGameActive"
    ></GameScreen>
  </div>
</template>

<script>
import { v1 } from "uuid";
import Board from "./components/Board.vue";
import GameScreen from "./components/GameScreen.vue";

const GAME_TIME_SECONDS = 20; // secs
const MOLE_ACTIVATE_INTERVAL = 500; // ms

const initialGameState = () => {
  const moleStates = {};
  for (let i = 0; i < 4; i += 1) {
    const id = v1();
    moleStates[id] = { id: id, active: false };
  }

  return {
    time: GAME_TIME_SECONDS,
    gameTimer: null,
    moleTimer: null,
    moleStates: moleStates,
    isGameActive: false
  };
};

const initialData = () => {
  return {
    score: 0,
    highScore: 0,
    gameState: initialGameState()
  };
};

const pickOne = arr => arr[Math.floor(Math.random() * arr.length)];

export default {
  name: "App",
  components: {
    Board,
    GameScreen
  },
  data: function() {
    return initialData();
  },
  computed: {
    boardProps: function() {
      return [
        { label: "Score", value: this.score },
        { label: "High Score", value: this.highScore },
        { label: "Timer", value: this.gameState.time }
      ];
    }
  },
  methods: {
    resetState: function() {
      this.endGame();
      this.gameState = initialGameState();
    },
    startGame: function() {
      this.resetState();
      this.gameState.isGameActive = true;
      this.startTimer();
      this.startMole();
    },
    endGame: function() {
      this.gameState.isGameActive = false;
      this.endMole();
      this.endTimer();
    },
    startTimer: function() {
      this.gameState.gameTimer = setInterval(() => {
        this.gameState.time -= 1;
        if (this.gameState.time <= 0) {
          this.endGame();
        }
      }, 1000);
    },
    endTimer: function() {
      if (this.gameState.gameTimer) {
        clearInterval(this.gameState.gameTimer);
      }
    },
    startMole: function() {
      this.gameState.moleTimer = setInterval(
        () => this.activateRandomMole(),
        MOLE_ACTIVATE_INTERVAL
      );
    },
    endMole: function() {
      if (this.gameState.moleTimer) {
        clearInterval(this.gameState.moleTimer);
      }
    },
    activateRandomMole: function() {
      const moleId = pickOne(Object.keys(this.gameState.moleStates));
      this.gameState.moleStates[moleId].active = true;
    }
  }
};
</script>

<style>
.whackamole {
  font-family: "Bungee", sans-serif;
  max-width: 960px;
  margin: auto;
  text-align: center;
}

.start-game {
  font-family: "Bungee", sans-serif;
  padding: 20px;
  border-radius: 3px;
  border: 0;
  background-color: #52b1d6;
  color: #fff;
  font-size: 1em;
  cursor: pointer;
}
</style>
