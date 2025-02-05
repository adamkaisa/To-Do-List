<template>
    <div class="todo-item" :class="{ completed: isCompleted }">
      <div class="task-text">
        <span>{{ task }}</span>
      </div>
      <div class="button-group">
        <button class="success" @click="completeTask">✅</button>
        <button class="danger" @click="$emit('remove')">🗑️</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      task: String,
    },
    data() {
      return {
        isCompleted: false,
      };
    },
    methods: {
      completeTask() {
        this.isCompleted = true;
      },
    },
  };
  </script>
  
  <style scoped>
  /* Styling untuk tugas yang telah diselesaikan */
  .todo-item.completed .task-text span {
    text-decoration: line-through;
    color: gray;
  }
  
  /* Mengatur tata letak elemen */
  .todo-item {
    display: flex;
    align-items: flex-start; /* Menjaga agar tombol tetap di atas */
    justify-content: space-between;
    padding: 10px;
    border-radius: 8px;
    margin-top: 10px;
    flex-wrap: wrap; /* Memungkinkan elemen turun ke baris berikutnya */
  }
  
  /* Mengatur teks agar turun ke baris berikutnya jika terlalu panjang */
  .task-text {
    flex: 1;
    min-width: 60%;
    word-wrap: break-word;
    overflow-wrap: break-word;
    white-space: normal;
    margin-bottom: 10px;
  }
  
  /* Mengelompokkan tombol */
  .button-group {
    display: flex;
    gap: 10px; /* Menambahkan jarak antar tombol */
    align-items: center;
  }
  
  /* Styling tombol */
  button {
    padding: 8px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 14px;
  }
  
  .success {
    background-color: #4caf50;
    color: white;
  }
  
  .danger {
    background-color: #f44336;
    color: white;
  }
  </style>
  