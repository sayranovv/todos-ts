<script setup lang="ts">
import AppTodoItem from '@/components/AppTodoItem.vue'
import type { Todo } from '@/types/Todo.ts'

defineProps<{
  todos: Todo[]
}>()

const emit = defineEmits<{
  (event: 'toggle-todo', id: number): void
  (event: 'remove-todo', id: number): void
}>()

const toggleTodo = (id: number) => {
  emit('toggle-todo', id)
}

const removeTodo = (id: number) => {
  emit('remove-todo', id)
}
</script>

<template>
  <ul class="todo-list">
    <AppTodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggleTodo="toggleTodo"
      @removeTodo="removeTodo"
    />
  </ul>
</template>

<style scoped></style>
