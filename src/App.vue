<template>
  <div class="app">
    <h1>To-Do List</h1>
    <form @submit.prevent="addTodo" class="input-section">
      <input v-model="newTodo" placeholder="Tambah kegiatan..." />
      <button type="submit">Tambah</button>
    </form>

    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        {{ todo.text }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const newTodo = ref('')
const todos = ref([])

function addTodo() {
  if (newTodo.value.trim() !== '') {
    todos.value.push({ text: newTodo.value })
    newTodo.value = ''
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
</style>