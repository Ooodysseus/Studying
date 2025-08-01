# Vue 3 (Vue.js): сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке Vue 3](#що-таке-vue-3)
-   [Історія та роль Vue](#історія-та-роль-vue)
-   [Встановлення та старт проекту](#встановлення-та-старт-проекту)
-   [Основи синтаксису](#основи-синтаксису)
-   [Структура компоненту](#структура-компоненту)
-   [Реактивність: ref, reactive, computed, watch](#реактивність-ref-reactive-computed-watch)
-   [Життєвий цикл компоненту](#життєвий-цикл-компоненту)
-   [Props, emits, slots](#props-emits-slots)
-   [Композиційний API vs Опціональний API](#композиційний-api-vs-опціональний-api)
-   [Роутінг (Vue Router)](#роутінг-vue-router)
-   [Стан додатку (Pinia)](#стан-додатку-pinia)
-   [Взаємодія з сервером (Fetch, Axios)](#взаємодія-з-сервером-fetch-axios)
-   [Формування шаблонів та рендеринг](#формування-шаблонів-та-рендеринг)
-   [Директиви (v-if, v-for, v-model, v-bind, v-on)](#директиви-v-if-v-for-v-model-v-bind-v-on)
-   [Компоненти та реюзабельність](#компоненти-та-реюзабельність)
-   [Слоти, Provide/Inject, Teleport](#слоти-provideinject-teleport)
-   [Composition API: поглиблений розбір](#composition-api-поглиблений-розбір)
-   [Внутрішні механізми: реактивність, virtual DOM, performance traps](#внутрішні-механізми-реактивність-virtual-dom-performance-traps)
-   [TypeScript у Vue 3](#typescript-у-vue-3)
-   [Тестування (Vitest, Cypress)](#тестування-vitest-cypress)
-   [Безпека та типові пастки](#безпека-та-типові-пастки)
-   [Best practices](#best-practices)
-   [Корисні ресурси та документація](#корисні-ресурси-та-документація)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**Vue 3 (Vue.js)** — сучасний прогресивний JavaScript-фреймворк для створення UI, SPA та складних фронтенд-додатків.  
Відрізняється легкістю, швидкістю, гнучкістю, чудовою інтеграцією з TypeScript і потужним Composition API.  
У 2024+ році Vue 3 — вибір для scalable, reactive, testable front-end проектів будь-якого рівня складності.

---

## Що таке Vue 3

Vue 3 — це open source JavaScript-фреймворк для побудови інтерфейсів, SPA, PWA та великих enterprise-додатків.

-   **Реактивність (reactivity)** — автоматичне оновлення UI при зміні стану.
-   **Компонентна архітектура** — UI розбивається на незалежні частини.
-   **Composition API** — гнучкість, реюзабельність логіки, чудова інтеграція з TypeScript.

---

## Історія та роль Vue

-   **2014:** Старт Vue.js (Evan You).
-   **2017:** Vue 2 — масова популярність серед розробників.
-   **2020+:** Vue 3 — революція: Composition API, Teleport, Suspense, покращена продуктивність.
-   **2024+:** Vue 3 — вибір для стартапів, enterprise, мобільних та desktop UI (Electron, Tauri).

---

## Встановлення та старт проекту

### Через CLI

```bash
npm create vue@latest
# Або
pnpm create vue@latest
```

### Через Vite (рекомендовано)

```bash
npm create vite@latest my-vue-app -- --template vue
cd my-vue-app
npm install
npm run dev
```

---

## Основи синтаксису

### Створення простого компоненту

```vue
<template>
    <h1>Вітаємо у Vue 3!</h1>
</template>

<script setup>
const message = "Це компонент з Composition API";
</script>

<style scoped>
h1 {
    color: #42b983;
}
</style>
```

---

## Структура компоненту

```vue
<template>
    <div>
        <h2>{{ title }}</h2>
        <button @click="increment">Додати</button>
        <p>Лічильник: {{ count }}</p>
    </div>
</template>

<script setup>
import { ref } from "vue";

const title = "Demo Компонент";
const count = ref(0);

function increment() {
    count.value++;
}
</script>

<style scoped>
/* Стилі тільки для цього компоненту */
</style>
```

---

## Реактивність: ref, reactive, computed, watch

### ref

```js
import { ref } from "vue";
const count = ref(0);
count.value++; // реактивно
```

### reactive

```js
import { reactive } from "vue";
const state = reactive({ clicks: 0, isActive: true });
state.clicks++;
```

### computed

```js
import { computed } from "vue";
const double = computed(() => count.value * 2);
```

### watch

```js
import { watch } from "vue";
watch(count, (newVal, oldVal) => {
    console.log("Лічильник змінився:", newVal);
});
```

---

## Життєвий цикл компоненту

-   `onMounted` — компонент змонтовано
-   `onUpdated` — оновлено
-   `onUnmounted` — демонтовано

```js
import { onMounted, onUnmounted } from "vue";

onMounted(() => {
    console.log("Компонент змонтовано!");
});
onUnmounted(() => {
    console.log("Компонент демонтовано!");
});
```

---

## Props, emits, slots

### Props

```vue
<script setup>
defineProps<{ title: string; count?: number }>();
</script>
```

### Emits

```vue
<script setup>
const emit = defineEmits<['increment']>();
function handleClick() {
  emit('increment');
}
</script>
```

### Slots

```vue
<template>
    <slot name="header"></slot>
    <slot></slot>
</template>
```

---

## Композиційний API vs Опціональний API

-   **Composition API** — сучасний підхід (реактивність, логіка в функціях, TypeScript-friendly).
-   **Options API** — класичний стиль (data, methods, computed, watch).

#### Приклад Options API

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
};
```

#### Приклад Composition API

```js
<script setup>
import { ref } from 'vue';
const count = ref(0);
function increment() {
  count.value++;
}
</script>
```

---

## Роутінг (Vue Router)

### Встановлення

```bash
npm install vue-router@4
```

### Основи налаштування

```js
import { createRouter, createWebHistory } from "vue-router";
import Home from "./views/Home.vue";
import About from "./views/About.vue";

const routes = [
    { path: "/", component: Home },
    { path: "/about", component: About },
];
const router = createRouter({
    history: createWebHistory(),
    routes,
});
export default router;
```

### Використання у додатку

```js
import { createApp } from "vue";
import App from "./App.vue";
import router from "./router";

createApp(App).use(router).mount("#app");
```

---

## Стан додатку (Pinia)

### Встановлення

```bash
npm install pinia
```

### Створення store

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

### Використання в компоненті

```js
import { useCounterStore } from "@/stores/counter";
const counter = useCounterStore();
counter.increment();
```

---

## Взаємодія з сервером (Fetch, Axios)

### Fetch API

```js
async function getUsers() {
    const res = await fetch("/api/users");
    const data = await res.json();
    return data;
}
```

### Axios

```js
import axios from "axios";
const users = await axios.get("/api/users");
```

---

## Формування шаблонів та рендеринг

-   **v-bind:** підв'язка атрибутів
-   **v-on:** обробка подій
-   **v-model:** двостороння прив'язка
-   **v-if/v-else/v-show:** умовний рендеринг
-   **v-for:** цикли

#### Приклад

```vue
<template>
    <input v-model="name" placeholder="Введіть ім’я" />
    <button @click="greet">Привітати</button>
    <p v-if="name">Вітаю, {{ name }}!</p>
</template>

<script setup>
import { ref } from "vue";
const name = ref("");
function greet() {
    alert(`Вітаю, ${name.value}!`);
}
</script>
```

---

## Директиви (v-if, v-for, v-model, v-bind, v-on)

-   **v-if / v-else / v-else-if:** умовний рендеринг
-   **v-for:** ітерування по масиву/об'єкту
-   **v-model:** двосторонній data binding
-   **v-bind:** підв’язка атрибутів
-   **v-on:** обробка подій

#### Приклад v-for

```vue
<template>
    <ul>
        <li v-for="user in users" :key="user.id">{{ user.name }}</li>
    </ul>
</template>

<script setup>
const users = [
    { id: 1, name: "Олег" },
    { id: 2, name: "Олена" },
];
</script>
```

---

## Компоненти та реюзабельність

-   Розбивай UI на маленькі незалежні компоненти.
-   Використовуй props, emits, slots для гнучкості.
-   Пиши компоненти як функції (script setup) для реюзабельності.

#### Приклад реюзабельного компоненту

```vue
<!-- Button.vue -->
<template>
    <button @click="onClick"><slot /></button>
</template>
<script setup>
const emit = defineEmits(["click"]);
function onClick() {
    emit("click");
}
</script>
```

---

## Слоти, Provide/Inject, Teleport

### Слоти

Дозволяють вставляти довільний контент у компонент.

```vue
<template>
    <slot name="header"></slot>
    <main><slot /></main>
    <slot name="footer"></slot>
</template>
```

### Provide/Inject

Глобальний обмін станом між компонентами.

```js
// Parent
import { provide } from "vue";
provide("theme", "dark");

// Child
import { inject } from "vue";
const theme = inject("theme");
```

### Teleport

Рендеринг у довільне місце DOM.

```vue
<teleport to="body">
  <div class="modal">Модалка</div>
</teleport>
```

---

## Composition API: поглиблений розбір

-   **ref, reactive** — створення реактивних змінних і об'єктів.
-   **computed** — реактивні вирази.
-   **watch, watchEffect** — слідкування за змінами.
-   **provide/inject** — глобальний state management.
-   **custom composables** — функції для реюзабельної логіки.

#### Приклад custom composable

```js
// useCounter.js
import { ref } from "vue";
export function useCounter() {
    const count = ref(0);
    function increment() {
        count.value++;
    }
    return { count, increment };
}
```

---

## Внутрішні механізми: реактивність, virtual DOM, performance traps

### Реактивність

-   Vue 3 використовує Proxy для реактивності.
-   Зміна стану автоматично оновлює всі залежні компоненти.

#### Схема

```
Proxy(state) <--> Dependency tracking <--> Render Queue <--> Virtual DOM <--> Real DOM
```

### Virtual DOM

-   Швидкий diff та patch для оновлення тільки потрібних частин DOM.

### Performance traps

-   **Великі компоненти** — розбивай на менші.
-   **Непотрібні watch** — оптимізуй залежності.
-   **Погана структура state** — уникай deeply nested reactive objects.

#### Діаграма реактивності

```
state (Proxy/Ref) --[dependents]--> computed, watcher --[update]--> template
```

---

## TypeScript у Vue 3

-   Повна підтримка TypeScript.
-   Композиційний API максимально TypeScript-friendly.

#### Приклад типізації пропсів

```vue
<script setup lang="ts">
defineProps<{ title: string; count?: number }>();
</script>
```

#### Типізація emit

```vue
<script setup lang="ts">
const emit = defineEmits<{
    (e: "increment", value: number): void;
}>();
</script>
```

---

## Тестування (Vitest, Cypress)

### Vitest (unit-тести)

```bash
npm install -D vitest @testing-library/vue
```

#### Приклад тесту

```js
import { render, fireEvent } from "@testing-library/vue";
import Counter from "./Counter.vue";

test("лічильник інкрементується", async () => {
    const { getByText } = render(Counter);
    await fireEvent.click(getByText("Додати"));
    getByText("Лічильник: 1");
});
```

### Cypress (E2E-тести)

```bash
npm install -D cypress
```

#### Приклад тесту

```js
describe("Counter", () => {
    it("лічильник працює", () => {
        cy.visit("/");
        cy.get("button").click();
        cy.contains("Лічильник: 1");
    });
});
```

---

## Безпека та типові пастки

-   **Використовуйте v-html обережно** — ризик XSS-атак.
-   **Не зберігайте sensitive data у реактивному state.**
-   **Валідуйте дані на сервері!**
-   **Уникайте глобальних змінних.**
-   **Завжди використовуйте :key для v-for.**

---

## Best practices

-   Використовуй Composition API, script setup, TypeScript.
-   Розбивай UI на малі компоненти.
-   Завжди додавай :key для v-for.
-   Використовуй Pinia для глобального state.
-   Валідуй дані з форм на сервері і клієнті.
-   Тестуй компоненти (unit, E2E).
-   Дотримуйся accessibility (aria-атрибути, семантика).
-   Не використовуй v-html для неперевірених даних.
-   Пиши документацію для composables та компонентів.
-   Використовуй офіційний eslint-plugin-vue для лінтингу.

---

## Корисні ресурси та документація

-   [Vue 3 Docs](https://vuejs.org/)
-   [Pinia Docs](https://pinia.vuejs.org/)
-   [Vue Router Docs](https://router.vuejs.org/)
-   [Vitest Docs](https://vitest.dev/)
-   [Testing Library Vue](https://testing-library.com/docs/vue-testing-library/intro/)
-   [Cypress Docs](https://docs.cypress.io/)
-   [VueUse (composables)](https://vueuse.org/)
-   [Vue DevTools](https://devtools.vuejs.org/)
-   [Awesome Vue](https://github.com/vuejs/awesome-vue)

---

## Короткий підсумок

**Vue 3 — це сучасний, реактивний, TypeScript-дружній фреймворк для scalable front-end проектів.**  
Гнучка компонентна архітектура, потужний Composition API, state management через Pinia, тестування через Vitest/Cypress — усе це дозволяє створювати швидкі, безпечні та професійні UI.  
Дотримуйся best practices, валідуй код, тестуй і використовуй офіційну документацію для глибокого занурення!

---
