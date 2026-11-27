# x-finance-frontend

Vue 3 frontend for X Finance, built with TypeScript and Vite.

## Tech stack

- [Vue 3](https://vuejs.org/) with `<script setup>` single-file components
- [TypeScript](https://www.typescriptlang.org/)
- [Vite](https://vite.dev/)
- [Vue Router](https://router.vuejs.org/)
- [Pinia](https://pinia.vuejs.org/)
- [Element Plus](https://element-plus.org/)
- [Axios](https://axios-http.com/)

## Requirements

- Node.js `^20.19.0` or `>=22.12.0`
- npm

## Getting started

```bash
npm install
npm run dev
```

The dev server prints a local URL. Open it in a browser. Edits under `src/` reload automatically.

## Scripts

| Command           | Description                                          |
| ----------------- | ---------------------------------------------------- |
| `npm run dev`     | Start the Vite development server                    |
| `npm run build`   | Type-check with `vue-tsc`, then build for production |
| `npm run preview` | Serve the production build locally                   |

Production files are written to `dist/`.

## Project structure

```
src/
├── assets/styles/       # Global styles and design tokens
├── components/          # common/ and layout/
├── layouts/
├── pages/               # Route pages
├── router/index.ts
├── stores/
├── services/api.ts      # Axios instance
├── types/
├── App.vue
└── main.ts
```

## Environment variables

Copy `.env.example` to `.env`. `VITE_API_BASE_URL` is the Axios base URL. Vite only exposes variables prefixed with `VITE_` to client code. `.env` is gitignored.

## Editor setup

VS Code and Cursor should use the [Vue - Official](https://marketplace.visualstudio.com/items?itemName=Vue.volar) extension (`Vue.volar`), which is listed in `.vscode/extensions.json`.
