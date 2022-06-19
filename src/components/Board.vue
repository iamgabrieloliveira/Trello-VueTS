<template>
    <link
      rel="stylesheet"
      href="https://unicons.iconscout.com/release/v4.0.0/css/line.css"
    />
  <div class="container">
  <div v-if="isEditing" class="editing-container">
    <i v-if="isEditing"  @click="handleEditBoardTitle"  class="uil uil-check-circle icon"></i>
    <div class="text-container">
      <input type="text" v-model="boardTitle" class="title-input" />
      <input type="text" v-model="boardSubTitle" class="subtitle-input"  />
    </div>
    </div>
    <div v-else class="editing-container">
    <i class="uil uil-edit icon" @click="handleEditBoardTitle" ></i>
    <div class="text-container">
      <h1>{{ boardTitle }}</h1> 
      <h2>{{ boardSubTitle }} </h2>
    </div>
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
      ],
      title: "",
      subTitle: "",
      isEditing: false,
      boardTitle: "Frello",
      boardSubTitle: "Frello task board"
    }
  },
  methods: {
    handleEditBoardTitle(){
      this.isEditing = !this.isEditing
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
  justify-content: space-between;
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
  
  min-height: 750px;

  margin: auto;
}
.board-title{
  display: flex;
  align-items: center;

  gap: 14px;
}
.uil.uil-edit.icon, .uil.uil-check-circle.icon {
  font-size: 17px;
  
  color: white;

  cursor: pointer;

  margin-bottom: 36px;
}
.title-input{
  background: none;
  color: white;
  font-size: 2em;
  font-weight: bold;
  border: none;
}
.title-input:focus{
  border: none;
  background: none;
  outline: 0;
}
.title-input::placeholder{
  color: white;
  font-weight: bold;
  border: none;
}
.subtitle-input{
  background: none;
  color: white;
  font-size: 20px;
  font-weight: normal;
  border: none;
  width: auto;  
}
.subtitle-input:focus{
  outline: 0;
  background: none;
  border: none;
}
.subtitle-input::placeholder{
  color: white;
}
.editing-container{
  display: flex;
  gap: 15px;
  align-items: center;
}

</style>

