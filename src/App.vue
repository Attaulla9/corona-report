<template>
  <div id="app">
    <Navbar />
    <Corona />
  </div>
</template>

<script>
import Corona from "./components/Corona.vue";
import Navbar from "./components/Navbar.vue";

export default {
  name: "App",
  components: {
    Corona,
    Navbar
  }
};
</script>

<style>
</style>
