<template>
    <div class="todo-input">
      <input v-model="task" type="text" placeholder="Add a new task" />
      <button @click="addTask">📝Add Task</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        task: '',
      };
    },
    emits: ['add-task'],
    methods: {
      addTask() {
        if (this.task.trim()) {
          this.$emit('add-task', this.task.trim());
          this.task = '';
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .todo-input {
    display: flex;
    align-items: flex-start;
    gap: 10px;
  }
  
  input {
    flex: 1;
    padding: 10px;
    height: 40px;
    border: 1px solid var(--button-bg-color);
    border-radius: 5px;
    background-color: var(--card-bg-color);
    color: var(--text-color);
    transition: background-color 0.3s ease, color 0.3s ease;
    font-size: 16px;
  }
  
  button {
    height: 40px;
    padding: 0 15px;
    border: none;
    border-radius: 5px;
    background-color: var(--success-color);
    color: white;
    cursor: pointer;
    transition: background-color 0.3s ease;
    font-size: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  button:hover {
    background-color: darkgreen;
  }
  </style>
  
  
  
  
