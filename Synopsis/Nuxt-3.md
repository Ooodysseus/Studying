# Nux 3 (Nuxt.js 3): сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке Nux 3 (Nuxt.js 3)](#що-таке-nux-3-nuxtjs-3)
-   [Історія та роль Nuxt.js](#історія-та-роль-nuxtjs)
-   [Встановлення та старт проекту](#встановлення-та-старт-проекту)
-   [Основи структури проекту](#основи-структури-проекту)
-   [Сторінки (Pages), роутінг та навігація](#сторінки-pages-роутінг-та-навігація)
-   [Компоненти (Components) та реюзабельність](#компоненти-components-та-реюзабельність)
-   [Реактивність, Composition API, Pinia](#реактивність-composition-api-pinia)
-   [Форми, валідація, робота з даними](#форми-валідація-робота-з-даними)
-   [Асинхронність, Fetch API, useAsyncData, useFetch](#асинхронність-fetch-api-useasyncdata-usefetch)
-   [SEO, Meta, Open Graph, Sitemap](#seo-meta-open-graph-sitemap)
-   [Внутрішні механізми: SSR, SSG, ISR, Middleware, Routing, Performance traps](#внутрішні-механізми-ssr-ssg-isr-middleware-routing-performance-traps)
-   [TypeScript у Nux 3](#typescript-у-nux-3)
-   [Тестування (Vitest, Cypress)](#тестування-vitest-cypress)
-   [Безпека та типові підводні камені](#безпека-та-типові-підводні-камені)
-   [Best practices](#best-practices)
-   [Deep Dive: SSR/SSG, SEO, Security](#deep-dive-ssr-ssg-seo-security)
-   [Корисні ресурси та документація](#корисні-ресурси-та-документація)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**Nux 3 (Nuxt.js 3)** — це сучасний, прогресивний фреймворк на базі Vue 3 для створення швидких, масштабованих, SEO-friendly web-додатків із підтримкою SSR (Server-Side Rendering), SSG (Static Site Generation), ISR (Incremental Static Regeneration), SPA та JAMstack.  
У 2024 році Nux 3 — стандарт для enterprise, e-commerce, SaaS, стартапів та корпоративних проектів, що потребують гнучкість, продуктивність і безпеку.

---

## Що таке Nux 3 (Nuxt.js 3)

Nuxt.js 3 — фреймворк на основі Vue 3 та Vite, який дає:

-   **SSR, SSG, SPA** — різні режими рендерингу.
-   **Zero-config** — автоматичне налаштування.
-   **File-based routing** — структура сторінок через директорії.
-   **TypeScript** — інтеграція з TS "з коробки".
-   **Модульна система** — розширення через офіційні та сторонні модулі.
-   **Performance** — оптимізований build, lazy loading, island architecture.
-   **SEO** — автоматичне управління мета-тегами.

---

## Історія та роль Nuxt.js

-   **2016:** Старт Nuxt.js (Atinux, Poilblanc).
-   **2018:** Nuxt 2 — популярність серед Vue-розробників.
-   **2022+:** Nuxt 3 — новий ядро на Vue 3, Vite, Composition API, TypeScript.
-   **2024+:** Nuxt 3 — вибір для JAMstack, SSR/SSG, e-commerce, SaaS, документування, блогів, enterprise UI.

---

## Встановлення та старт проекту

### Через CLI

```bash
npx nuxi@latest init my-nuxt-app
cd my-nuxt-app
npm install
npm run dev
```

### Через pnpm

```bash
pnpm create nuxt-app my-nuxt-app
pnpm install
pnpm dev
```

---

## Основи структури проекту

```
my-nuxt-app/
├─ app.vue             # Головний layout
├─ nuxt.config.ts      # Головний конфіг Nuxt
├─ pages/              # Сторінки (routing)
├─ components/         # Глобальні/локальні компоненти
├─ layouts/            # Layout-и для сторінок
├─ composables/        # Custom логіка (composition API)
├─ stores/             # Pinia stores
├─ public/             # Статичні файли
├─ assets/             # Стилі, зображення
├─ middleware/         # Middleware для роутів
├─ tests/              # Тестування
└─ types/              # Типи (TypeScript)
```

---

## Сторінки (Pages), роутінг та навігація

-   **File-based routing:** кожен файл у `pages/` — окрема сторінка.
-   **Динамічні роутинг:** `[id].vue` — динамічний параметр.
-   **Nested routing:** папки — вкладені маршрути.
-   **Навігація:** `<NuxtLink />` — сучасний router-link.

#### Приклад сторінки

```vue
<!-- pages/index.vue -->
<template>
    <h1>Головна сторінка</h1>
    <NuxtLink to="/about">Про проект</NuxtLink>
</template>
```

#### Динамічна сторінка

```vue
<!-- pages/users/[id].vue -->
<template>
    <h2>Користувач: {{ user.name }}</h2>
</template>

<script setup>
const { params } = useRoute();
const { data: user } = await useAsyncData("user", () =>
    $fetch(`/api/users/${params.id}`)
);
</script>
```

---

## Компоненти (Components) та реюзабельність

-   **Глобальні компоненти** — автоматичне імпорт через `components/`.
-   **Локальні компоненти** — імпорт у потрібному файлі.
-   **Композиція** — використання props, slots, emit.
-   **script setup** — сучасний підхід для компонентів.

#### Приклад компонента

```vue
<!-- components/MyButton.vue -->
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

#### Використання

```vue
<MyButton @click="handleClick">Натисни мене</MyButton>
```

---

## Реактивність, Composition API, Pinia

-   **ref, reactive, computed, watch** — Vue 3 реактивність.
-   **composables/** — власні хуки-логіки (useCounter, useAuth).
-   **Pinia** — сучасний state manager для Nuxt 3.

#### Приклад composable

```js
// composables/useCounter.ts
import { ref } from "vue";
export function useCounter() {
    const count = ref(0);
    function increment() {
        count.value++;
    }
    return { count, increment };
}
```

#### Використання Pinia store

```js
// stores/counter.ts
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

---

## Форми, валідація, робота з даними

-   **Використання v-model** для двосторонньої прив'язки.
-   **Валідація:** vee-validate, yup, custom logic.
-   **Робота з даними:** useFetch, useAsyncData.

#### Приклад форми

```vue
<template>
    <form @submit.prevent="submit">
        <input v-model="email" type="email" required />
        <button type="submit">Відправити</button>
        <span v-if="error">{{ error }}</span>
    </form>
</template>

<script setup>
import { ref } from "vue";
const email = ref("");
const error = ref("");

function submit() {
    if (!email.value.includes("@")) {
        error.value = "Некоректний email";
        return;
    }
    // Надсилання на сервер
}
</script>
```

---

## Асинхронність, Fetch API, useAsyncData, useFetch

-   **useFetch:** для SSR/CSR запитів.
-   **useAsyncData:** для асинхронних даних з SSR/SSG.
-   **$fetch:** Nuxt-обгортка для fetch, автоматичне проксі API.

#### Приклад useFetch

```vue
<script setup>
const { data, pending, error } = await useFetch("/api/products");
</script>
```

#### Приклад useAsyncData

```vue
<script setup>
const { data: posts } = await useAsyncData("posts", () => $fetch("/api/posts"));
</script>
```

---

## SEO, Meta, Open Graph, Sitemap

-   **useHead:** для управління мета-тегами.
-   **Nuxt SEO module:** автоматизація sitemap, robots.txt.
-   **Open Graph, Twitter Card:** підтримка соцмереж.

#### Приклад useHead

```js
import { useHead } from "@nuxtjs/composition-api";
useHead({
    title: "Головна Nux 3",
    meta: [
        { name: "description", content: "Сучасний Nuxt 3 конспект" },
        { property: "og:title", content: "Nux 3" },
    ],
});
```

#### Sitemap

-   Встанови [nuxt-simple-sitemap](https://nuxt.com/modules/sitemap).

---

## Внутрішні механізми: SSR, SSG, ISR, Middleware, Routing, Performance traps

### SSR (Server-Side Rendering)

-   Рендеринг сторінки на сервері — швидкий перший рендер, кращий SEO.

### SSG (Static Site Generation)

-   Генерація сторінок як статичних файлів на етапі build.

### ISR (Incremental Static Regeneration)

-   Оновлення окремих сторінок після деплою без повного rebuild.

### Middleware

-   Код, що виконується при кожному роуті (авторизація, валідація).

#### Приклад middleware

```js
// middleware/auth.ts
export default defineNuxtRouteMiddleware((to, from) => {
    const user = useUserStore();
    if (!user.isAuth) return navigateTo("/login");
});
```

### Routing

-   File-based, підтримка динамічних, вкладених, параметрів, guards.

### Performance traps

-   **Великі payload-и:** ленива загрузка компонентів.
-   **Велика кількість SSR-API:** кешування, оптимізація.
-   **Глибокі вкладені сторінки:** island architecture, split chunks.

#### Схема SSR/CSR

```
Client Request → Server (SSR) → HTML → Hydration (CSR) → Interactive App
```

---

## TypeScript у Nux 3

-   Повна підтримка TS у компонентах, сторінках, composables, stores.
-   type safety для props, emits, state.

#### Приклад типізації props

```vue
<script setup lang="ts">
defineProps<{ title: string; count?: number }>();
</script>
```

#### Типізація Pinia store

```ts
export const useUserStore = defineStore("user", {
    state: (): { name: string; isAuth: boolean } => ({
        name: "",
        isAuth: false,
    }),
});
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

test("лічильник працює", async () => {
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
    it("лічильник інкрементується", () => {
        cy.visit("/");
        cy.get("button").click();
        cy.contains("Лічильник: 1");
    });
});
```

---

## Безпека та типові підводні камені

-   **Використання v-html тільки для trusted data** — ризик XSS.
-   **Валідація даних на сервері і клієнті.**
-   **Правильне використання middleware для авторизації.**
-   **Уникай глобальних змінних у сторінках/компонентах.**
-   **Слідкуй за продуктивністю SSR/CSR: кешування, оптимізація запитів.**
-   **Додавай :key для v-for.**
-   **Обмежуй доступ до приватних API через серверний middleware.**

---

## Best practices

-   Використовуй Composition API, script setup, TypeScript.
-   Розбивай UI на малі компоненти, використовуйте slots для реюзабельності.
-   Всі запити — через useFetch/useAsyncData ($fetch).
-   Використовуй Pinia для глобального state.
-   Тестуй компоненти (unit, E2E).
-   Дотримуйся accessibility (aria, семантика).
-   Використовуй useHead для SEO.
-   Кешуй SSR-дані для продуктивності.
-   Оновлюй залежності до останніх версій.
-   Валідуй код через ESLint, Prettier.
-   Винось типи у окремі файли.
-   Використовуй middleware для захисту роутів.

---

## Deep Dive: SSR/SSG, SEO, Security

---

### SSR (Server-Side Rendering) та SSG (Static Site Generation) у Nuxt 3

#### Вступ та пояснення

**SSR** — рендеринг сторінки на сервері. Коли користувач заходить на сайт, сервер повертає вже готовий HTML, який швидко показується браузером.  
**SSG** — сторінки генеруються як статичні файли на етапі білду. Користувач отримує готовий HTML без звернень до серверу при кожному запиті.

#### Як працює SSR у Nuxt 3

-   Nuxt 3 використовує Vite, Nitro та Vue 3 для швидкого SSR.
-   SSR дозволяє повертати SEO-friendly HTML, швидше завантаження першого екрану ("first paint").
-   SSR автоматично гідрується на клієнті: JS підключає інтерфейс та додає інтерактивність.

##### Схема SSR

```
Користувач → Сервер Nuxt (SSR) → HTML + дані → Браузер → Hydration (CSR) → Інтерактивність
```

##### SSR Flow:

1. Користувач відкриває сторінку.
2. Сервер Nuxt отримує запит, формує HTML, додає дані через useAsyncData/useFetch.
3. Відправляє готовий HTML з даними.
4. JS-клієнт "гідрує" сторінку для подальшої взаємодії.

#### Як працює SSG

-   Nuxt 3 білдить всі сторінки заздалегідь та зберігає їх як статичні файли.
-   Ідеально для блогів, документації, лендингів.
-   Підтримка ISR (Incremental Static Regeneration): сторінки оновлюються частинами після деплою.

##### Схема SSG

```
Nuxt Build → Генерація HTML для кожної сторінки → Зберігання у /dist → CDN → Користувач
```

##### SSG Flow:

1. Nuxt білдить проект, виконує всі запити, зберігає результат.
2. Користувач звертається до статичного файлу — миттєве завантаження.

#### SSR vs SSG: коли і що обирати?

| SSR                               | SSG                               |
| --------------------------------- | --------------------------------- |
| Динамічні дані, особисті кабінети | Блог, документація, лендинги      |
| Актуальні дані на кожному запиті  | Фіксовані дані                    |
| Кращий SEO для динаміки           | Швидкість та дешеве хостингування |
| Більше серверних ресурсів         | Висока масштабованість            |

#### Best practices SSR/SSG

-   Використовуй SSR для сторінок з динамікою та персоналізацією.
-   SSG — для публічного контенту, що рідко змінюється.
-   Кешуй SSR-сторінки для продуктивності.
-   Оновлюй SSG через ISR для частково динамічного контенту.
-   Завжди тестуй сторінки на різних пристроях (first paint, hydration).

#### Корисні ресурси

-   [Nuxt 3 SSR Docs](https://nuxt.com/docs/getting-started/rendering#server-side-rendering)
-   [Nuxt 3 SSG Docs](https://nuxt.com/docs/getting-started/deployment#static-site-generation-ssg)
-   [Nitro Engine](https://nitro.unjs.io/)
-   [Incremental Static Regeneration](https://nuxt.com/blog/incremental-static-regeneration)

---

### Deep Dive SEO (Search Engine Optimization) в Nuxt 3

#### Вступ та пояснення

SEO — це комплекс дій для підвищення видимості сайту в пошукових системах. Nuxt 3, завдяки SSR/SSG, автоматично генерує "чистий" HTML, що ідеально індексується пошуковиками.

#### Механізми SEO в Nuxt 3

-   SSR/SSG — повертає повноцінний HTML для crawler-ів.
-   useHead — сучасний API для керування meta-тегами, Open Graph, Twitter Card.
-   Модулі Nuxt (SEO, sitemap) — автоматичне формування sitemap.xml, robots.txt.
-   Canonical, hreflang — для багатомовних сайтів.

#### Приклад SEO-конфігурації

```js
import { useHead } from "nuxt/app";

useHead({
    title: "Nuxt 3 Deep Dive",
    meta: [
        {
            name: "description",
            content: "Глибокий конспект Nuxt 3 з SSR, SSG, SEO, Security.",
        },
        {
            name: "keywords",
            content: "nuxt, vue, ssr, ssg, seo, security, 2024",
        },
        { property: "og:title", content: "Nuxt 3 Deep Dive" },
        {
            property: "og:description",
            content: "SSR, SSG, SEO, Security — сучасні рішення.",
        },
        { name: "twitter:card", content: "summary" },
    ],
    link: [{ rel: "canonical", href: "https://my-site.com/" }],
});
```

#### Sitemap та robots.txt

-   Встановлюй [nuxt-simple-sitemap](https://nuxt.com/modules/sitemap) для автоматичного формування sitemap.
-   robots.txt — дозволяє або забороняє індексацію певних сторінок.

#### Open Graph та Social Preview

-   Додавай OG-теги для коректного відображення при розшарюванні в соцмережах.
-   Twitter Card — для Twitter preview.

#### Accessibility & SEO

-   Використовуй семантичні елементи (main, nav, article), alt для зображень.
-   Правильна структура заголовків (`h1`, `h2`, …).
-   Валідуй HTML ([validator.w3.org](https://validator.w3.org/)).

#### Best practices SEO

-   Завжди додавай унікальні title, description для кожної сторінки.
-   Використовуй useHead для динамічних meta-тегів.
-   Додавай canonical для уникнення дублювання контенту.
-   Впроваджуй sitemap.xml для покращення індексації.
-   Тестуй SEO через Google Search Console, Lighthouse.

#### Корисні ресурси

-   [Nuxt SEO Docs](https://nuxt.com/modules/seo)
-   [Nuxt useHead](https://nuxt.com/docs/api/composables/use-head)
-   [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/seo/)
-   [Google Search Console](https://search.google.com/search-console)
-   [Open Graph Protocol](https://ogp.me/)
-   [Twitter Cards](https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/abouts-cards)

---

### Deep Dive Security (Безпека) в Nuxt 3

#### Вступ та пояснення

Безпека — фундамент сучасного вебу. Nuxt 3 забезпечує захист через middleware, SSR, server-side validation, automatized security headers та best practices.

#### Потенційні загрози

-   XSS (Cross-site Scripting) — ін'єкція коду через неперевірені дані.
-   CSRF (Cross-Site Request Forgery) — фейкові запити від імені користувача.
-   Leakage sensitive data — витік даних через неправильну архітектуру.
-   Open redirects, insecure headers, weak authentication.

#### Захист від XSS

-   Ніколи не вставляй дані напряму у v-html без санітайзу.
-   Для рендерингу довірених даних — використовуй бібліотеки типу [DOMPurify](https://github.com/cure53/DOMPurify).
-   Завжди валідуй і санітайзь дані на сервері.

```vue
<template>
    <!-- Небезпечно: вставка userInput напряму -->
    <div v-html="userInput"></div>
</template>
```

```js
// Краще: очищення через DOMPurify (на сервері або клієнті)
import DOMPurify from "dompurify";
const safeHTML = DOMPurify.sanitize(userInput);
```

#### Захист від CSRF

-   Використовуй токени CSRF для POST/PUT/DELETE-запитів.
-   Перевіряй автентичність запитів у middleware.

#### Secure Headers

-   Встановлюй security headers через серверну частину Nuxt (Nitro).
-   Content-Security-Policy, X-Frame-Options, X-XSS-Protection, Strict-Transport-Security.

```js
// nuxt.config.ts
export default defineNuxtConfig({
    nitro: {
        routeRules: {
            "/api/**": {
                headers: {
                    "X-Frame-Options": "DENY",
                    "X-XSS-Protection": "1; mode=block",
                },
            },
        },
    },
});
```

#### Middleware для авторизації

```js
// middleware/auth.ts
export default defineNuxtRouteMiddleware((to, from) => {
    const user = useUserStore();
    if (!user.isAuth) return navigateTo("/login");
});
```

#### Валідація даних

-   Всі дані з форм — перевіряй на сервері.
-   Використовуй yup, zod або власну логіку для типізації та валідації.

#### Best practices Security

-   Валідуй дані на сервері й клієнті.
-   Не використовуй v-html для неперевірених даних.
-   Впроваджуй secure headers.
-   Використовуй HTTPS для всіх запитів.
-   Обмежуй доступ через middleware.
-   Оновлюй залежності та стеж за відомими уразливостями (npm audit).
-   Використовуй [Nuxt Security Module](https://nuxt.com/modules/security) для автоматичного захисту.

#### Корисні ресурси

-   [Nuxt Security Module](https://nuxt.com/modules/security)
-   [OWASP Nuxt Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Nuxt_Security_Cheat_Sheet.html)
-   [DOMPurify](https://github.com/cure53/DOMPurify)
-   [MDN Security](https://developer.mozilla.org/en-US/docs/Web/Security)
-   [Vulnerabilities audit (npm)](https://docs.npmjs.com/cli/v10/commands/npm-audit)

---

## Корисні ресурси та документація

-   [Nuxt 3 Docs](https://nuxt.com/docs)
-   [Nuxt 3 Examples](https://github.com/nuxt/examples)
-   [Nuxt Modules Directory](https://nuxt.com/modules)
-   [Pinia Docs](https://pinia.vuejs.org/)
-   [Vitest Docs](https://vitest.dev/)
-   [Cypress Docs](https://docs.cypress.io/)
-   [Nuxt SEO Module](https://nuxt.com/modules/seo)
-   [Nuxt DevTools](https://devtools.nuxt.com/)
-   [Awesome Nuxt](https://github.com/nuxt/awesome-nuxt)
-   [Nuxt Deep Dive](https://nuxt.com/blog/deep-dive-into-nuxt3)
-   [Nuxt Security Module](https://nuxt.com/modules/security)

---

## Короткий підсумок

**Nux 3 (Nuxt.js 3) — сучасний фреймворк для швидких, SEO-friendly, scalable web-додатків на базі Vue 3 та Vite.**  
SSR, SSG, SEO, Security — ключові складові сучасної розробки.  
Дотримуйся best practices, тестуй, оптимізуй продуктивність, валідуй дані і використовуй офіційну документацію для глибокого занурення!

---
