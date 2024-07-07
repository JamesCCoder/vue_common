<template>
  <div>
    <h1>My To-Do List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    <button @click="addTask">Add</button>

    <div v-for="(task, index) in tasks" :key="index" class="task-item">
      <div v-if="!task.editing">{{ task.text }}</div>
      <input v-else v-model="task.text" @keyup.enter="saveTask(index)" @blur="saveTask(index)" />
      <button @click="editTask(index)">Edit</button>
      <button @click="deleteTask(index)">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      newTask: '',
      tasks: [
        { text: 'Task 1', editing: false },
        { text: 'Task 2', editing: false }
      ]
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, editing: false });
        this.newTask = '';
      }
    },
    editTask(index) {
      this.tasks[index].editing = true;
    },
    saveTask(index) {
      if (this.tasks[index].text.trim() === '') {
        this.deleteTask(index);
      } else {
        this.tasks[index].editing = false;
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.task-item {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.task-item div,
.task-item input {
  flex: 1;
}

.task-item button {
  margin-left: 10px;
}
</style>
