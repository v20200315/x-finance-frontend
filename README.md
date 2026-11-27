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

| Command | Description |
| --- | --- |
| `npm run dev` | Start the Vite development server |
| `npm run build` | Type-check with `vue-tsc`, then build for production |
| `npm run preview` | Serve the production build locally |

Production files are written to `dist/`.

## Project structure

```
.
├── public/              # Static files served as-is
├── src/
│   ├── assets/          # Images and other imported assets
│   ├── components/      # Vue components
│   ├── App.vue          # Root component
│   ├── main.ts          # Application entry
│   └── style.css        # Global styles
├── index.html
├── vite.config.ts
└── tsconfig.json
```

## Environment variables

Local configuration belongs in `.env`. Vite only exposes variables prefixed with `VITE_` to client code. `.env` files are gitignored. A shared template named `.env.example` can be committed when the project needs one.

## Editor setup

VS Code and Cursor should use the [Vue - Official](https://marketplace.visualstudio.com/items?itemName=Vue.volar) extension (`Vue.volar`), which is listed in `.vscode/extensions.json`.
