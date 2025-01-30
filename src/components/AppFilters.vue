<script setup lang="ts">
import type { Filter } from '@/types/Filter.ts'

defineProps<{ activeFilter: Filter }>()

const emit = defineEmits<{
  (event: 'setFilter', filter: string): void
}>()

const filters: Filter[] = ['All', 'Active', 'Done']

const setFilter = (filter: string) => {
  emit('setFilter', filter)
}
</script>

<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        v-for="filter in filters"
        :key="filter"
        class="button"
        :class="{ 'button--primary': activeFilter === filter }"
        @click="setFilter(filter)"
      >
        {{ filter }}
      </button>
    </section>
  </aside>
</template>

<style scoped></style>
