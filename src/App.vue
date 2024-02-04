<script setup>
import { RouterView } from "vue-router";
import TodoHeader from "./components/TodoHeader.vue";
import Footer from "./components/Footer.vue";
</script>

<template>
  <TodoHeader />
  <div class="content">
    <RouterView />
  </div>
  <Footer />
</template>

<style lang="scss">
* {
  font-family: "Rubik", "sans-serif";
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.content {
  min-height: 85vh;
}
.container {
  max-width: 1100px;
  margin: 0 auto;
}
</style>
