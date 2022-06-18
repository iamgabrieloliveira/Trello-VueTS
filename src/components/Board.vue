<template>
  <div class="container">
    <div class="text-container">
      <h1>Project Name</h1>
      <h2>About Project</h2>
    </div>
    <div class="board-container">
      <Column v-for="column in BoardData" :key="column.columnId" :ColumnData="column" :BoardData="BoardData"/> 
    </div>
  </div>
</template>

<script lang="ts">

import Column from "./Column.vue";

export default {
  name: "Board",
  components: {
    Column,
  },
  data() {
    return {
      BoardData: [
        {
          title: "Backlog",
          columnId: 0,
          tasks: [],
        },
        {
          title: "To Do",
          columnId: 1,
          tasks: [],
        },
        {
          title: "In Progress",
          columnId: 2,
          tasks: [],
        },
        {
          title: "Finished",
          columnId: 3,
          tasks: [],
        }
      ]
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  gap: 50px;
}
.text-container {
  color: white;

  display: flex;
  flex-direction: column;
  gap: 12px;
}
.text-container h2{
  font-weight: lighter;
  font-size: 20px;
}
.board-container {
  display: flex;
  gap: 24px;
  
  height: 700px;

  margin: auto;
}
</style>

