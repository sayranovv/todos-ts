<script setup lang="ts">
import { ref } from 'vue'
import type { Todo } from '@/types/Todo.ts'

const emit = defineEmits<{
  (event: 'addTodo', todo: Todo): void
}>()

const isFormVisible = ref<boolean>(false)
const todoText = ref<string>('')

const toggleForm = () => {
  isFormVisible.value = !isFormVisible.value
}

const addTodo = () => {
  emit('addTodo', {
    id: Date.now(),
    text: todoText.value,
    completed: false,
  })
  todoText.value = ''
}
</script>

<template>
  <section class="add-todo">
    <form v-if="isFormVisible" class="add-todo__form" @submit.prevent="addTodo">
      <button class="close-button" type="button" @click="toggleForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input class="input" v-model="todoText" />
      </div>
      <button class="button button--filled" type="submit">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="toggleForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<style scoped></style>
