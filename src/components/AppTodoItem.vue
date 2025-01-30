<script setup lang="ts">
import type { Todo } from '@/types/Todo.ts'

const props = defineProps<{ todo: Todo }>()

const emit = defineEmits<{
  (event: 'toggle-todo', id: number): void
  (event: 'remove-todo', id: number): void
}>()

const toggleTodo = () => {
  emit('toggle-todo', props.todo.id)
}

const removeTodo = () => {
  emit('remove-todo', props.todo.id)
}
</script>

<template>
  <li class="todo-item" :class="{ 'todo-item--done': todo.completed }" @click="toggleTodo">
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ todo.text }}</span>
    <button class="todo-item__remove-button" @click.stop="removeTodo">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>

<style scoped></style>
