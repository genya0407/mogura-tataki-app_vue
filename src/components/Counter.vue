<template>
  <div class="counter">
    <h2>{{label}}</h2>
    <h1>{{value}}</h1>
  </div>
</template>

<script scoped>
export default {
  name: "Counter",
  props: {
    label: String,
    value: Number
  }
};
</script>

<style scoped>
.counter {
  border: 1px solid #000;
  margin-top: 20px;
  padding: 20px;
}

.counter h1,
.counter h2 {
  margin: 0;
}
</style>