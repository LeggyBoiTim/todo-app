# tasks.md

- [x] Define `Todo` type (`id`, `text`, `done`) in `src/types/todo.ts`
- [x] Create `TodoItem.vue` component with typed props via `defineProps<{ todo: Todo }>` and emit for toggle/delete
- [x] Add `todos` ref and load from `localStorage` on mount in `App.vue`
- [x] Implement `addTodo(text)` with ref<Todo[]> typing that appends a new todo and persists
- [x] Implement `deleteTodo(id)` that filters and persists
- [x] Implement `toggleTodo(id)` using computed-derived remaining count
- [x] Bind input + button to `addTodo` in template
- [x] Render list with `v-for` and `:key`, wire toggle/delete events
- [x] Persist todos to `localStorage` on change (watcher)
- [x] Style todo items with scoped CSS (padding, border, hover)
- [x] Style title, adding todos and remaining todos with scoped CSS
- [x] Run `npm run build` (typecheck + build) and fix errors
- [x] Test by adding 3 todos, checking rendering and localStorage