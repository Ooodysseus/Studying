# Nuxt 3 Cheatsheet

## Install & Create Project
npx nuxi init my-app  
cd my-app  
npm install  
npm run dev  
npm run build  
npm run preview  

## Project Structure
app.vue  
nuxt.config.ts  
pages/  
components/  
layouts/  
composables/  
middleware/  
plugins/  
assets/  
public/  
store/ (Pinia)  

## Routing
pages/index.vue → /  
pages/about.vue → /about  
pages/blog/[id].vue → /blog/:id  
pages/blog/[...slug].vue → /blog/anything/here  
pages/user/[id]/settings.vue → /user/:id/settings  
<NuxtLink to="/about">About</NuxtLink>  
<NuxtPage />  
definePageMeta({ middleware: ['auth'] })  

## Layouts
layouts/default.vue  
layouts/admin.vue  
<NuxtLayout name="admin">  
<slot />  
</NuxtLayout>  
definePageMeta({ layout: 'admin' })  

## Components
components/MyButton.vue  
<template><button>Click!</button></template>  
<Script setup>defineProps()</Script>  
<template><MyButton label="OK" /></template>  

## Auto Imports
useState  
useFetch  
useAsyncData  
useHead  
computed  
ref  
watch  
defineNuxtPlugin  

## Composables
composables/useCounter.ts  
export function useCounter() { const count = ref(0); return { count } }  
const { count } = useCounter()  

## useState
const counter = useState('counter', () => 0)  
counter.value++  

## useFetch / useAsyncData
const { data, pending, error } = await useFetch('/api/items')  
const { data } = await useAsyncData('items', () => $fetch('/api/items'))  

## Pinia Store
npm install pinia  
// stores/counter.ts  
import { defineStore } from 'pinia'  
export const useCounterStore = defineStore('counter', {  
  state: () => ({ count: 0 }),  
  actions: { increment() { this.count++ } }  
})  
const counter = useCounterStore()  
counter.increment()  

## API Routes
server/api/hello.get.ts  
export default defineEventHandler(() => 'Hello API')  
server/api/user/[id].get.ts  
export default event => { return { id: event.context.params.id } }  

## Middleware
middleware/auth.ts  
export default defineNuxtRouteMiddleware((to, from) => {  
  if (!isLoggedIn()) return navigateTo('/login')  
})  
definePageMeta({ middleware: ['auth'] })  

## Plugins
plugins/myPlugin.ts  
export default defineNuxtPlugin(nuxtApp => { nuxtApp.provide('hello', () => 'Hello from plugin') })  
const hello = useNuxtApp().$hello()  

## Environment Variables
.env  
NUXT_API_URL=https://api.example.com  
process.env.NUXT_API_URL  
$config.NUXT_API_URL  

## Nuxt Config
// nuxt.config.ts  
export default defineNuxtConfig({  
  modules: ['@pinia/nuxt'],  
  css: ['~/assets/main.css'],  
  runtimeConfig: { public: { apiUrl: 'https://api.example.com' } }  
})  

## Assets & Public
assets/styles.css  
public/favicon.ico  
<img src="/favicon.ico">  
<img src="~/assets/image.png">  

## Head & Meta
useHead({ title: 'Nuxt App', meta: [ { name: 'description', content: 'Nuxt 3 cheatsheet' } ] })  
<Head>  
  <title>Nuxt App</title>  
</Head>  
definePageMeta({ title: 'Home' })  

## SSR & SSG
npm run build  
npm run preview  
npm run generate  

## Error Handling
throw createError({ statusCode: 404, statusMessage: 'Not found' })  
defineNuxtRouteMiddleware((to, from) => { if (!auth) throw createError({ statusCode: 401 }) })  

## useCookie
const token = useCookie('token')  
token.value = 'abc123'  

## useRouter
const router = useRouter()  
router.push('/login')  

## useRuntimeConfig
const config = useRuntimeConfig()  
config.public.apiUrl  

## useAsyncData
const { data, error, pending } = await useAsyncData('key', () => $fetch('/api/data'))  

## useFetch
const { data } = await useFetch('https://api.example.com/data')  

## <script setup>
<script setup lang="ts">  
const count = ref(0)  
defineProps<{ label: string }>()  
</script>  

## Props & Emits
defineProps<{ msg: string }>()  
defineEmits(['clicked'])  

## Transitions
<Transition name="fade"><div v-if="show">Hi</div></Transition>  

## Directives
v-if  
v-for  
v-show  
v-model  
v-bind  
v-on  
v-html  
v-text  

## Computed & Reactive
const count = ref(0)  
const doubled = computed(() => count.value * 2)  

## Watch
watch(count, val => { console.log(val) })  

## Lifecycle Hooks
onMounted(() => { ... })  
onUnmounted(() => { ... })  
onUpdated(() => { ... })  

## UseSlots
const slots = useSlots()  

## UseAttrs
const attrs = useAttrs()  

## Fetch in API Route
export default defineEventHandler(async (event) => {  
  const data = await $fetch('https://api.example.com')  
  return data  
})  

## NuxtLink
<NuxtLink to="/about">About</NuxtLink>  

## NuxtImage
<NuxtImg src="/logo.png" width="100" />  

## Nuxt Layouts
<NuxtLayout name="admin"><slot /></NuxtLayout>  
definePageMeta({ layout: 'admin' })  

## Custom 404
layouts/error.vue  
<template>Page Not Found</template>  

## Testing
npm install --save-dev vitest  
npm run test  
import { describe, it, expect } from 'vitest'  
describe('test', () => { it('should work', () => { expect(true).toBe(true) }) })  

## Deployment
npm run build  
npm run preview  
vercel deploy  
netlify deploy  

## Useful Modules
@nuxt/image  
@nuxt/content  
@nuxt/auth  
@nuxt/i18n  
@pinia/nuxt  
@nuxtjs/tailwindcss  
@nuxtjs/axios  

## Best Practices
Use composables for logic  
Keep components small  
Use Pinia for state management  
Organize pages and layouts  
Validate user input  
Document components  
Handle errors gracefully  
Keep code DRY  
Prefer <script setup>  
Use auto-imported composables  
Test API endpoints  
Keep assets optimized  
Write tests  
Use environment variables  
Version config  
Automate deployment  
Keep dependencies updated  
Use SSR for SEO  
Support mobile devices  
Monitor performance  
Compress images  
Implement lazy loading  
Use transitions for UI  
Keep styles scoped  
Comment complex logic  
Use meta tags for SEO  
Document API routes  
Handle authentication  
Use middleware for protection  
Support localization  
Review security updates  
Use proper naming  
Minimize global state  
Test edge cases  
Refactor old code  
Archive unused modules  
Keep changelog  
Automate builds  
Prefer TypeScript  
Lint code  
Monitor logs  
Optimize bundle size  
Use dynamic imports  
Support accessibility  
Version releases  
Backup configuration  
Test user flows  
Use error boundaries  
Keep code readable  
