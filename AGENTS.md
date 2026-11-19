# AGENTS.md

## Goal
Build a todo component: add/delete items, persisted to `localStorage`.

## Tech stack
Vue 3, TypeScript, Vite.

## Commands
- `npm run dev` — Vite dev server with HMR.
- `npm run build` — `vue-tsc -b` then `vite build` (typecheck + build).
- `npm run preview` — preview production build.

## Architecture
SFCs with `<script setup lang="ts">` and Composition API (`ref`, `computed`), scoped CSS. State lives in component; persistence via `localStorage` (read on mount, write on change).

## Key Rules
- Vue 3 best practices: `<script setup>`, typed props/emits (`defineProps<{ ... }>`), avoid mutating props. No Options API. Use `computed()` for derived state.
- TypeScript strict: `noUnusedLocals`, `noUnusedParameters`, `erasableSyntaxOnly`, `noFallthroughCasesInSwitch`. No unused imports/vars.
- Project references: `tsconfig.json` → `tsconfig.app.json` + `tsconfig.node.json`; `vue-tsc -b` builds both.
