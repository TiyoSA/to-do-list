<template>
  <div class="app">
    <h1>To-Do List</h1>
    
    <form @submit.prevent="addTodo" class="input-section">
      <input v-model="newTodo" placeholder="Tambah kegiatan..." />
      <input v-model="newTime" type="time" class="time-input" />
      <button type="submit">Tambah</button>
    </form>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="filterIncomplete" />
        Tampilkan yang belum selesai
      </label>
    </div>

    <div class="table-header">
      <span class="col-checkbox">Selesai</span>
      <span class="col-task">Kegiatan</span>
      <span class="col-action">Aksi</span>
    </div>

    <ul class="todo-table">
      <li
        v-for="(todo, index) in filteredTodos"
        :key="index"
        :class="{ done: todo.done }"
      >
        <div class="col-checkbox">
          <input type="checkbox" v-model="todo.done" />
        </div>
        <div class="col-task">
          <span>{{ todo.text }} - <small>{{ todo.time }}</small></span>
        </div>
        <div class="col-action">
          <button @click="removeTodo(index)">Batal</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const newTodo = ref('')
const newTime = ref('')
const todos = ref([])
const filterIncomplete = ref(false)

function addTodo() {
  if (newTodo.value.trim() !== '' && newTime.value !== '') {
    todos.value.push({ text: newTodo.value, time: newTime.value, done: false })
    newTodo.value = ''
    newTime.value = ''
  }
}

function removeTodo(index) {
  todos.value.splice(index, 1)
}

const filteredTodos = computed(() => {
  return filterIncomplete.value
    ? todos.value.filter(todo => !todo.done)
    : todos.value
})
</script>

<style scoped>
body {
  margin: 0;
  background-color: #121212;
  color: #f1f1f1;
  font-family: 'Segoe UI', sans-serif;
}

.app {
  background-color: #1e1e1e;
  max-width: 700px;
  margin: 50px auto;
  padding: 30px 25px;
  border-radius: 15px;
  box-shadow: 0 0 25px rgba(0, 0, 0, 0.4);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  color: #4dd0e1;
}

.input-section {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input[type="text"],
input[type="time"] {
  padding: 10px;
  background-color: #2c2c2c;
  border: 1px solid #444;
  border-radius: 8px;
  color: white;
}

input[type="text"] {
  flex: 2;
}

input[type="time"] {
  flex: 1;
}

button {
  padding: 10px 16px;
  border: none;
  background-color: #4dd0e1;
  color: #1e1e1e;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

button:hover {
  background-color: #26c6da;
}

.filter {
  margin-bottom: 15px;
  font-size: 14px;
}

/* Tabel gaya horizontal */
.table-header {
  display: flex;
  font-weight: bold;
  margin-bottom: 10px;
  padding: 8px 10px;
  background-color: #333;
  border-radius: 6px;
}

.table-header span {
  flex: 1;
  color: #4dd0e1;
}

.todo-table {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-table li {
  display: flex;
  align-items: center;
  padding: 10px;
  margin-bottom: 8px;
  background-color: #2b2b2b;
  border-radius: 6px;
  transition: background 0.2s;
}

.todo-table li.done .col-task span {
  text-decoration: line-through;
  color: #999;
}

.col-checkbox,
.col-task,
.col-action {
  flex: 1;
  display: flex;
  align-items: center;
}

.col-task {
  padding: 0 10px;
}

.col-task span {
  word-break: break-word;
}

.col-action {
  justify-content: flex-end;
}

.todo-table button {
  background-color: #ff5252;
  padding: 6px 12px;
  border-radius: 6px;
  font-size: 14px;
  font-weight: bold;
  border: none;
  cursor: pointer;
  color: white;
}

.todo-table button:hover {
  background-color: #ff1744;
}
</style>