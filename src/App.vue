<template>
  <div id="app">
    <TodoList :tasks="tasks" @update-tasks="updateTasks" />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  components: {
    TodoList,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    loadTasks() {
      const savedTasks = localStorage.getItem("tasks");
      if (savedTasks) {
        this.tasks = JSON.parse(savedTasks);
      }
    },
    saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    updateTasks(newTasks) {
      this.tasks = newTasks;
      this.saveTasks();
    },
  },
  mounted() {
    this.loadTasks();
  },
};
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0;
  min-height: 100vh;
  background-color: var(--background-color);
  transition: background-color 0.3s;
}
h1 {
  color: var(--text-color);
}

html.dark #app {
  background-color: #121212;
  color: white;
}
</style>
