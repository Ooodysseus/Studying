# Vue 3 Cheatsheet

## CLI & Project Setup
npm create vue@latest my-app  
npm run dev  
npm run build  
npm run test  
npm run lint  
npm install vue-router@4 pinia@latest  
npm install @vueuse/core  
npm install -D vitest @vue/test-utils

## Component
```vue
<script setup>
import { ref } from 'vue'
const title = ref('Hello Vue 3!')
</script>
<template>
  <h1>{{ title }}</h1>
</template>
```

## Props & Emits
```vue
<script setup>
const props = defineProps<{ name: string }>()
const emit = defineEmits<['update']>()
emit('update', 'new value')
</script>
```

## Data Binding
<template>
  {{ message }}
  <input v-model="message">
  <button @click="onClick">Click</button>
  <span :class="{ active: isActive }"></span>
  <img :src="imgUrl">
  <Child :data="parentData" />
  <input :disabled="isDisabled">
  <button @dblclick="doDouble"></button>
  <input @input="onInput">
</template>

## Conditional & List Rendering
v-if="isTrue"
v-else
v-show="visible"
v-for="(item, idx) in items" :key="item.id"
v-slot:default
v-slot:header

## Attribute & Event Directives
:class="{ active: isActive }"
:style="{ color: 'red' }"
:hidden="!isVisible"
:readonly="isReadonly"
:required="true"
@click="handleClick"
@input="onInput"
v-model="inputVal"
v-html="rawHtml"

## Computed & Watch
<script setup>
import { ref, computed, watch } from 'vue'
const count = ref(0)
const double = computed(() => count.value * 2)
watch(count, (val, old) => { /* ... */ })
</script>

## Lifecycle Hooks
<script setup>
import { onMounted, onUpdated, onUnmounted, onBeforeMount, onBeforeUpdate } from 'vue'
onMounted(() => { /* ... */ })
onUpdated(() => { /* ... */ })
onUnmounted(() => { /* ... */ })
</script>

## Slots
<Child>
  <template #default>Default Slot</template>
  <template #header>Header Content</template>
</Child>

## Provide / Inject
// Parent
import { provide } from 'vue'
provide('theme', 'dark')
// Child
import { inject } from 'vue'
const theme = inject('theme')

## Teleport
<Teleport to="body">
  <div>Modal Content</div>
</Teleport>

## Suspense
<Suspense>
  <template #default>
    <AsyncComponent />
  </template>
  <template #fallback>Loading...</template>
</Suspense>

## Template Refs
<template>
  <input ref="inputRef">
</template>
<script setup>
import { ref, onMounted } from 'vue'
const inputRef = ref(null)
onMounted(() => inputRef.value.focus())
</script>

## Vue Router
import { createRouter, createWebHistory } from 'vue-router'
const routes = [{ path: '/', component: Home }]
const router = createRouter({ history: createWebHistory(), routes })
createApp(App).use(router).mount('#app')

<router-link to="/">Home</router-link>
<router-view />

## Pinia (State Management)
import { createPinia, defineStore } from 'pinia'
createApp(App).use(createPinia())

export const useCounter = defineStore('counter', {
  state: () => ({ count: 0 }),
  actions: { increment() { this.count++ } }
})

const counter = useCounter()
counter.increment()

## Async Components
const AsyncComp = defineAsyncComponent(() => import('./AsyncComp.vue'))

## TypeScript Support
<script lang="ts" setup>
import { ref } from 'vue'
const count = ref<number>(0)
</script>

## Forms
<input v-model="inputVal">
<select v-model="selected">
  <option value="A">A</option>
  <option value="B">B</option>
</select>
<textarea v-model="text"></textarea>
<ValidationComponent :rules="{ required: true }" v-model="value" />

## Custom Directives
app.directive('focus', {
  mounted(el) { el.focus() }
})

## Mixins & Composables
// composables/useToggle.js
import { ref } from 'vue'
export function useToggle(initial = false) {
  const state = ref(initial)
  const toggle = () => (state.value = !state.value)
  return { state, toggle }
}

