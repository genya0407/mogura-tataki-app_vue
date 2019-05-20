<template>
  <div class="board">
    <Counter
      v-for="boardProp in boardProps"
      v-bind:label="boardProp.label"
      v-bind:value="boardProp.value"
      v-bind:key="boardProp.label"
    ></Counter>
  </div>
</template>

<script>
import Counter from "./Counter.vue";

export default {
  name: "Board",
  components: {
    Counter
  },
  props: {
    boardProps: Array
  }
};
</script>

<style scoped>
.board {
  display: flex;
  justify-content: space-evenly;
}
</style>