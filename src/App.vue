<template>
  <div class="whackamole">
    <h1 class="logo">Whack-a-mole!</h1>
    <button class="start-game">Start Game</button>
    <Board v-bind:board-props="boardProps"></Board>
    <div class="moles-container gameActive">
      <div class="mole-container inactive">
        <div class="mole-image-container">
          <img class="mole" src="./assets/mole.png" alt="mole">
        </div>
        <img class="dirt" src="./assets/dirt.svg" alt="mole dirt">
      </div>
      <div class="mole-container inactive">
        <div class="mole-image-container">
          <img class="mole" src="./assets/mole.png" alt="mole">
        </div>
        <img class="dirt" src="./assets/dirt.svg" alt="mole dirt">
      </div>
      <div class="mole-container inactive">
        <div class="mole-image-container">
          <img class="mole" src="./assets/mole.png" alt="mole">
        </div>
        <img class="dirt" src="./assets/dirt.svg" alt="mole dirt">
      </div>
      <div class="mole-container inactive">
        <div class="mole-image-container">
          <img class="mole" src="./assets/mole.png" alt="mole">
        </div>
        <img class="dirt" src="./assets/dirt.svg" alt="mole dirt">
      </div>
    </div>
  </div>
</template>

<script>
import Board from "./components/Board.vue";

export default {
  name: "App",
  components: {
    Board
  },
  data: function() {
    return {
      score: 0,
      highScore: 0,
      time: 0
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

.moles-container {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  opacity: 0.5;
  transition: opacity 0.3s ease;
}

.moles-container.game-active {
  opacity: 1;
}

.mole-container {
  width: 160px;
  height: 160px;
  display: inline-block;
  margin: 10px;
  position: relative;
}

.mole-image-container {
  overflow: hidden;
  width: 160px;
  height: 140px;
}

.mole-container img {
  display: block;
  transition: all 0.3s ease;
}

.mole {
  position: relative;
  width: 60%;
  margin: auto;
  cursor: pointer;
}

.mole-container.active .mole {
  /* display: block; */
  top: 0px;
}

.mole-container.inactive .mole {
  top: 200px;
}

.dirt {
  width: 100%;
  margin: auto;
  z-index: 1;
  position: absolute;
  bottom: 0;
}
</style>
