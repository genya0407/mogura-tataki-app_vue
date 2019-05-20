<template>
  <div class="whackamole">
    <h1 class="logo">Whack-a-mole!</h1>
    <button class="start-game">Start Game</button>
    <Board v-bind:board-props="boardProps"></Board>
    <GameScreen v-bind:mole-states="moleStates" v-bind:is-game-active="isGameActive"></GameScreen>
  </div>
</template>

<script>
import { v1 } from "uuid";
import Board from "./components/Board.vue";
import GameScreen from "./components/GameScreen.vue";

export default {
  name: "App",
  components: {
    Board,
    GameScreen
  },
  data: function() {
    const moleStates = {};
    for (let i = 0; i < 4; i += 1) {
      const id = v1();
      moleStates[id] = { id: id, active: false };
    }

    return {
      score: 0,
      highScore: 0,
      time: 0,
      moleStates: moleStates,
      isGameActive: true
    };
  },
  computed: {
    boardProps: function() {
      return [
        { label: "Score", value: this.score },
        { label: "High Score", value: this.highScore },
        { label: "Timer", value: this.time }
      ];
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
