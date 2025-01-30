<script setup lang="ts">
import type { Stats } from '@/types/Stats.ts'

defineProps<{
  stats: Stats
}>()
</script>

<template>
  <footer class="app-footer">{{ stats.active }} more to do, {{ stats.done }} done</footer>
</template>

<style scoped></style>
