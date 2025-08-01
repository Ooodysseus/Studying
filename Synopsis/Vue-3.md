# Ultimate Vue 3 Cheat Sheet

## ⭐ Description

Vue 3 is a modern JavaScript framework for building reactive web interfaces and single-page applications. It features the Composition API, improved performance, and TypeScript support.

## ⭐ Relationship With Other Technologies

-   **HTML:** Vue templates are written in HTML syntax with special directives.
-   **CSS/SCSS:** Scoped or global styles for components.
-   **JS/TS:** Vue logic written in JS or TS.
-   **Nuxt, Angular:** Competing frameworks; Nuxt built on Vue.
-   **Node/Express:** Vue apps often consume APIs served by Node/Express.
-   **Electron:** Vue can build desktop apps via Electron.

---

## 1. Project Structure

```
src/
  components/
  views/
  assets/
  App.vue
  main.js / main.ts
  router/
  store/
  composables/
```

-   Single File Components (SFC): `.vue` files contain `<template>`, `<script>`, `<style>`

---

## 2. Single File Component (SFC)

```vue
<template>
    <div>
        <h1>{{ title }}</h1>
        <button @click="increment">Click me</button>
        <p>Count: {{ count }}</p>
    </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
const title = ref("Hello Vue 3");
const count = ref(0);
function increment() {
    count.value++;
}
</script>

<style scoped>
h1 {
    color: #42b983;
}
</style>
```

---

## 3. Composition API

-   Reactive References: `ref`, `reactive`
-   Lifecycle Hooks: `onMounted`, `onUnmounted`, `onUpdated`, `onBeforeMount`, etc.
-   Computed Properties: `computed`
-   Watchers: `watch`, `watchEffect`
-   Provide/Inject: Dependency injection for components.

```js
import { ref, computed, watch, onMounted } from "vue";
const count = ref(0);
const double = computed(() => count.value * 2);
watch(count, (newVal) => {
    console.log(newVal);
});
onMounted(() => {
    console.log("Mounted!");
});
```

---

## 4. Options API (Classic)

```js
export default {
    data() {
        return { count: 0 };
    },
    methods: {
        increment() {
            this.count++;
        },
    },
    computed: {
        double() {
            return this.count * 2;
        },
    },
    watch: {
        count(val) {
            console.log(val);
        },
    },
    mounted() {
        console.log("Mounted!");
    },
};
```

---

## 5. Directives

-   `v-bind`: Bind attribute
-   `v-model`: Two-way binding
-   `v-if`, `v-else`, `v-else-if`: Conditional rendering
-   `v-for`: List rendering
-   `v-on`: Event binding (shorthand: `@`)
-   `v-show`: Toggle visibility
-   `v-slot`: Scoped slots
-   `v-pre`, `v-cloak`, `v-once`: Miscellaneous

```vue
<input v-model="value" :disabled="isDisabled">
<ul>
  <li v-for="item in items" :key="item.id">{{ item.text }}</li>
</ul>
<button @click="doSomething">Click</button>
```

---

## 6. Routing (Vue Router 4)

```js
import { createRouter, createWebHistory } from "vue-router";
const routes = [
    { path: "/", component: Home },
    { path: "/about", component: About },
];
const router = createRouter({
    history: createWebHistory(),
    routes,
});
```

-   Usage: `<router-link to="/">Home</router-link>`, `<router-view />`

---

## 7. State Management (Pinia)

```js
import { defineStore } from "pinia";
export const useCounterStore = defineStore("counter", {
    state: () => ({ count: 0 }),
    actions: {
        increment() {
            this.count++;
        },
    },
});
```

-   Replace Vuex in Vue 3.

---

## 8. Props, Emits, Slots

-   **Props:** Pass data from parent to child.
-   **Emits:** Trigger events from child to parent.
-   **Slots:** Distribute content from parent to child.

```vue
<MyButton :label="btnLabel" @click="handleClick">
  <template #icon> <Icon /> </template>
</MyButton>
```

---

## 9. Teleport, Suspense, Fragment

-   `<teleport to="body">`: Move content outside parent DOM.
-   `<Suspense>`: Async component loading.
-   Fragments: Multiple root nodes in template.

---

## 10. Typescript Support

-   Use `<script setup lang="ts">`
-   Full type inference for props, emits, refs.

---

## 11. Testing & Tooling

-   Unit: [Vitest](https://vitest.dev/)
-   E2E: [Cypress](https://www.cypress.io/)
-   Linting: [eslint-plugin-vue](https://eslint.vuejs.org/)
-   Formatting: [Prettier](https://prettier.io/)

---

## 12. Ecosystem

-   [Vue Router](https://router.vuejs.org/)
-   [Pinia](https://pinia.vuejs.org/)
-   [VueUse](https://vueuse.org/)
-   [Vite](https://vitejs.dev/) (recommended bundler)
-   [Vuetify, Element Plus, Quasar] (UI kits)

---

## 13. Best Practices

-   Use Composition API for scalable apps.
-   Use `scoped` styles in SFCs.
-   Use keys with `v-for`.
-   Avoid mutating props directly.
-   Prefer Pinia for state management.
-   Type everything with TypeScript.

---

## 14. Resources

-   [Vue 3 Docs](https://vuejs.org/)
-   [Awesome Vue](https://github.com/vuejs/awesome-vue)
-   [Vue Mastery](https://www.vuemastery.com/)

---

## 15. Interoperability Table

| Feature     | Vue 3 | HTML | CSS/SCSS | JS/TS | Nuxt | Angular | Node/Express | Electron |
| ----------- | ----- | ---- | -------- | ----- | ---- | ------- | ------------ | -------- |
| Templates   | ✔️    | ✔️   | ✔️       | ✔️    | ✔️   | ✔️      |              | ✔️       |
| State Mgmt  | ✔️    |      |          | ✔️    | ✔️   | ✔️      |              | ✔️       |
| Routing     | ✔️    |      |          | ✔️    | ✔️   | ✔️      |              | ✔️       |
| API Consume | ✔️    |      |          | ✔️    | ✔️   | ✔️      | ✔️           | ✔️       |
| Desktop     | ✔️    |      |          | ✔️    |      |         |              | ✔️       |
