<template>
  <div id="app">
    <h1>Random Gif Cat</h1>
    <Gif msg="" />
  </div>
</template>

<script>
import Gif from "./components/Gif.vue";

export default {
  name: "App",
  components: {
    Gif,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  background-color: #30cafc;
  background-size: cover;
  color: #2c3e50;
  padding-bottom: 50px;
}
h1 {
  font-size: 80px;
  margin: 0;
  padding: 40px;
}
img {
  margin-bottom: 50px;
}
</style>
