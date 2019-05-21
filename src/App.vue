<template>
  <div class="whackamole">
    <h1 class="logo">Whack-a-mole!</h1>
    <button class="start-game" v-on:click="startGame">Start Game</button>
    <Board v-bind:board-props="boardProps"></Board>
    <GameScreen v-bind:mole-states="moleStates" v-bind:is-game-active="isGameActive"></GameScreen>
  </div>
</template>

<script>
import { v1 } from "uuid";
import Board from "./components/Board.vue";
import GameScreen from "./components/GameScreen.vue";

const GAME_INTERVAL = 20;

const initialData = () => {
  const moleStates = {};
  for (let i = 0; i < 4; i += 1) {
    const id = v1();
    moleStates[id] = { id: id, active: false };
  }

  return {
    score: 0,
    highScore: 0,
    time: GAME_INTERVAL,
    timer: null,
    moleStates: moleStates,
    isGameActive: false
  };
};

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
        { label: "Timer", value: this.time }
      ];
    }
  },
  methods: {
    resetState: function() {
      const data = initialData();
      Object.keys(data).forEach(key => {
        this[key] = data[key];
      });
    },
    startGame: function() {
      this.resetState();
      this.isGameActive = true;
      this.timer = setInterval(() => {
        this.time -= 1;
        if (this.time <= 0) {
          this.endGame();
        }
      }, 1000);
    },
    endGame: function() {
      this.isGameActive = false;
      if (this.timer) {
        clearInterval(this.timer);
      }
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
