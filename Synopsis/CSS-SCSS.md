# Ultimate CSS & SCSS Cheat Sheet

## ⭐ Description

CSS (Cascading Style Sheets) is used to style and layout web pages. SCSS (Sassy CSS) extends CSS with variables, nesting, mixins, and logic.

## ⭐ Relationship With Other Technologies

-   HTML: CSS/SCSS styles HTML elements.
-   JS/TS: JS/TS can manipulate styles dynamically.
-   Vue/Angular/Nuxt/Electron: Use CSS/SCSS for component styling, support scoped styles.
-   Node/Express, Django: Serve CSS files for client-side styling.

---

## 1. Selectors

-   Universal: `*`
-   Type: `div`, `p`, `h1`
-   Class: `.my-class`
-   ID: `#my-id`
-   Attribute: `[type="text"]`
-   Child: `ul > li`
-   Descendant: `div p`
-   Sibling: `h2 + p`
-   Grouping: `h1, h2, h3`
-   Pseudo-class: `a:hover`, `input:focus`, `li:first-child`
-   Pseudo-element: `p::before`, `p::after`, `input::placeholder`

---

## 2. Properties

### Typography

```css
font-family: "Roboto", sans-serif;
font-size: 16px;
font-weight: 700;
line-height: 1.5;
letter-spacing: 0.1em;
text-align: center;
text-transform: uppercase;
text-decoration: underline;
text-shadow: 2px 2px #888;
```

### Colors & Backgrounds

```css
color: #333;
background-color: #fafafa;
background-image: url("bg.jpg");
background-size: cover;
background-repeat: no-repeat;
background-position: center;
opacity: 0.7;
```

### Box Model

```css
margin: 10px 20px;
padding: 1em 2em;
border: 1px solid #ccc;
border-radius: 8px;
box-sizing: border-box;
width: 100vw;
height: 50vh;
```

### Layout: Display, Position, Float

```css
display: block;
display: inline-block;
display: flex;
display: grid;
float: right;
clear: both;
position: relative;
top: 10px;
left: 20px;
z-index: 100;
overflow: auto;
```

### Flexbox

```css
.container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
}
```

### Grid

```css
.grid {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    grid-template-rows: auto 100px;
    grid-gap: 10px;
    grid-area: header;
}
```

### Effects

```css
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
filter: blur(2px);
transform: scale(1.1) rotate(15deg);
transition: color 0.3s, background 0.3s;
```

---

## 3. Responsive Design

```css
@media (max-width: 600px) {
    body {
        font-size: 14px;
    }
    .sidebar {
        display: none;
    }
}
@media (min-width: 1200px) {
    .container {
        max-width: 1200px;
    }
}
```

-   Use media queries for mobile-first design.

---

## 4. Variables

### CSS Custom Properties

```css
:root {
    --primary: #3498db;
    --padding: 1rem;
}
.button {
    color: var(--primary);
    padding: var(--padding);
}
```

### SCSS Variables

```scss
$primary: #e74c3c;
$padding: 1rem;
.button {
    color: $primary;
    padding: $padding;
}
```

---

## 5. SCSS Features

### Nesting

```scss
nav {
    ul {
        li {
            a {
                color: $primary;
                &:hover {
                    color: darken($primary, 10%);
                }
            }
        }
    }
}
```

### Mixins

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

### Extends

```scss
%btn-base {
    padding: 0.5em 1em;
    border-radius: 4px;
}
.button {
    @extend %btn-base;
}
```

### Functions

```scss
@function rem($px) {
    @return $px / 16 * 1rem;
}
.text {
    font-size: rem(18);
}
```

### Import & Use

```scss
@import "variables";
@use "mixins";
```

---

## 6. Animations

```css
@keyframes fadein {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}
.fade {
    animation: fadein 1.5s ease-in;
}
```

-   Combine with `transition` for smooth effects.

---

## 7. Custom Fonts

```css
@font-face {
    font-family: "MyFont";
    src: url("myfont.woff2") format("woff2");
}
body {
    font-family: "MyFont", Arial, sans-serif;
}
```

---

## 8. Utility Classes

```css
.mt-4 {
    margin-top: 4rem;
}
.text-center {
    text-align: center;
}
.w-100 {
    width: 100%;
}
.d-none {
    display: none;
}
```

---

## 9. CSS Specificity

-   Inline style > ID > Class > Type > Universal
-   Use specificity calculator: [https://polypane.app/css-specificity-calculator/](https://polypane.app/css-specificity-calculator/)

---

## 10. CSS Variables vs. SCSS Variables

| Feature           | CSS Variables                             | SCSS Variables   |
| ----------------- | ----------------------------------------- | ---------------- |
| Dynamic (runtime) | ✔️                                        | ❌               |
| Scoped            | ✔️                                        | ❌ (global only) |
| JS Access         | `element.style.getPropertyValue('--var')` | ❌               |
| Compilation       | ❌                                        | ✔️               |

---

## 11. CSS Grid vs Flexbox

| Feature        | Flexbox         | Grid                 |
| -------------- | --------------- | -------------------- |
| Axis           | 1D (row/column) | 2D (row+column)      |
| Complex Layout | ❌              | ✔️                   |
| Responsive     | ✔️              | ✔️                   |
| Subgrid        | ❌              | ✔️ (modern browsers) |

---

## 12. Best Practices

-   Use BEM naming (`.block__elem--mod`).
-   Prefer classes, avoid IDs for styling.
-   Keep style modular and DRY.
-   Use preprocessors (SCSS) for large projects.
-   Minify CSS for production.
-   Use logical properties: `margin-inline`, `padding-block`.

---

## 13. Tools & Resources

-   [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS)
-   [Sass Official](https://sass-lang.com/)
-   [Autoprefixer](https://github.com/postcss/autoprefixer)
-   [Can I use](https://caniuse.com/)
-   [CSS Tricks](https://css-tricks.com/)

---

## 14. Interoperability Table

| Feature      | CSS/SCSS  | HTML | JS/TS | Vue/Angular/Nuxt | Node/Express | Django/Python | Electron |
| ------------ | --------- | ---- | ----- | ---------------- | ------------ | ------------- | -------- |
| Styling      | ✔️        |      |       | ✔️ (scoped)      | (static)     | (static)      | ✔️       |
| Dynamic      |           |      | ✔️    | ✔️               |              |               | ✔️       |
| Preprocessor | ✔️ (SCSS) |      |       | ✔️               |              |               | ✔️       |
