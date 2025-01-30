<script setup lang="ts">
import AppHeader from '@/components/AppHeader.vue'
import AppFilters from '@/components/AppFilters.vue'
import AppTodoList from '@/components/AppTodoList.vue'
import AppAddTodo from '@/components/AppAddTodo.vue'
import AppFooter from '@/components/AppFooter.vue'
import type { Todo } from '@/types/Todo'
import { ref } from 'vue'

const todos = ref<Todo[]>([
  { id: 0, text: 'Learn the basics of Vue', completed: true },
  { id: 1, text: 'lorem2', completed: false },
  { id: 2, text: 'lorem5', completed: false },
])

const toggleTodo = (id: number) => {
  const targetTodo = todos.value.find((todo: Todo) => todo.id === id)

  if (targetTodo) {
    targetTodo.completed = !targetTodo.completed
  }
}

const removeTodo = (id: number) => {
  todos.value = todos.value.filter((todo: Todo) => todo.id !== id)
}
const addTodo = (todo: Todo) => {
  todos.value.push(todo)
}
</script>

<template>
  <AppHeader />

  <AppFilters />

  <main class="app-main">
    <AppTodoList :todos="todos" @toggleTodo="toggleTodo" @removeTodo="removeTodo" />

    <AppAddTodo @addTodo="addTodo" />
  </main>

  <AppFooter />
</template>

<style scoped></style>
