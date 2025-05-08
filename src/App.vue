<template>
  <div class="container">
    <h1>To-do with Vue</h1>

    <form @submit.prevent="addTodo">
      <input v-model="newTodo" placeholder="Add a task" />
      <button type="submit">Add</button>
    </form>

    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.done" />
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
        <button @click="deleteTodo(index)">❌</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const newTodo = ref('')
const todos = ref([])

function addTodo() {
  if (newTodo.value.trim()) {
    todos.value.push({ text: newTodo.value, done: false })
    newTodo.value = ''
  }
}

function deleteTodo(index) {
  todos.value.splice(index, 1)
}
</script>

<style scoped>
.container {
  max-width: 400px;
  margin: 10;
  padding: 20px;
  font-family: sans-serif;
}

.done {
  text-decoration: line-through;
  color: blue;
}

input[type="text"] {
  width: 70%;
  padding: 8px;
  margin-right: 8px;
}

button {
  padding: 6px 10px;
  margin: 4px;
}
</style>
