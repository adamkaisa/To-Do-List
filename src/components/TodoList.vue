<template>
    <div :class="['todo-container', { 'dark-mode': isDark }]">
      <h1>📝To-Do List</h1>
      <TodoInput @add-task="addTask" />
      <div v-for="(task, index) in tasks" :key="index">
        <TodoItem
          :task="task"
          @remove="removeTask(task)"
          @complete-task="completeTask"
        />
      </div>
      <ThemeToggle :isDark="isDark" @toggle-theme="toggleTheme" />
    </div>
  </template>
  
  <script>
  import TodoInput from './TodoInput.vue';
  import TodoItem from './TodoItem.vue';
  import ThemeToggle from './ThemeToggle.vue';
  
  export default {
    components: {
      TodoInput,
      TodoItem,
      ThemeToggle,
    },
    data() {
      return {
        tasks: [],
        isDark: false,
      };
    },
    methods: {
      addTask(task) {
        this.tasks.push(task);
        this.saveTasks(); // Simpan daftar tugas ke localStorage
      },
      removeTask(task) {
        this.tasks = this.tasks.filter((t) => t !== task);
        this.saveTasks(); // Simpan perubahan ke localStorage
      },
      completeTask(task) {
        alert(`Task "${task}" completed!`);
      },
      toggleTheme() {
        this.isDark = !this.isDark;
        document.documentElement.classList.toggle('dark', this.isDark);
      },
      saveTasks() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks)); // Simpan ke localStorage
      },
      loadTasks() {
        const savedTasks = localStorage.getItem('tasks'); // Ambil data dari localStorage
        if (savedTasks) {
          this.tasks = JSON.parse(savedTasks); // Parse data dan tetapkan ke tasks
        }
      },
    },
    mounted() {
      this.loadTasks(); // Muat data dari localStorage saat komponen dipasang
    },
  };
  </script>
  
  <style scoped>
  .todo-container {
    max-width: 400px;
    margin: 50px auto;
    padding: 20px;
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    transition: background-color 0.3s;
  }
  
  .todo-container.dark-mode {
    background-color: #333;
    color: white;
  }
  </style>
  