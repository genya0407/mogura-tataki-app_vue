<template>
  <div v-bind:class="{ 'moles-container': true, 'game-active': isGameActive }">
    <Mole
      v-for="moleId in moleIds"
      v-bind:mole-state="moleStates[moleId]"
      v-bind:key="moleId"
      v-on:mole-clicked="propagateMoleClickedEvent"
    ></Mole>
  </div>
</template>

<style scoped>
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
</style>

<script>
import Mole from "./Mole.vue";

export default {
  name: "GameScreen",
  components: {
    Mole
  },
  props: {
    isGameActive: Boolean,
    moleStates: Object,
    moleClickedHandler: Function
  },
  computed: {
    moleIds: function() {
      return Object.keys(this.moleStates);
    }
  },
  methods: {
    propagateMoleClickedEvent: function(moleId) {
      if (this.isGameActive) {
        this.$emit("mole-clicked", moleId);
      }
    }
  }
};
</script>