<script setup lang="ts">
import AppHeader from '@/components/AppHeader.vue'
import AppFilters from '@/components/AppFilters.vue'
import AppTodoList from '@/components/AppTodoList.vue'
import AppAddTodo from '@/components/AppAddTodo.vue'
import AppFooter from '@/components/AppFooter.vue'
import type { Todo } from '@/types/Todo'
import { computed, ref } from 'vue'
import type { Filter } from '@/types/Filter.ts'
import type { Stats } from '@/types/Stats.ts'

const activeFilter = ref<Filter>('All')

const todos = ref<Todo[]>([
  { id: 0, text: 'Task #1', completed: true },
  { id: 1, text: 'Task #2', completed: false },
  { id: 2, text: 'Task #3', completed: false },
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

const setFilter = (filter: Filter) => {
  activeFilter.value = filter
}

const filteredTodos = computed((): Todo[] => {
  switch (activeFilter.value) {
    case 'Active':
      return activeTodos.value
    case 'Done':
      return doneTodos.value
    case 'All':
    default:
      return todos.value
  }
})

const stats = computed((): Stats => {
  return {
    active: activeTodos.value.length,
    done: doneTodos.value.length,
  }
})

const activeTodos = computed((): Todo[] => {
  return todos.value.filter((todo) => !todo.completed)
})

const doneTodos = computed((): Todo[] => {
  return todos.value.filter((todo) => todo.completed)
})
</script>

<template>
  <AppHeader />

  <AppFilters :active-filter="activeFilter" @setFilter="setFilter" />

  <main class="app-main">
    <AppTodoList :todos="filteredTodos" @toggleTodo="toggleTodo" @removeTodo="removeTodo" />

    <AppAddTodo @addTodo="addTodo" />
  </main>

  <AppFooter :stats="stats" />
</template>

<style scoped></style>
