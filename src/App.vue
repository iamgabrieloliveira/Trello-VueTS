<template>
  <div class="screen-container">
    <Board />
  </div>
</template>

<script lang="ts">
import Board from "./components/Board.vue";

export default {
  name: "App",
  components: {
    Board,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;

  box-sizing: border-box;

  font-family: "Open Sans", sans-serif;
}

body {
  background: #136cf1;
}
</style>

<style scoped>

.screen-container{
  padding: 40px 120px 20px 120px;
}

</style>