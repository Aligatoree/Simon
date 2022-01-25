<template>
  <div id="app">
    <Saimon />
  </div>
</template>

<script>
import Saimon from "./components/Saimon.vue";

export default {
  name: "App",
  components: {
    Saimon,
  },
};
</script>

<style>
body {
  background-color: rgb(255, 255, 225);
}
#app {
  width: 60%;
  min-width: 300px;
  margin: 50px auto;
}
</style>
