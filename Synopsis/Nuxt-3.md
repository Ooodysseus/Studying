# Ultimate Nuxt 3 Cheat Sheet

## ⭐ Description

Nuxt 3 is a powerful framework built on Vue 3, designed for server-side rendering (SSR), static site generation (SSG), and fullstack applications. It provides routing, data fetching, module ecosystem, and improved developer experience.

## ⭐ Relationship With Other Technologies

-   **Vue 3:** Nuxt is built on Vue—uses Vue for UI.
-   **HTML/CSS/SCSS:** Nuxt components use HTML templates and style with CSS/SCSS.
-   **JS/TS:** Logic and API written in JS/TS.
-   **Node/Express:** Nuxt runs on Node and can integrate with Express APIs.
-   **Angular:** Similar goals, different architecture.
-   **Electron:** Nuxt can be used for desktop apps with Electron.

---

## 1. Project Structure

```
app/
  components/
  layouts/
  pages/
  assets/
  middleware/
  plugins/
  composables/
nuxt.config.ts
```

-   **Pages:** Automatic routing via files in `pages/`
-   **Layouts:** Define page shells
-   **Plugins:** Register code before app start
-   **Composables:** Reusable logic, e.g., `useFetch`

---

## 2. Page & Layout Example

```vue
<!-- pages/index.vue -->
<template>
    <div>
        <h1>Welcome to Nuxt 3</h1>
        <NuxtLink to="/about">About</NuxtLink>
    </div>
</template>
```

```vue
<!-- layouts/default.vue -->
<template>
    <header>Header</header>
    <main><slot /></main>
    <footer>Footer</footer>
</template>
```

---

## 3. Routing

-   File-based: `/pages/about.vue` → `/about`
-   Dynamic: `/pages/posts/[id].vue` → `/posts/123`
-   Nested: `/pages/posts/[id]/comments.vue`
-   `<NuxtLink>` for navigation

---

## 4. Data Fetching

### useFetch (SSR/SSG/CSR)

```js
const { data, pending, error } = await useFetch("/api/posts");
```

-   Auto SSR/CSR/SSG aware, works in setup.

### useAsyncData

```js
const { data } = await useAsyncData("posts", () => $fetch("/api/posts"));
```

-   Use for custom keys, caching.

---

## 5. API Routes

-   Place in `/server/api/hello.ts`
-   Automatic API endpoints

```ts
export default defineEventHandler(() => {
    return { message: "Hello API!" };
});
```

-   Accessible at `/api/hello`

---

## 6. State Management

-   Use [Pinia](https://pinia.vuejs.org/), integrated out of the box.

```js
// stores/counter.ts
import { defineStore } from "pinia";
export const useCounter = defineStore("counter", {
    state: () => ({ count: 0 }),
    actions: {
        increment() {
            this.count++;
        },
    },
});
```

---

## 7. Plugins

-   Register plugins in `plugins/` folder.
-   Example: `plugins/axios.ts`

```ts
import axios from "axios";
export default defineNuxtPlugin((nuxtApp) => {
    nuxtApp.provide("axios", axios);
});
// Use in components: const axios = useNuxtApp().$axios
```

---

## 8. Middleware

-   Global: `middleware/auth.ts`
-   Page/Route: `definePageMeta({ middleware: 'auth' })`

---

## 9. Nuxt Config (`nuxt.config.ts`)

```ts
export default defineNuxtConfig({
    ssr: true,
    modules: ["@nuxtjs/tailwindcss"],
    runtimeConfig: {
        public: { apiBase: "/api" },
        private: { secretKey: "123" },
    },
    app: { head: { title: "Nuxt App" } },
});
```

---

## 10. Styling

-   Use `<style scoped>` in components.
-   Supports CSS, SCSS, Tailwind, etc.

---

## 11. TypeScript Support

-   Nuxt 3 is written in TS; full type inference.
-   Use `lang="ts"` in `<script setup>`

---

## 12. Modules Ecosystem

-   [@nuxt/content](https://content.nuxtjs.org/) for Markdown/Blog
-   [@nuxt/image](https://image.nuxtjs.org/) for images
-   [@nuxt/auth](https://auth.nuxtjs.org/) for authentication
-   [@nuxtjs/tailwindcss](https://tailwindcss.nuxtjs.org/)

---

## 13. Deployment

-   Supports Vercel, Netlify, Cloudflare, DigitalOcean, custom Node servers.
-   `npx nuxi build` for static export.
-   SSR for dynamic sites.

---

## 14. Testing & Tooling

-   Unit/E2E: [Vitest](https://vitest.dev/), [Cypress](https://www.cypress.io/)
-   Linting: [eslint-plugin-vue](https://eslint.vuejs.org/)
-   Formatting: [Prettier](https://prettier.io/)

---

## 15. Best Practices

-   Use `useFetch` for SSR-aware data.
-   Organize composables for reusable logic.
-   Use Pinia for state management.
-   Use modules for ecosystem features.
-   Prefer `<script setup>` for simplicity.

---

## 16. Resources

-   [Nuxt 3 Docs](https://nuxt.com/docs)
-   [Nuxt Awesome](https://github.com/nuxt/awesome-nuxt)
-   [Nuxt Discord](https://discord.com/invite/nuxt)

---

## 17. Interoperability Table

| Feature     | Nuxt 3 | Vue 3 | HTML | CSS/SCSS | JS/TS | Angular | Node/Express | Electron |
| ----------- | ------ | ----- | ---- | -------- | ----- | ------- | ------------ | -------- |
| SSR/SSG     | ✔️     |       |      |          |       |         | ✔️           |          |
| Routing     | ✔️     | ✔️    |      |          | ✔️    | ✔️      |              |          |
| API Consume | ✔️     | ✔️    |      |          | ✔️    | ✔️      | ✔️           | ✔️       |
| Desktop     | ✔️     | ✔️    |      |          | ✔️    |         |              | ✔️       |
