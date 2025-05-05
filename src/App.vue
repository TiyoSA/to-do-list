<template>
  <div class="app">
    <h1>To-Do List</h1>
    <form @submit.prevent="addTodo" class="input-section">
      <input v-model="newTodo" placeholder="Tambah kegiatan..." />
      <input v-model="newTime" type="time" class="time-input" />
      <button type="submit">Tambah</button>
    </form>

    <ul>
      <li v-for="(todo, index) in todos" :key="index" :class="{ done: todo.done }">
        <input type="checkbox" v-model="todo.done" />
        {{ todo.text }} - <small>{{ todo.time }}</small>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const newTodo = ref('')
const newTime = ref('')
const todos = ref([])

function addTodo() {
  if (newTodo.value.trim() !== '' && newTime.value !== '') {
    todos.value.push({ text: newTodo.value, time: newTime.value, done: false })
    newTodo.value = ''
    newTime.value = ''
  }
}
</script>

<style scoped>
.app {
  max-width: 600px;
  margin: 0 auto;
  padding: 30px;
}
.input-section {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
input {
  flex: 1;
  padding: 10px;
}
button {
  padding: 10px 20px;
}
.done {
  text-decoration: line-through;
  color: #aaa;
}
</style>