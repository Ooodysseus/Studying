# CSS / SCSS: Від основ до advanced (повний конспект)

---

## Зміст

1. [Вступ: Що таке CSS/SCSS і для чого вони потрібні](#вступ)
2. [Базові поняття: стилі, правила, селектори, пріоритетність](#базові-поняття)
3. [Підключення CSS: зовнішній, внутрішній, інлайн](#підключення-css)
4. [Синтаксис та структура CSS](#синтаксис-та-структура-css)
5. [Селектори: види, комбінатори, специфічність](#селектори)
6. [Базові властивості: кольори, фони, шрифти, відступи, розміри, межі](#базові-властивості)
7. [Боксова модель, box-sizing, overflow](#боксова-модель)
8. [Позиціонування: static, relative, absolute, fixed, sticky; z-index](#позиціонування)
9. [Розмітка: display, float, clear, visibility, opacity, outline](#розмітка)
10. [Flexbox: синтаксис, властивості, приклади](#flexbox)
11. [Grid: синтаксис, властивості, приклади](#grid)
12. [Псевдокласи, псевдоелементи, advanced-селектори](#псевдокласи)
13. [Транзиції, анімації, keyframes](#анімації)
14. [Медіа-запити, адаптивність, responsive design](#медіа-запити)
15. [Змінні, функції, calc(), custom properties](#змінні-функції)
16. [SCSS: основи, вкладеність, змінні, міксіни, extend, функції, оператори, цикли](#scss)
17. [Advanced: кастомні властивості, clamp/fit-content/min/max, CSS Houdini, CSS-in-JS, ізоляція стилів, performance](#advanced)
18. [Типові помилки, антипатерни, best practices](#типові-помилки)
19. [Практичні поради, методології (BEM, SMACSS, OOCSS)](#практичні-поради)
20. [Корисні ресурси](#корисні-ресурси)

---

## 1. Вступ: Що таке CSS/SCSS і для чого вони потрібні <a name="вступ"></a>

-   **CSS (Cascading Style Sheets)** — мова для оформлення зовнішнього вигляду HTML-документу.
-   **SCSS/SASS** — надбудова над CSS (препроцесор): дає змінні, вкладеність, міксіни, функції, цикли.
-   CSS описує кольори, шрифти, розміри, положення, анімації, переходи, адаптивність.
-   SCSS використовується для великих проектів, де важлива підтримуваність і DRY-код.

---

## 2. Базові поняття: стилі, правила, селектори, пріоритетність <a name="базові-поняття"></a>

-   **Правило**: селектор + блок властивостей.
-   **Селектор**: визначає, до яких елементів застосовувати стиль.
-   **Властивість**: наприклад, color, font-size, margin.
-   **Значення**: наприклад, red, 16px, auto.
-   **Каскадність** — чим “ближчий” стиль, тим вищий пріоритет.
-   **Специфічність**: inline style > id > class > тег. `!important` перебиває все (але зловживати не варто).

---

## 3. Підключення CSS: зовнішній, внутрішній, інлайн <a name="підключення-css"></a>

-   **Зовнішній**:
    ```html
    <link rel="stylesheet" href="styles.css" />
    ```
-   **Внутрішній**:
    ```html
    <style>
        body {
            color: navy;
        }
    </style>
    ```
-   **Інлайн**:
    ```html
    <div style="background: yellow;">Текст</div>
    ```

---

## 4. Синтаксис та структура CSS <a name="синтаксис-та-структура-css"></a>

```css
селектор {
    властивість: значення;
    інша-властивість: інше-значення;
}
```

**Приклад:**

```css
h1 {
    color: #333;
    margin-bottom: 20px;
}
```

---

## 5. Селектори: види, комбінатори, специфічність <a name="селектори"></a>

-   **Тег**: `p {}`
-   **Клас**: `.menu {}`
-   **Id**: `#header {}`
-   **Атрибут**: `input[type="text"] {}`
-   **Комбінатори**:
    -   “>” — прямий нащадок: `ul > li`
    -   “ ” — нащадок будь-якого рівня: `nav a`
    -   “+” — сусідній елемент: `h2 + p`
    -   “~” — всі наступні брати: `h2 ~ p`
-   **Групування**: `h1, h2, h3 {}`

**Специфічність**:

-   inline style: 1000
-   id: 100
-   class/attr/pseudo-class: 10
-   тег/псевдоелемент: 1

---

## 6. Базові властивості: кольори, фони, шрифти, відступи, розміри, межі <a name="базові-властивості"></a>

```css
body {
    color: #222;
    background-color: #f9f9f9;
    font-family: "Roboto", Arial, sans-serif;
    font-size: 18px;
    line-height: 1.6;
    margin: 0;
    padding: 0;
}

img {
    width: 100%;
    max-width: 400px;
    border-radius: 10px;
    border: 2px solid #eee;
}
```

-   **Відступи**: margin, padding
-   **Межі**: border, border-radius, border-style, border-color, outline
-   **Фон**: background, background-image, background-size, background-position, background-repeat
-   **Тіні**: box-shadow, text-shadow

---

## 7. Боксова модель, box-sizing, overflow <a name="боксова-модель"></a>

-   **Боксова модель**: content → padding → border → margin
-   **box-sizing: border-box** — padding і border враховуються у width/height.
-   **overflow**: визначає, що робити з контентом, який “вилазить” за межі блока.

```css
.box {
    width: 300px;
    padding: 20px;
    border: 2px solid #333;
    margin: 10px;
    box-sizing: border-box;
    overflow: auto;
}
```

---

## 8. Позиціонування: static, relative, absolute, fixed, sticky; z-index <a name="позиціонування"></a>

```css
.relative {
    position: relative;
    left: 20px;
    top: 10px;
}
.absolute {
    position: absolute;
    right: 10px;
    top: 30px;
}
.fixed {
    position: fixed;
    bottom: 0;
    width: 100%;
}
.sticky {
    position: sticky;
    top: 0;
}
```

-   **z-index** — порядок накладання (тільки для позиціонованих елементів).

---

## 9. Розмітка: display, float, clear, visibility, opacity, outline <a name="розмітка"></a>

-   **display**: block, inline, inline-block, none, flex, grid, contents
-   **float**: left, right
-   **clear**: left, right, both
-   **visibility**: visible, hidden, collapse
-   **opacity**: 0 (прозорий) — 1 (непрозорий)
-   **outline**: обводка (не впливає на розмір)

---

## 10. Flexbox: синтаксис, властивості, приклади <a name="flexbox"></a>

```css
.flex-container {
    display: flex;
    flex-direction: row; /* або column */
    justify-content: space-between; /* вирівнювання по осі X */
    align-items: center; /* вирівнювання по осі Y */
    gap: 24px;
}
.flex-item {
    flex: 1 1 0; /* grow, shrink, basis */
    align-self: flex-end;
}
```

-   **order**: порядок елемента
-   **flex-wrap**: wrap, nowrap

---

## 11. Grid: синтаксис, властивості, приклади <a name="grid"></a>

```css
.grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: auto 150px;
    gap: 20px;
}
.grid-item {
    grid-column: 1 / 3;
    grid-row: 2 / 3;
    grid-area: header;
}
```

-   **justify-items**, **align-items**, **place-items**
-   **grid-auto-flow**: row, column, dense

---

## 12. Псевдокласи, псевдоелементи, advanced-селектори <a name="псевдокласи"></a>

-   **Псевдокласи**: :hover, :active, :focus, :visited, :checked, :nth-child(), :not(), :disabled, :first-of-type
-   **Псевдоелементи**: ::before, ::after, ::first-letter, ::first-line, ::placeholder

```css
a:hover {
    color: red;
}
input:focus {
    outline: 2px solid blue;
}
li:nth-child(even) {
    background: #eee;
}
span::before {
    content: "→ ";
}
```

---

## 13. Транзиції, анімації, keyframes <a name="анімації"></a>

-   **Транзиція**:
    ```css
    .btn {
        transition: background 0.3s, color 0.3s;
    }
    .btn:hover {
        background: #333;
        color: #fff;
    }
    ```
-   **Анімація**:
    ```css
    @keyframes pulse {
        0% {
            transform: scale(1);
        }
        50% {
            transform: scale(1.1);
        }
        100% {
            transform: scale(1);
        }
    }
    .logo {
        animation: pulse 2s infinite;
    }
    ```

---

## 14. Медіа-запити, адаптивність, responsive design <a name="медіа-запити"></a>

```css
@media (max-width: 600px) {
    .menu {
        flex-direction: column;
    }
    body {
        font-size: 16px;
    }
}
```

-   **min-width / max-width** — mobile first!
-   **orientation, print, hover, pointer** — для специфічних пристроїв

---

## 15. Змінні, функції, calc(), custom properties <a name="змінні-функції"></a>

-   **CSS-змінні (custom properties):**
    ```css
    :root {
        --main-color: #09f;
        --gap: 20px;
    }
    .title {
        color: var(--main-color);
        margin-bottom: var(--gap);
    }
    ```
-   **calc()**:
    ```css
    .box {
        width: calc(100% - 40px);
    }
    ```
-   **clamp()** для адаптивних розмірів:
    ```css
    font-size: clamp(14px, 4vw, 24px);
    ```

---

## 16. SCSS: основи, вкладеність, змінні, міксіни, extend, функції, оператори, цикли <a name="scss"></a>

-   **Змінні:**
    ```scss
    $main-color: #09f;
    $padding: 24px;
    ```
-   **Вкладеність:**
    ```scss
    nav {
        ul {
            margin: 0;
        }
        li {
            display: inline-block;
        }
    }
    ```
-   **Міксіни:**
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
-   **Extend:**
    ```scss
    %btn-base {
        padding: 10px;
        border-radius: 5px;
    }
    .btn {
        @extend %btn-base;
    }
    ```
-   **Функції:**
    ```scss
    $darker: darken($main-color, 10%);
    ```
-   **Оператори:**
    ```scss
    .col {
        width: (100% / 3);
    }
    ```
-   **Цикли:**
    ```scss
    @for $i from 1 through 3 {
        .m-#{$i} {
            margin: #{$i * 10}px;
        }
    }
    ```

---

## 17. Advanced: кастомні властивості, clamp/fit-content/min/max, CSS Houdini, CSS-in-JS, ізоляція стилів, performance <a name="advanced"></a>

-   **clamp(), min(), max()** — для адаптивних значень.
-   **fit-content** — обрізка/розтягування блоку по контенту.
    ```css
    .card {
        width: fit-content;
    }
    ```
-   **CSS Houdini** — API для створення власних CSS-властивостей.
-   **CSS-in-JS** — стилізація компонентів прямо у JS (Styled Components, Emotion).
-   **Ізоляція стилів:** shadow DOM, BEM, CSS Modules.
-   **Performance:** мінімізація селекторів, low specificity, уникати великих вкладеностей, не зловживати heavy-ефектами.

---

## 18. Типові помилки, антипатерни, best practices <a name="типові-помилки"></a>

-   Зловживання `!important`, inline-стилями.
-   div-суп (все у div, нема семантики).
-   Глибока вкладеність у SCSS (>3-4 рівнів).
-   Відсутність адаптивності.
-   Неунікальні імена класів/id.
-   Дублювання коду, не використання міксінів/змінних.
-   Перевантаження специфічності селекторів.
-   Незрозумілі/“одноразові” імена класів.

---

## 19. Практичні поради, методології (BEM, SMACSS, OOCSS) <a name="практичні-поради"></a>

-   Структуруй стилі: спочатку reset/normalize, потім базові стилі, далі компоненти/модулі.
-   Використовуй BEM для класів: `.block__element--modifier`
-   Винось кольори/відступи/шрифти у змінні.
-   Пиши DRY-код: повторювані блоки — через міксіни або компоненти.
-   Використовуй SCSS для великих проектів.
-   Для адаптивності — mobile first, потім розширюй.
-   Перевіряй стилі на [CSS Validator](https://jigsaw.w3.org/css-validator/).
-   Для великих проектів — розбивай SCSS на partials (`_header.scss`, `_footer.scss`).

---

## 20. Корисні ресурси <a name="корисні-ресурси"></a>

-   [MDN Web Docs: CSS](https://developer.mozilla.org/uk/docs/Web/CSS)
-   [CSS Tricks](https://css-tricks.com/)
-   [Sass офіційно](https://sass-lang.com/)
-   [Flexbox Froggy](https://flexboxfroggy.com/)
-   [Grid Garden](https://cssgridgarden.com/)
-   [Can I use](https://caniuse.com/)
-   [smacss.com](https://smacss.com/)
-   [bem.info](https://en.bem.info/)

---

**CSS — це не просто “пофарбувати фон”. Глибоке знання CSS/SCSS допоможе робити красиві, підтримувані, адаптивні і швидкі інтерфейси.**
