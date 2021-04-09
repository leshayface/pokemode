<template>
  <div id="app" class="bg-gray-200" style="margin:0;">
    <!-- style="background: #FFC519; margin:0;" -->
    <Pokemon />
  </div>
</template>

<script>
import Pokemon from "./components/Pokemon";
import "./assets/css/tailwind.css";

export default {
  name: "App",
  components: {
    Pokemon,
  },
};
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
