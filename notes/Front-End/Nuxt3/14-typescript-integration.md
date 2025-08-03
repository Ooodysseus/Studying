# Інтеграція з TypeScript

## Фундаментальні механізми інтеграції Nuxt3 з TypeScript

TypeScript — це надбудова над JavaScript, яка додає статичну типізацію, автодоповнення, рефакторинг і контроль помилок на етапі компіляції. Nuxt3 має повну підтримку TypeScript, що дозволяє типізувати компоненти, props, emits, ref, computed, API та інтегрувати типи у весь проєкт.

---

## Чому варто використовувати TypeScript у Nuxt3?

-   Зменшення кількості runtime-помилок.
-   Краще автодоповнення у редакторі.
-   Легший рефакторинг великих проєктів.
-   Документування API через типи.

---

## Основи типізації компонентів

### Типізація props

```ts
import { defineComponent, PropType } from "vue";

export default defineComponent({
    props: {
        items: Array as PropType<string[]>,
        count: {
            type: Number,
            required: true,
        },
    },
});
```

### Типізація emits

```ts
const emit = defineEmits<{ (e: "update", value: number): void }>();
```

---

## Composition API з TypeScript

Composition API дозволяє типізувати ref, computed, inject, provide.

#### Приклад:

```ts
import { ref, computed } from "vue";

const count = ref<number>(0);
const double = computed(() => count.value * 2);
```

---

## Типізація шаблонів

Шаблони у Nuxt3 автоматично отримують типи з компонентів, але для складних кейсів можна використовувати generic-компоненти.

#### Приклад generic-компонента:

```ts
<script lang="ts">
import { defineComponent, PropType } from 'vue';

export default defineComponent({
  props: {
    value: {
      type: Object as PropType<T>,
      required: true,
    },
  },
});
</script>
```

---

## Advanced: типізація слота, provide/inject, API

-   Типізуйте слоти через SlotProps.
-   Використовуйте типи для provide/inject:

```ts
provide("user", ref<User>({ name: "Anna" }));
inject<User>("user");
```

-   Типізуйте API-запити через інтерфейси.

---

## Best practices

-   Використовуйте strict режим у tsconfig.json.
-   Типізуйте всі props, emits, слоти.
-   Використовуйте інтерфейси для складних об’єктів.
-   Не ігноруйте any — завжди уточнюйте типи.
-   Інтегруйте типи у API, state, router.
-   Оновлюйте типи при рефакторингу.

---

## Типові помилки та антипатерни

-   Відсутність типізації props/emits.
-   Використання any замість конкретних типів.
-   Відсутність типізації API-запитів.
-   Відсутність strict режиму у tsconfig.json.
-   Відсутність типізації слота.

---

## Таблиця: порівняння підходів типізації

| Підхід             | Плюси           | Мінуси                 |
| ------------------ | --------------- | ---------------------- |
| Options API        | Простота        | Менше типів            |
| Composition API    | Гнучкість, типи | Складніше для новачків |
| Generic-компоненти | Гнучкість       | Складна типізація      |

---

## Діаграма: flow інтеграції TypeScript у Nuxt3

```mermaid
flowchart TD
    Code --> TypeScript
    TypeScript --> NuxtComponent
    NuxtComponent --> Template
    Template --> API
    API --> Test
```

---

## Практичні кейси

-   Міграція проєкту з JS на TS: поступово додавайте типи, використовуйте strict режим.
-   Типізація API: створіть інтерфейси для response/request.
-   Типізація router: використовуйте типи для route params.
-   Типізація store (Pinia): визначайте state, getters, actions через інтерфейси.

---

## FAQ по інтеграції TypeScript у Nuxt3

-   Як налаштувати tsconfig.json? — Використовуйте strict, include src, exclude node_modules.
-   Чи можна типізувати слоти? — Так, через SlotProps.
-   Як типізувати emits? — Через generic у defineEmits.
-   Як інтегрувати типи у API? — Через інтерфейси для response/request.

---

## Додаткові ресурси

-   [Nuxt3 + TypeScript Guide](https://nuxt.com/docs/guide/typescript)
-   [TypeScript Handbook](https://www.typescriptlang.org/docs/)
-   [Pinia + TypeScript](https://pinia.vuejs.org/cookbook/typescript.html)
-   [Nuxt3 Router + TS](https://nuxt.com/docs/guide/directory-structure/pages#typescript-support)

---

## Підсумок

Інтеграція TypeScript у Nuxt3 — це шлях до якісного, безпечного та масштабованого коду. Типізуйте все, використовуйте best practices, і ваш проєкт буде легким для підтримки та розвитку.
