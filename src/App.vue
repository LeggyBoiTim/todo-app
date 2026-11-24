<script setup lang="ts">
import { ref, onMounted, computed, watch } from 'vue'
import type { Todo } from './types/todo'
import TodoItem from './components/TodoItem.vue'

const todos = ref<Todo[]>([])

const remainingCount = computed(() => todos.value.filter((todo) => !todo.done).length)

watch(
  todos,
  (value) => {
    localStorage.setItem('todos', JSON.stringify(value))
  },
  { deep: true }
)

const newText = ref('')
const inputRef = ref<HTMLInputElement | null>(null)

function handleAdd() {
  const text = newText.value.trim()
  if (!text) return
  addTodo(text)
  newText.value = ''
  inputRef.value?.focus()
}

function addTodo(text: string) {
  const nextId = Math.max(0, ...todos.value.map((todo) => todo.id)) + 1
  todos.value.push({ id: nextId, text, done: false })
  localStorage.setItem('todos', JSON.stringify(todos.value))
}

function deleteTodo(id: number) {
  todos.value = todos.value.filter((todo) => todo.id !== id)
  localStorage.setItem('todos', JSON.stringify(todos.value))
}

function toggleTodo(id: number) {
  const todo = todos.value.find((item) => item.id === id)
  if (todo) {
    todo.done = !todo.done
    localStorage.setItem('todos', JSON.stringify(todos.value))
  }
}

onMounted(() => {
  const stored = localStorage.getItem('todos')
  if (stored) {
    try {
      const parsed = JSON.parse(stored) as Todo[]
      if (Array.isArray(parsed)) {
        todos.value = parsed
      }
    } catch {
      // ignore malformed stored data
    }
  }
})
</script>

<template>
  <main>
    <h1>Todos</h1>
    <div class="add">
      <input
  ref="inputRef"
  v-model="newText"
  type="text"
  placeholder="New todo"
  @keyup.enter="handleAdd"
/>
      <button type="button" @click="handleAdd">Add</button>
    </div>
    <p class="remaining">{{ remainingCount }} remaining</p>
    <ul class="todo-list">
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @toggle="toggleTodo"
        @delete="deleteTodo"
      />
    </ul>
  </main>
</template>

<style scoped>
main {
  max-width: 640px;
  margin: 0 auto;
  padding: 2rem 1.5rem;
}

h1 {
  font-size: 2rem;
  margin: 0 0 1.5rem;
  text-align: left;
}

.add {
  display: flex;
  gap: 0.75rem;
  margin-bottom: 1.25rem;
}

.add input {
  flex: 1;
  padding: 0.6rem 0.8rem;
  border: 1px solid var(--border);
  border-radius: 8px;
  font-size: 1rem;
  color: var(--text-h);
  background: var(--bg);
}

.add input:focus {
  outline: 2px solid var(--accent);
  outline-offset: 1px;
}

.add button {
  padding: 0.6rem 1.2rem;
  border: none;
  border-radius: 8px;
  background: var(--accent);
  color: #fff;
  font-size: 1rem;
  cursor: pointer;
  transition: opacity 0.2s;
}

.add button:hover {
  opacity: 0.9;
}

.remaining {
  margin: 0 0 1rem;
  font-weight: 600;
  color: var(--text);
  text-align: left;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