## Testing
import { mount } from '@vue/test-utils'
import { describe, it, expect } from 'vitest'
describe('MyComponent', () => {
  it('renders', () => {
    const wrapper = mount(MyComponent)
    expect(wrapper.text()).toContain('Hello')
  })
})

## Error Handling
try { /* ... */ } catch(e) { console.error(e) }
app.config.errorHandler = (err, vm, info) => { /* ... */ }

## Animations & Transitions
<template>
  <transition name="fade">
    <div v-if="show">Fade Me</div>
  </transition>
</template>
<style>
.fade-enter-active, .fade-leave-active { transition: opacity 0.5s }
.fade-enter-from, .fade-leave-to { opacity: 0 }
</style>

## Provide/Inject with Symbols (advanced)
const ThemeSymbol = Symbol()
provide(ThemeSymbol, 'dark')
const theme = inject(ThemeSymbol)

## Environment Variables
VITE_API_URL, import.meta.env.VITE_API_URL

## Internationalization
npm install vue-i18n
import { createI18n } from 'vue-i18n'
const i18n = createI18n({ locale: 'en', messages })
createApp(App).use(i18n)

$t('welcome')
<template><span>{{ $t('welcome') }}</span></template>

## SSR (Nuxt, Vite SSR)
npm create nuxt-app@latest
npm run dev

## Common Errors
"Property was accessed during render but is not defined"
"Failed to resolve component"
"Invalid prop: type check failed"
"Cannot read property 'value' of null"

## Useful Links
- [Vue 3 Docs](https://vuejs.org/guide/introduction.html)
- [Vue Router Docs](https://router.vuejs.org/)
- [Pinia Docs](https://pinia.vuejs.org/)
- [VueUse](https://vueuse.org/)
- [Vue 3 API Reference](https://vuejs.org/api/)
- [Vitest](https://vitest.dev/)

## Best Practices
Use <script setup> for composition API  
Group logic in composables  
Use Pinia for state management  
Keep components small and focused  
Type props and data  
Validate props/events  
Limit template nesting  
Split code into modules  
Test components and composables  
Use async components for code splitting  
Document complex logic  
Automate builds and tests  
Keep dependencies updated  
Backup config files  
Optimize for performance  
Monitor runtime errors  
Prefer composition API over options API  
Use named slots  
Archive unused code  
Update README  
Use transitions for UX  
Support SSR  
Use environment variables  
Use internationalization  
Prefer SCSS/SASS for styles  
Use Vite for builds  
Prefer functional components  
Use SVG icons  
Optimize images and assets  
Profile and monitor performance  
Automate linting and formatting  
Test edge cases  
Handle errors gracefully  
Prefer strong typing  
Use feature flags for experiments  
Use constants for magic values  
Organize routes and stores  
Keep code DRY  
Minimize global state  
Prefer readonly props  
Handle loading and error states  
Use async/await in composables  
Review and update dependencies  
Document APIs and types  
Support accessibility  
Prefer modular structure  
Use lazy loading for routes  
Handle 404 and fallback UI  
Implement pagination and search  
Review bundle size  
Use code splitting  
Follow Vue style guide  
Use CI/CD pipelines  
Backup configs  
Monitor logs  
Implement dark mode and themes  
Support mobile and responsive layouts  
Archive unused components  
Prefer composition over inheritance  
Use content projection  
Handle side effects in composables  
Use server-side rendering when needed  
Profile memory usage  
Write comments for complex logic  
Lint before commit  
Keep test coverage high  
Refactor old code  
Archive unused modules  
Review dependencies  
Optimize change detection  
Prefer native APIs  
Use tree-shakable modules  
Test real-world flows  
Implement SEO  
Check accessibility  
Use ARIA attributes  
Profile performance  
Automate deployment  
Use code reviews  
Optimize for mobile  
Support localization  
Use code splitting  
Prefer ES modules  
Cache static assets  
Monitor error logs  
Prefer stateless components  
Handle side effects  
Use feature modules  
Write integration tests  
Automate code formatting  
Use Husky for git hooks  
Handle edge cases in forms  
Share data via composables  
Document environment setup  
Prefer template over inline HTML  
Use theme support  
Implement loading states  
Handle API rate limits  
Use retry for failed requests  
Archive unused code  
Optimize bundle size  
Review updates  