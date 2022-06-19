<template>
  <link rel="stylesheet" href="https://unicons.iconscout.com/release/v4.0.0/css/line.css"/>
  <div
    v-if="isModalVisible"
    @click="handleShowAddTaskModal"
    class="addtaskmodal-overlay"
  ></div>
  <div class="column-container">
    <div class="column-title-container">
      <input class="title-edit-input" v-if="isEditing" type="text" v-model="ColumnData.title" />
      <h1 v-else class="column-title">{{ ColumnData.title }}</h1>
      <div class="changes-buttons-container">
      <i v-if="isEditing" class="uil uil-check-circle icon edit-btn" @click="handleEditTitleColumn"></i>
      <i v-else class="uil uil-edit icon edit-btn" @click="handleEditTitleColumn"></i>
      <i
        v-if="isModalVisible"
        class="uil uil-times icon-btn"
        @click="handleShowAddTaskModal"
      ></i>
      <i
        v-else
        class="uil uil-plus icon-btn"
        @click="handleShowAddTaskModal"
      ></i>
      </div>
      <div v-if="isModalVisible" class="addtask-modal">
        <div class="addtask-content">
          <input
            v-model="taskTitleAdd"
            type="text"
            class="addtask-input"
            placeholder="Title"
          />
          <input
            v-model="taskDescriptionAdd"
            type="text"
            class="addtask-input"
            placeholder="Description"
          />
          <button class="addtask-button" @click="handleAddTask">
            Create Task
          </button>
        </div>
      </div>
    </div>
    <div 
    class="tasks-wrapper"
    >
      <Task 
        v-for="(task, i) in ColumnData.tasks"
        :key="i"
        :TaskData="task"
        :ColumnData="ColumnData"
        :taskIndex="i"
      />
    </div>
  </div>
</template>

<script lang="ts">

import Task from "./Task.vue";

export default {
  name: "Column",
  components: {
    Task,
  },
  props: {
    ColumnData: Object,
    BoardData: Object,
  },
  data() {
    return {
      isModalVisible: false,
      taskTitleAdd: "",
      taskDescriptionAdd: "",
      isEditing: false,
    };
  },
  methods: {
    handleShowAddTaskModal() {
      this.isModalVisible = !this.isModalVisible;
    },
    handleAddTask() {
      this.handleShowAddTaskModal();

      const newTask = {
        title: this.taskTitleAdd,
        description: this.taskDescriptionAdd,
        columnId: this.ColumnData.columnId,
      };

      if (newTask.title == "" && newTask.description == "") {
        newTask.title = "Title";
        newTask.description = "Description";
      }

      this.taskTitleAdd = "";
      this.taskDescriptionAdd = "";

      this.ColumnData.tasks.push(newTask);
    },
    handleEditTitleColumn(){
      this.isEditing = !this.isEditing
    }
  },
};
</script>

<style scoped>
.column-container {
  min-height: 500px;
  width: 390px;

  background: #f3f5f6;

  padding: 30px;

  border-radius: 5px;
}

.column-title-container {
  margin-bottom: 24px;

  display: flex;
  justify-content: space-between;
  align-items: center;
}

.column-title {
  font-size: 25px;
  color: #313131;
}

.tasks-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 24px;
}

.addtask-modal {
  position: absolute;
  top: 49%;
  left: 50%;

  transform: translate(-50%, -50%);

  width: 360px;
  height: 150px;

  background: #fff;

  border-radius: 4px;
  border: 1px solid #cfd1d1;

  padding: 14px;

  z-index: 100000;
}

.addtask-input {
  background: none;
  color: black;
  border: none;
  font-size: 19px;
  font-weight: normal;
}

.addtask-content {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.addtask-input:focus {
  outline: 0;
  border: none;
}

.addtask-button {
  color: white;

  font-weight: bolder;

  background: none;
  color: black;
  border: red;

  width: 100px;

  border: none;
  border-radius: 4px;

  padding: 4px 8px;

  position: absolute;
  bottom: 16px;
  right: 16px;

  cursor: pointer;

  transition: 0.3s;
}

.addtask-button:hover {
  background: #136cf1;
  color: white;
}

.addtaskmodal-overlay {
  position: absolute;
  inset: 0;
  z-index: 10000;
  background: rgba(0, 0, 0, .5);
}

.icon-btn {
  font-size: 22px;
  font-weight: bolder;
  cursor: pointer;
  position: relative;
  z-index: 1000;
}
.edit-btn{
  font-size: 20px;
  font-weight: bolder;
  cursor: pointer;
  position: relative;
  z-index: 1000;
}

.placeholder {
  background-color: rgba(150, 150, 200, 0.1);
  border: 1px dashed #abc;
  margin: 5px 45px 5px 5px;
}
.changes-buttons-container{
  display: flex;
  align-items: center;
  gap: 10px;
}
.title-edit-input{
  background: none;
  border: none;
  font-size: 25px;
  font-weight: bolder;
  color: #313131;
  width: 250px;
}
.title-edit-input:focus{
  outline: 0;
  background: none;
}

</style>

