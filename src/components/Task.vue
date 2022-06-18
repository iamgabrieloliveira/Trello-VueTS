<template>
  <link
    rel="stylesheet"
    href="https://unicons.iconscout.com/release/v4.0.0/css/line.css"
  />
  <div class="task-container">
    <div v-if="isEditing" class="task-data">
      <input v-model="titleInput" type="text" :placeholder="TaskData.title" class="edit-input title-input" />
      <input v-model="descriptionInput" type="text" :placeholder="TaskData.description" class="edit-input description-input" />
    </div>
    <div v-else class="task-data">
      <h1>{{ TaskData.title }}</h1>
      <h2>{{ TaskData.description }}</h2>
    </div>

    <div class="utility-icons">
      <i v-if="isEditing" class="uil uil-check-circle icon" @click="handleEditTask"></i>
      <i v-else class="uil uil-edit icon" @click="handleEditTask"></i>
      <i class="uil uil-trash-alt icon" @click="handleDeleteTask"></i>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: "Task",
  props: {
    TaskData: Object,
    ColumnData: Object,
    taskIndex: Number,
  },
  data() {
    return {
      isEditing: false,
      titleInput: this.TaskData.title,
      descriptionInput: this.TaskData.description,
    };
  },
  methods: {
    handleDeleteTask() {
      this.ColumnData.tasks.splice(this.taskIndex, 1);
    },
    handleEditTask(){
      this.isEditing = !this.isEditing
      this.TaskData.title = this.titleInput;
      this.TaskData.description = this.descriptionInput;
    }
  },
};
</script>

<style scoped>
.task-container {
  width: 330px;
  height: 150px;

  background: #fff;

  border-radius: 12px;

  box-shadow: 0px 10px 0px rgba(0, 0, 0, 0.15);

  padding: 20px;

  display: flex;
  flex-direction: column;
  gap: 15px;

  cursor: pointer;
}

.task-container h1, .title-input {
  font-size: 18px;
  font-weight: bold;
}
.task-container h2, .description-input {
  font-size: 15px;
  font-weight: lighter;
}
.icon {
  font-size: 22px;
  color: #0000008c;
  cursor: pointer;
}
.utility-icons {
  position: absolute;
  margin-left: 249px;
  display: flex;
  margin-top: -10px;
  gap: 6px;
}

.task-data{
  display: flex;
  flex-direction: column;
  gap: 15px;

  margin-top: 10px;
}
.edit-input{
  background: none;
  border: none;

  color: black;
}
.edit-input:focus{
  border: none;
  background: none;
  outline: none;
}
.edit-input::placeholder{
  color: black;
}
</style>