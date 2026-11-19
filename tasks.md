# tasks.md

- [ ] Define `Todo` type (`id`, `text`, `done`) in `src/types/todo.ts`
- [ ] Create `TodoItem.vue` component with typed props via `defineProps<{ todo: Todo }>` and emit for toggle/delete
- [ ] Add `todos` ref and load from `localStorage` on mount in `App.vue`
- [ ] Implement `addTodo(text)` with ref<Todo[]> typing that appends a new todo and persists
- [ ] Implement `deleteTodo(id)` that filters and persists
- [ ] Implement `toggleTodo(id)` using computed-derived remaining count
- [ ] Bind input + button to `addTodo` in template
- [ ] Render list with `v-for` and `:key`, wire toggle/delete events
- [ ] Persist todos to `localStorage` on change (watcher)
- [ ] Style todo items with scoped CSS (padding, border, hover)
- [ ] Run `npm run build` (typecheck + build) and fix errors
- [ ] Test by adding 3 todos, checking rendering and localStorage