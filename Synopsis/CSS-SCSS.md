# CSS/SCSS: сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке CSS та SCSS](#що-таке-css-та-scss)
-   [Історія та еволюція CSS](#історія-та-еволюція-css)
-   [Базова структура CSS](#базова-структура-css)
-   [Основні селектори](#основні-селектори)
-   [Властивості та значення](#властивості-та-значення)
-   [Box Model: Підкапотний розбір](#box-model-підкапотний-розбір)
-   [Flexbox: сучасний layout](#flexbox-сучасний-layout)
-   [Grid: потужна система розташування](#grid-потужна-система-розташування)
-   [SCSS та SASS: синтаксис, розширення](#scss-та-sass-синтаксис-розширення)
-   [Перемінні, вкладеність, міксіни, розширення](#перемінні-вкладеність-міксіни-розширення)
-   [Responsive Design: адаптивність](#responsive-design-адаптивність)
-   [Media Queries: контроль пристроїв](#media-queries-контроль-пристроїв)
-   [Анімації та переходи](#анімації-та-переходи)
-   [Custom Properties (CSS-змінні)](#custom-properties-css-змінні)
-   [Псевдокласи та псевдоелементи](#псевдокласи-та-псевдоелементи)
-   [Взаємодія з JavaScript](#взаємодія-з-javascript)
-   [Accessibility в CSS](#accessibility-в-css)
-   [Performance traps](#performance-traps)
-   [Внутрішні механізми CSS: розбір рендерингу](#внутрішні-механізми-css-розбір-рендерингу)
-   [Підводні камені та глибокі концепції](#підводні-камені-та-глибокі-концепції)
-   [Best practices](#best-practices)
-   [Корисні ресурси](#корисні-ресурси)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**CSS (Cascading Style Sheets)** — це мова стилів, що задає вигляд HTML-елементів на сторінці.  
**SCSS (Sassy CSS)** — надбудова над CSS, яка дає змогу використовувати змінні, вкладеність, міксіни й інші сучасні можливості для організації коду.  
У 2024 році CSS та SCSS — фундамент для гнучкого дизайну, адаптивності, анімацій, accessibility та швидкого масштабування front-end проектів.

---

## Що таке CSS та SCSS

-   **CSS** — стандартна технологія W3C для опису стилів HTML-документів.
-   **SCSS** — синтаксичне розширення CSS, частина препроцесора **Sass** (Syntactically Awesome Style Sheets).

### Порівняння

|             | CSS                         | SCSS                       |
| ----------- | --------------------------- | -------------------------- |
| Змінні      | Custom Properties (`--var`) | `$variable`                |
| Вкладеність | Немає                       | Є                          |
| Міксіни     | Немає                       | Є (`@mixin`)               |
| Логіка      | Мінімальна                  | Є (`@if`, `@for`, `@each`) |
| Імпорт      | `@import` (застаріло)       | `@use`, `@forward`         |

---

## Історія та еволюція CSS

-   **CSS1 (1996):** базові стилі для HTML.
-   **CSS2 (1998):** позиціонування, медіа-типи.
-   **CSS3 (2011+):** модульність, анімації, flexbox, grid, custom properties.
-   **2024+:** Wide gamut, container queries, advanced selectors, has(), layer, state-driven styling.

---

## Базова структура CSS

```css
/* Коментар українською: стиль для заголовка */
h1 {
    color: #2d2d2d;
    font-size: 2rem;
    margin-bottom: 1em;
}
```

### Селектор → Властивість: Значення

```css
селектор {
    властивість: значення;
}
```

#### Приклад для SCSS

```scss
// Коментар українською: вкладеність та змінна
$main-color: #0099ff;

.header {
    background: $main-color;
    .logo {
        width: 120px;
    }
}
```

---

## Основні селектори

| Селектор      | Опис                      | Приклад            |
| ------------- | ------------------------- | ------------------ |
| Елемент       | Всі елементи певного типу | `p {}`             |
| Клас          | Всі елементи з класом     | `.menu {}`         |
| ID            | Елемент з унікальним id   | `#header {}`       |
| Комбінований  | Елементи всередині іншого | `.nav a {}`        |
| Груповий      | Кілька селекторів разом   | `h1, h2 {}`        |
| Псевдоклас    | Стан елемента             | `a:hover {}`       |
| Псевдоелемент | Частина елемента          | `p::first-line {}` |

#### Приклад комбінованих селекторів

```css
nav ul li a.active {
    color: #ff6600;
}
```

---

## Властивості та значення

### Основні властивості

-   **Колір:** `color`, `background-color`
-   **Розміри:** `width`, `height`, `max-width`, `min-height`
-   **Відступи:** `margin`, `padding`
-   **Рамки:** `border`, `border-radius`
-   **Шрифти:** `font-family`, `font-size`, `font-weight`, `line-height`
-   **Вирівнювання:** `text-align`, `vertical-align`
-   **Позиціонування:** `position`, `top`, `left`, `z-index`
-   **Зображення:** `background-image`, `object-fit`
-   **Тіні:** `box-shadow`, `text-shadow`
-   **Opacity:** `opacity`, `visibility`

#### Приклад стилізації кнопки

```css
.button {
    background: linear-gradient(90deg, #0099ff 0%, #66ffcc 100%);
    border: none;
    border-radius: 8px;
    color: #fff;
    padding: 0.75em 2em;
    font-size: 1rem;
    cursor: pointer;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
    transition: background 0.3s;
}
.button:hover {
    background: linear-gradient(90deg, #0066cc 0%, #33cc99 100%);
}
```

---

## Box Model: Підкапотний розбір

Box Model — фундаментальна концепція CSS.

```
+----------------------------+
|      margin (зовнішній)    |
|  +----------------------+  |
|  |    border (рамка)    |  |
|  |  +----------------+  |  |
|  |  |  padding       |  |  |
|  |  |+-------------+ |  |  |
|  |  || content     | |  |  |
|  |  |+-------------+ |  |  |
|  |  +----------------+  |  |
|  +----------------------+  |
+----------------------------+
```

-   **content** — основний контент блоку
-   **padding** — внутрішній відступ
-   **border** — рамка навколо контенту
-   **margin** — зовнішній відступ

#### Приклад:

```css
.card {
    width: 300px;
    padding: 16px;
    border: 2px solid #e0e0e0;
    margin: 32px auto;
    box-sizing: border-box; /* сучасний best practice */
}
```

---

## Flexbox: сучасний layout

**Flexbox** — модуль для гнучкого розташування елементів.

### Основні властивості

-   `display: flex`
-   `flex-direction`
-   `justify-content`
-   `align-items`
-   `flex-wrap`
-   `flex-grow`, `flex-shrink`, `flex-basis`

#### Приклад горизонтального меню

```css
.menu {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 2rem;
}
.menu-item {
    padding: 0.5em 1.5em;
    border-radius: 6px;
    transition: background 0.2s;
}
.menu-item:hover {
    background: #f2f2f2;
}
```

#### Візуалізація

```
+--------+--------+--------+--------+
| Item 1 | Item 2 | Item 3 | Item 4 |
+--------+--------+--------+--------+
```

---

## Grid: потужна система розташування

**CSS Grid** — двовимірна система layout.

### Основні властивості

-   `display: grid`
-   `grid-template-columns`
-   `grid-template-rows`
-   `grid-gap` / `gap`
-   `grid-column`, `grid-row`
-   `grid-area`, `grid-template-areas`

#### Приклад Grid Layout

```css
.grid {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    gap: 24px;
}
.grid-item {
    background: #f8f8ff;
    padding: 1.5em;
    border-radius: 10px;
}
```

#### Схема

```
+-------------------------------+
|  1fr |   2fr   |   1fr        |
+-------------------------------+
| Item |  Item   |  Item        |
+-------------------------------+
```

---

## SCSS та SASS: синтаксис, розширення

**Sass** — препроцесор для CSS.  
**SCSS** — сучасний синтаксис Sass (майже як CSS).

### Основні можливості SCSS

-   Змінні: `$color: #0099ff;`
-   Вкладеність: вкладення селекторів
-   Міксіни: `@mixin`
-   Наслідування: `@extend`
-   Логіка: `@if`, `@for`, `@each`
-   Імпорт/forward: `@use`, `@forward`

#### Приклад SCSS

```scss
$primary: #0099ff;
$radius: 8px;

@mixin button-style($bg) {
    background: $bg;
    border-radius: $radius;
    color: #fff;
    padding: 0.75em 2em;
    transition: background 0.2s;
}

.button {
    @include button-style($primary);
    &:hover {
        background: darken($primary, 10%);
    }
}
```

---

## Перемінні, вкладеність, міксіни, розширення

### Змінні

```scss
$main-bg: #f3f7fb;
$text-dark: #222;
```

### Вкладеність

```scss
.card {
    background: $main-bg;
    h2 {
        color: $text-dark;
    }
    a {
        color: $main-bg;
        &:hover {
            color: $text-dark;
        }
    }
}
```

### Міксіни

```scss
@mixin flex-center {
    display: flex;
    justify-content: center;
    align-items: center;
}
.header {
    @include flex-center;
}
```

### Наслідування

```scss
%absolute-center {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}
.modal {
    @extend %absolute-center;
}
```

---

## Responsive Design: адаптивність

Адаптивний (responsive) дизайн — обов’язковий стандарт 2024+.

-   Використання відносних одиниць (`rem`, `%`, `vw`, `vh`)
-   Гнучкі layout-и (Flexbox, Grid)
-   Адаптивні зображення (`srcset`)
-   Відсутність фіксованих розмірів

#### Приклад адаптації:

```css
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2vw;
}
@media (max-width: 700px) {
    .container {
        padding: 0 1vw;
    }
    .menu {
        flex-direction: column;
    }
}
```

---

## Media Queries: контроль пристроїв

**Media queries** — ключ до адаптивності.

```css
@media (max-width: 600px) {
    body {
        font-size: 1rem;
    }
    .grid {
        grid-template-columns: 1fr;
    }
}
@media (orientation: landscape) {
    .hero {
        height: 60vh;
    }
}
```

#### Актуальні фічі 2024+:

-   container queries (`@container`)
-   prefers-color-scheme (темна/світла тема)
-   pointer, hover, resolution

---

## Анімації та переходи

CSS дозволяє створювати smooth transitions та keyframe animations.

### Transition

```css
.button {
    transition: background 0.2s, box-shadow 0.2s;
}
.button:hover {
    background: #0055aa;
    box-shadow: 0 4px 24px #0055aa33;
}
```

### Keyframes

```css
@keyframes fade-in {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}
.modal {
    animation: fade-in 0.6s ease-in;
}
```

---

## Custom Properties (CSS-змінні)

**CSS Custom Properties** (змінні) — стандарт 2024+.

```css
:root {
    --main-bg: #f7fafc;
    --accent: #0099ff;
}
.header {
    background: var(--main-bg);
    color: var(--accent);
}
.button {
    background: var(--accent);
}
```

-   Можна змінювати значення змінних через JS, адаптувати тему

---

## Псевдокласи та псевдоелементи

### Псевдокласи

-   `:hover`, `:active`, `:focus`
-   `:nth-child(n)`, `:first-child`, `:last-child`
-   `:not()`, `:disabled`, `:checked`

### Псевдоелементи

-   `::before`, `::after`
-   `::first-line`, `::placeholder`

#### Приклад:

```css
.input:focus {
    outline: 2px solid #0099ff;
}
.button::after {
    content: " →";
}
```

---

## Взаємодія з JavaScript

CSS може змінюватись програмно через JS.

```js
// Зміна теми через змінні CSS
document.documentElement.style.setProperty("--accent", "#ff6600");

// Додавання класу для анімації
element.classList.add("is-active");
```

---

## Accessibility в CSS

-   Високий контраст для тексту й інтерфейсу
-   Видимий фокус (`:focus`)
-   Не приховуй елементи, якщо вони мають бути доступні з клавіатури
-   Використання `@media (prefers-reduced-motion)` для користувачів з обмеженнями

```css
@media (prefers-reduced-motion: reduce) {
    * {
        animation: none !important;
        transition: none !important;
    }
}
```

---

## Performance traps

### Типові пастки:

-   Великі CSS-файли без оптимізації
-   Застарілі селектори з великою специфічністю
-   Зловживання `:nth-child` на великих DOM-деревах
-   Inline-стилі замість класів
-   CSS, що блокує рендеринг (`@import` у CSS, не у SCSS!)

---

## Внутрішні механізми CSS: розбір рендерингу

### Як браузер обробляє CSS

1. **Парсинг** — браузер створює CSSOM (CSS Object Model)
2. **Об’єднання DOM + CSSOM** → Render Tree
3. **Layout** — визначення розміру та положення елементів
4. **Paint** — промальовування стилів
5. **Composite** — складання шарів у кінцеве зображення

#### Схема

```
HTML → DOM
CSS  → CSSOM
DOM + CSSOM → Render Tree → Layout → Paint → Composite
```

### Performance traps

-   Reflow (зміна layout) — важко для браузера
-   Repaint (зміна стилів) — легше, але часто
-   Слідкуй за кількістю шарів та анімацій

---

## Підводні камені та глибокі концепції

### Специфічність

-   Inline-стилі > ID > клас > тег
-   !important — найвища специфічність, уникай!

### Наслідування

-   Не всі властивості наслідуються автоматично
-   Наслідування залежить від типу властивості (наприклад, `color` наслідується, `margin` — ні)

### Глобальні стилі vs модульні

-   Використовуй CSS-модулі, SCSS-локалізацію, BEM, або сучасні інструменти (CSS-in-JS)

### Container queries

```css
@container (min-width: 500px) {
    .card {
        font-size: 1.5rem;
    }
}
```

---

## Best practices

-   Використовуй SCSS/Custom Properties для змінних та тем
-   Групуй стилі за компонентами, а не за сторінками
-   Не перевантажуй селектори (уникай надмірної специфічності)
-   Розділяй лейаути з використанням flexbox/grid
-   Завжди тестуй адаптивність на різних пристроях
-   Валідуй CSS ([CSS Validator](https://jigsaw.w3.org/css-validator/))
-   Використовуй сучасні препроцесори (SCSS, PostCSS)
-   Підключай CSS-файли асинхронно (`rel="preload"`)
-   Мінімізуй та оптимізуй CSS перед релізом

---

## Корисні ресурси

-   [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS)
-   [Sass Official Guide](https://sass-lang.com/guide)
-   [CSS Tricks](https://css-tricks.com/)
-   [Web.dev CSS](https://web.dev/css/)
-   [Smashing Magazine CSS](https://www.smashingmagazine.com/category/css/)
-   [Can I Use](https://caniuse.com/)
-   [CSS Grid Guide](https://cssgrid.io/)
-   [Flexbox Froggy](https://flexboxfroggy.com/)
-   [CSS Validator](https://jigsaw.w3.org/css-validator/)
-   [Accessibility Cheatsheet](https://webaim.org/resources/contrastchecker/)
-   [Container Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Container_Queries)

---

## Короткий підсумок

**CSS/SCSS — це потужний інструмент для створення сучасних, адаптивних, швидких та доступних інтерфейсів.**  
Глибоке розуміння Box Model, Flexbox, Grid, специфічності, рендерингу та accessibility дозволяє створювати професійний код, що легко підтримується і масштабуються.  
Дотримуйся best practices, регулярно оновлюй знання, тестуй на реальних пристроях і використовуй сучасні можливості CSS (2024+).  
Для поглибленого вивчення — обирай офіційні ресурси та експериментуй із сучасними інструментами!

---
