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
      tasks: [], // Data todo list
    };
  },
  methods: {
    loadTasks() {
      const savedTasks = localStorage.getItem("tasks");
      if (savedTasks) {
        this.tasks = JSON.parse(savedTasks); // Muat data dari localStorage
      }
    },
    saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks)); // Simpan data ke localStorage
    },
    updateTasks(newTasks) {
      this.tasks = newTasks; // Perbarui daftar tugas
      this.saveTasks(); // Simpan perubahan ke localStorage
    },
  },
  mounted() {
    this.loadTasks(); // Muat data saat aplikasi diluncurkan
  },
};
</script>

<style>
/* CSS dasar untuk elemen root aplikasi */
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
/* Mode gelap: set background */
html.dark #app {
  background-color: #121212;
  color: white;
}
</style>
