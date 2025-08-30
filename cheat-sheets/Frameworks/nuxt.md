# NUXT.JS

Nuxt.js — фреймворк для створення серверних і статичних Vue-додатків із підтримкою SSR, SSG, роутингу, модулів, API та автоматичної організації структури проекту.

## Категорія: Основні CLI-команди

| Команда/метод     | Опис               | Приклад/Аутпут       |
| ----------------- | ------------------ | -------------------- |
| npx nuxi init app | створити проект    | npx nuxi init my-app |
| npm run dev       | запуск dev-сервера | npm run dev          |
| npm run build     | зібрати проект     | npm run build        |
| npm run generate  | статична генерація | npm run generate     |
| npm run preview   | перегляд збірки    | npm run preview      |
| nuxi add module   | додати модуль      | nuxi add tailwindcss |

## Категорія: Структура проекту

| Команда/метод  | Опис                | Приклад/Аутпут         |
| -------------- | ------------------- | ---------------------- |
| pages/         | сторінки (роутинг)  | pages/index.vue        |
| layouts/       | шаблони             | layouts/default.vue    |
| components/    | компоненти          | components/Header.vue  |
| composables/   | хуки                | composables/useAuth.ts |
| plugins/       | плагіни             | plugins/axios.ts       |
| middleware/    | проміжні            | middleware/auth.ts     |
| app.vue        | кореневий компонент | app.vue                |
| nuxt.config.ts | конфігурація        | nuxt.config.ts         |

## Категорія: Основи сторінок і роутингу

| Команда/метод             | Опис              | Приклад/Аутпут                           |
| ------------------------- | ----------------- | ---------------------------------------- |
| <NuxtPage/>               | рендер сторінки   | <NuxtPage/>                              |
| definePageMeta            | метадані сторінки | definePageMeta({layout:'custom'})        |
| useRoute(), useRouter()   | роутер/маршрут    | const route = useRoute()                 |
| navigateTo('/about')      | перехід           | navigateTo('/about')                     |
| defineNuxtRouteMiddleware | middleware        | defineNuxtRouteMiddleware((to,from)=>{}) |
| params, query             | параметри/запити  | route.params.id, route.query.page        |

## Категорія: Компоненти та стейт

| Команда/метод           | Опис               | Приклад/Аутпут                                        |
| ----------------------- | ------------------ | ----------------------------------------------------- |
| defineComponent         | створити компонент | export default defineComponent({})                    |
| defineProps/defineEmits | пропси/події       | const props = defineProps<{id:number}>()              |
| useState('key',()=>0)   | глобальний стейт   | const count = useState('count',()=>0)                 |
| useAsyncData            | асинхронні дані    | const {data} = await useAsyncData('k',()=>fetch(...)) |
| useFetch                | SSR-запит          | const {data} = await useFetch('/api')                 |
| provide/inject          | контекст           | provide('k',v); inject('k')                           |

## Категорія: API, серверні функції

| Команда/метод           | Опис               | Приклад/Аутпут                                 |
| ----------------------- | ------------------ | ---------------------------------------------- |
| server/api/             | серверні ендпоінти | server/api/user.get.ts                         |
| defineEventHandler      | обробник запиту    | export default defineEventHandler((event)=>{}) |
| useBody, useQuery       | тіло/запит         | const body = await useBody(event)              |
| sendRedirect, sendError | редірект/помилка   | sendRedirect(event,'/login')                   |

## Категорія: Модулі та плагіни

| Команда/метод    | Опис                | Приклад/Аутпут                                 |
| ---------------- | ------------------- | ---------------------------------------------- |
| modules: []      | підключення модулів | modules: ['@nuxtjs/tailwindcss']               |
| defineNuxtPlugin | створити плагін     | export default defineNuxtPlugin((nuxtApp)=>{}) |
| useRuntimeConfig | змінні оточення     | const cfg = useRuntimeConfig()                 |
| useHead          | мета-теги           | useHead({title:'Home'})                        |

## Категорія: Інше

| Команда/метод                 | Опис                | Приклад/Аутпут                         |
| ----------------------------- | ------------------- | -------------------------------------- |
| <NuxtLayout/>                 | шаблон              | <NuxtLayout name="custom"/>            |
| <NuxtLink to="/">             | посилання           | <NuxtLink to="/about">About</NuxtLink> |
| useCookie                     | куки                | const c = useCookie('token')           |
| useSeoMeta                    | SEO-мета            | useSeoMeta({title:'Home'})             |
| process.server/process.client | оточення            | if(process.server){...}                |
| $fetch                        | універсальний fetch | const d = await $fetch('/api')         |
| defineNuxtPlugin              | плагін              | export default defineNuxtPlugin(...)   |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
