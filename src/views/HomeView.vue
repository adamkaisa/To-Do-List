<!-- src/views/Home.vue -->
<template>
  <div>
    <h1 class="text-center text-3xl font-bold mb-4">To-Do List</h1>
    <ThemeToggle @toggle="toggleTheme" />
    <TodoInput @addTodo="addTodo" />
    <TodoList 
      :todos="todos" 
      @removeTodo="removeTodo" 
      @toggleComplete="toggleComplete" 
    />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import TodoList from '../components/TodoList.vue';
import TodoInput from '../components/TodoInput.vue';
import ThemeToggle from '../components/ThemeToggle.vue';

export default {
  components: {
    TodoList,
    TodoInput,
    ThemeToggle,
  },
  setup() {
    const theme = ref('light');
    const todos = ref([]);

    const saveToLocalStorage = () => {
      localStorage.setItem('todos', JSON.stringify(todos.value));
    };

    const addTodo = (todo) => {
      todos.value.push({ text: todo, completed: false });
      saveToLocalStorage();
    };

    const removeTodo = (index) => {
      todos.value.splice(index, 1);
      saveToLocalStorage();
    };

    const toggleComplete = (index) => {
      todos.value[index].completed = !todos.value[index].completed;
      saveToLocalStorage();
    };

    const toggleTheme = () => {
      theme.value = theme.value === 'light' ? 'dark' : 'light';
    };

    onMounted(() => {
      const savedTodos = localStorage.getItem('todos');
      if (savedTodos) {
        todos.value = JSON.parse(savedTodos);
      }
    });

    return { theme, todos, addTodo, removeTodo, toggleComplete, toggleTheme };
  },
};
</script>

<style scoped>
.light {
  background-color: white;
  color: black;
}

.dark {
  background-color: #333;
  color: white;
}
</style>