<template>
  <div id="app">
    <Simon />
  </div>
</template>

<script>
import Simon from "./components/Simon.vue";

export default {
  name: "App",
  components: {
    Simon,
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
