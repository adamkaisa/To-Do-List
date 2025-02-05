<template>
    <button @click="toggleTheme">
      {{ isDark ? '☀️' : '🌙' }}
    </button>
  </template>
  
  <script>
  export default {
    props: {
      isDark: Boolean,
    },
    emits: ['toggle-theme'],
    methods: {
      toggleTheme() {
        this.$emit('toggle-theme');
      },
    },
  };
  </script>
  
  <style scoped>
  button {
    position: absolute;
    top: 10px;
    right: 10px;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    color: #000;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  button:hover {
    background-color: #f0f0f0;
  }
  </style>
  
