<template>
  <div id="app">
    <my-gauge></my-gauge>
  </div>
</template>

<script>
import MyGauge from "./components/my-gauge.vue"

export default {
  name: "App",
  components: {
    MyGauge,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
