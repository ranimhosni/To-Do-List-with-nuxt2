<template>
  <div class="todo-container">
    <h2>To-Do List 📝</h2>
    
    <div class="todo-input">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="    add your task here" />
      <button @click="addTask">Add</button>
    </div>

    <ul>
      <li v-for="(task, index) in tasks" :key="index">
      <label class="checkbox-container">
  <input type="checkbox">
  <div class="checkbox-custom":class="{ done: task.completed }" @click="toggleTask(index)"></div>
</label>
        <span :class="{ done: task.completed }" @click="toggleTask(index)">
          {{ task.text }}
        </span>
        <button @click="removeTask(index)">✖</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: []
    };
  },
  mounted() {
    this.loadTasks();
  },
  methods: {
    addTask() {
      if (this.newTask.trim() === "") return;

      this.tasks.push({ text: this.newTask, completed: false });
      this.newTask = "";
      this.saveTasks();
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
      this.saveTasks();
    },
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    loadTasks() {
      const savedTasks = localStorage.getItem("tasks");
      if (savedTasks) {
        this.tasks = JSON.parse(savedTasks);
      }
    }
  }
};
</script>

<style scoped>
.todo-container {
  max-width: 400px;
  margin:10%;
  margin-left:35%;
  
  
}
.todo-input {
  display: flex;
  gap: 10px;

}
.todo-input button{
  color: white;
  background: rgb(248, 78, 27);
  border: 1px  rgba(255, 255, 255, 0.2);
  border-radius: 5em;
  width: 100px;
  height: 40px;
  margin:8px;
}
.todo-input input {
  flex: 1;
  padding: 0px;
  background: rgba(243, 232, 232, 0.97);
  border: 2px  rgba(255, 255, 255, 0.2);
  border-radius: 9999em;
  position: relative;
  margin:8px;
  margin-right:0px;
  
}
button {
  cursor: pointer;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  display: flex;
  justify-content: space-between;
  padding: 8px;
  border-bottom: 1px solid #ddd;
}
.done {
  text-decoration: line-through;
  color: gray;
}
*{
    background-color: white;
    padding:7px;
    border-radius: 0.9em;
    
}
h2{
    color: rgba(23, 5, 63, 0.73);
}
.checkbox-container {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.checkbox-container input {
  display: none;
}

.checkbox-custom {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  border: 1px solid grey;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: 0.3s;
}

.checkbox-container input:checked + .checkbox-custom {
  background-color: rgb(248, 78, 27);
  border-color: rgb(248, 78, 27);
}

.checkbox-container input:checked + .checkbox-custom::after {
  content: "✔";
  color: white;
  font-size: 14px;
  font-weight: bold;
}
</style>
