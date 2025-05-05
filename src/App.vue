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

    <ul>
      <li v-for="(todo, index) in filteredTodos" :key="index" :class="{ done: todo.done }">
        <input type="checkbox" v-model="todo.done" />
        {{ todo.text }} - <small>{{ todo.time }}</small>
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

const filteredTodos = computed(() => {
  return filterIncomplete.value
    ? todos.value.filter(todo => !todo.done)
    : todos.value
})
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
.filter {
  margin-bottom: 15px;
  font-size: 14px;
}
</style>