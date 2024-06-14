<template>
    <div class="container mt-5">
      <h1 class="text-center mb-4">{{ formattedToday }}</h1>
      
      <div class="input-group mb-4">
        <input
          v-model="newTodoText"
          type="text"
          class="form-control"
          placeholder="Add new Task"
          @keyup.enter="addTodo"
        />
        <button class="btn btn-primary" @click="addTodo">Add Todo</button>
      </div>
  
      <div class="mb-4 text-center">
        <small>
          <span class="badge list-group-item-primary">New</span>
          <span class="badge bg-warning text-dark">In Progress</span>
          <span class="badge bg-success">Completed</span>
        </small>
      </div>
  
      <ul class="list-group">
        <li
          v-for="todo in todos"
          :key="todo.id"
          :class="['list-group-item', getTodoClass(todo)]"
          @dblclick="deleteCompleted(todo)"
        >
          <span>{{ todo.text }}</span>
          <div class="float-end">
            <button
              v-if="todo.state === 'New'"
              class="btn btn-sm btn-warning me-2"
              @click="changeState(todo, 'In Progress')"
            >
              <i class="fas fa-tasks"></i>
            </button>
            <button
              v-if="todo.state === 'In Progress'"
              class="btn btn-sm btn-success me-2"
              @click="changeState(todo, 'Completed')"
            >
              <i class="fas fa-check"></i>
            </button>
            <button
              v-if="todo.state === 'In Progress'"
              class="btn btn-sm btn-primary me-2"
              @click="changeState(todo, 'New')"
            >
              <i class="fas fa-undo"></i>
            </button>
            <button
              v-if="todo.state !== 'Completed'"
              class="btn btn-sm btn-danger"
              @click="deleteTodo(todo.id)"
            >
              <i class="fas fa-trash"></i>
            </button>
          </div>
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, watch } from 'vue';
  
  const newTodoText = ref('');
  const todos = ref([]);
  const today = new Date();
  const formattedToday = today.toLocaleDateString('en-GB').replaceAll("/","-");

  const loadTodos = () => {
    const savedTodos = localStorage.getItem('todos');
    if (savedTodos) {
      todos.value = JSON.parse(savedTodos);
    }
  };
  
  const saveTodos = () => {
    localStorage.setItem('todos', JSON.stringify(todos.value));
  };
  
  const addTodo = () => {
    if (newTodoText.value.trim()) {
      todos.value.push({
        id: Date.now(),
        text: newTodoText.value.trim(),
        state: 'New',
      });
      newTodoText.value = '';
    }
  };
  
  const changeState = (todo, newState) => {
    todo.state = newState;
  };
  
  const deleteTodo = (id) => {
    todos.value = todos.value.filter((todo) => todo.id !== id);
  };
  
  const deleteCompleted = (todo) => {
    if (todo.state === 'Completed') {
      deleteTodo(todo.id);
    }
  };
  
  const getTodoClass = (todo) => {
    if (todo.state === 'New') {
      console.log(todo);
      return 'list-group-item-primary';
    } else if (todo.state === 'In Progress') {
      return 'list-group-item-warning';
    } else if (todo.state === 'Completed') {
      return 'list-group-item-success';
    }
  };
  
  onMounted(loadTodos);
  watch(todos, saveTodos, { deep: true });
  </script>
  
  <style scoped>
  body {
    background-color: #f8f9fa;
    font-family: 'Roboto', sans-serif;
  }
  
  .container {
    max-width: 600px;
  }
  
  h1 {
    color: #343a40;
  }
  
  .input-group {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  .list-group-item {
    border: none;
    border-radius: 0.375rem;
    margin-bottom: 0.5rem;
    padding: 1rem;
    font-weight: bold;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  .list-group-item-primary {
    background-color: #004085 !important;
    color: #cce5ff !important;
  }
  
  .list-group-item-warning {
    background-color: #ffc107;
    color: #212529;
  }
  
  .list-group-item-success {
    background-color:#198754;
    color: #f8f8f8;
  }
  
  .btn {
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .btn:hover {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
  
  .float-end {
    display: flex;
    gap: 0.5rem;
  }
  
  .badge {
    margin: 0 5px;
    padding: 10px;
  }
  </style>
  