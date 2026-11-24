<script setup lang="ts">
import type { Todo } from '../types/todo'

defineProps<{ todo: Todo }>()

const emit = defineEmits<{
  toggle: [id: number]
  delete: [id: number]
}>()
</script>

<template>
  <li class="todo-item">
    <input
      type="checkbox"
      :checked="todo.done"
      @change="emit('toggle', todo.id)"
    />
    <span :class="{ done: todo.done }">{{ todo.text }}</span>
    <button type="button" @click="emit('delete', todo.id)">Delete</button>
  </li>
</template>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 1rem;
  margin-bottom: 0.5rem;
  border: 1px solid var(--border);
  border-radius: 8px;
  background: var(--bg);
  transition: background-color 0.2s, border-color 0.2s, box-shadow 0.2s;
}

.todo-item:hover {
  background: var(--accent-bg);
  border-color: var(--accent-border);
  box-shadow: var(--shadow);
}

.todo-item input[type='checkbox'] {
  width: 1.1rem;
  height: 1.1rem;
  accent-color: var(--accent);
}

.todo-item span {
  flex: 1;
  text-align: left;
  color: var(--text-h);
}

.todo-item .done {
  text-decoration: line-through;
  opacity: 0.6;
}

.todo-item button {
  border: none;
  background: transparent;
  color: var(--text);
  cursor: pointer;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  transition: background-color 0.2s, color 0.2s;
}

.todo-item button:hover {
  background: var(--accent-bg);
  color: var(--accent);
}
</style>
