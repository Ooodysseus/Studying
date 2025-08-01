# HTML (HyperText Markup Language): сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке HTML](#що-таке-html)
-   [Історія та еволюція HTML](#історія-та-еволюція-html)
-   [Сучасна структура HTML-документа](#структура-html-документа)
-   [Основні елементи](#основні-елементи)
-   [Атрибути](#атрибути)
-   [Семантичні елементи](#семантичні-елементи)
-   [Вкладеність і DOM](#вкладеність-i-dom)
-   [Мультимедіа](#мультимедіа)
-   [Графіка та SVG](#графіка-та-svg)
-   [Форми та введення даних](#форми-та-введення-даних)
-   [Accessibility (доступність)](#accessibility-доступність)
-   [SEO-оптимізація](#seo-оптимізація)
-   [Безпека HTML](#безпека-html)
-   [Performance (продуктивність)](#performance-продуктивність)
-   [Внутрішні механізми: як працює HTML](#внутрішні-механізми-робота-html)
-   [Підводні камені та глибокі концепції](#підводні-камені-глибокі-концепції)
-   [Web Components: Custom Elements, Shadow DOM](#web-components-custom-elements-shadow-dom)
-   [Best practices (кращі практики)](#best-practices-кращі-практики)
-   [Корисні ресурси та документація](#корисні-ресурси-та-документація)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

HTML (HyperText Markup Language) — це основа всього web-простору. Саме HTML задає структуру, семантику, доступність та взаємодію контенту на сторінці, а також служить фундаментом для CSS (Cascading Style Sheets) і JavaScript. У 2024 році HTML залишається універсальною платформою для створення web-додатків і сайтів, інтегрується з сучасними фреймворками (React, Vue, Angular, Svelte), постійно оновлюється завдяки WHATWG та W3C.

---

## Що таке HTML

HTML — декларативна мова розмітки, що дозволяє описувати структуру web-документа за допомогою тегів (tags). Вона не є мовою програмування, але відіграє ключову роль у побудові інтерфейсів.

### Основні функції HTML:

-   Структурує контент для браузера та користувача.
-   Забезпечує семантику (значення) кожного елемента.
-   Додає доступність (accessibility).
-   Взаємодіє з CSS, JavaScript, Web APIs.

---

## Історія та еволюція HTML

-   **1991:** Тим Бернерс-Лі створює першу версію HTML.
-   **1997:** HTML 4.0 — перший великий стандарт.
-   **2014:** HTML5 — революція у web-технологіях: семантика, мультимедіа, API.
-   **2024+:** HTML розвивається як "living standard" (WHATWG), отримує нові елементи, API, інтеграцію з Web Components.

---

## Сучасна структура HTML-документа

```html
<!DOCTYPE html>
<html lang="uk">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Сучасний HTML документ</title>
        <link rel="stylesheet" href="styles.css" />
    </head>
    <body>
        <header>
            <h1>Вітаємо у світі сучасного HTML!</h1>
            <nav>
                <ul>
                    <li><a href="#main">Головна</a></li>
                    <li><a href="#about">Про HTML</a></li>
                </ul>
            </nav>
        </header>
        <main id="main">
            <section>
                <h2 id="about">Опис</h2>
                <p>Це приклад сучасної структури документа HTML.</p>
            </section>
        </main>
        <footer>
            <p>&copy; 2025 HTML Deep Dive</p>
        </footer>
        <script src="app.js" defer></script>
    </body>
</html>
```

### Ключові моменти:

-   `<!DOCTYPE html>` — визначає HTML5.
-   `lang="uk"` — локалізація, важливо для accessibility та SEO.
-   Мета-теги (`meta`) — для коректного відображення на різних пристроях.
-   Семантичні елементи (`header`, `main`, `section`, `footer`).
-   Сучасний підхід: зовнішні стилі та скрипти підключаються через `link` та `script` з атрибутом `defer`.

---

## Основні елементи

### Базові теги та їх призначення

| Елемент        | Опис                              |
| -------------- | --------------------------------- |
| `<div>`        | Блочний контейнер (без семантики) |
| `<span>`       | Рядковий контейнер                |
| `<p>`          | Абзац                             |
| `<h1>–<h6>`    | Заголовки різних рівнів           |
| `<a>`          | Гіперпосилання                    |
| `<img>`        | Зображення                        |
| `<ul>`, `<ol>` | Нумеровані та марковані списки    |
| `<li>`         | Елемент списку                    |
| `<table>`      | Таблиця                           |
| `<form>`       | Форма введення                    |
| `<button>`     | Кнопка                            |
| `<input>`      | Поле вводу                        |

#### Приклад списку:

```html
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>
```

#### Приклад таблиці:

```html
<table>
    <thead>
        <tr>
            <th>Мова</th>
            <th>Рік появи</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>HTML</td>
            <td>1991</td>
        </tr>
        <tr>
            <td>JavaScript</td>
            <td>1995</td>
        </tr>
    </tbody>
</table>
```

---

## Атрибути

Атрибути — додаткові властивості до тегів.

```html
<a
    href="https://developer.mozilla.org/"
    target="_blank"
    rel="noopener noreferrer"
    >MDN Web Docs</a
>
```

-   `href` — адреса посилання.
-   `target="_blank"` — відкриття у новій вкладці.
-   `rel="noopener noreferrer"` — безпека при відкритті нового вікна.

### Глобальні атрибути

-   `class`
-   `id`
-   `data-*` (для кастомних даних)
-   `style`
-   `tabindex`
-   `aria-*` (для доступності)

#### Приклад data-атрибутів:

```html
<div data-user-id="123" data-role="admin">...</div>
```

#### Приклад aria-атрибуту:

```html
<button aria-label="Закрити діалог">✖</button>
```

---

## Семантичні елементи

Семантичні елементи розкривають структуру та значення контенту, підвищують доступність і SEO.

| Елемент        | Опис                 |
| -------------- | -------------------- |
| `<header>`     | Шапка сторінки       |
| `<nav>`        | Навігація            |
| `<main>`       | Основний контент     |
| `<section>`    | Розділ               |
| `<article>`    | Самостійний матеріал |
| `<aside>`      | Бічний контент       |
| `<footer>`     | Підвал сторінки      |
| `<figure>`     | Візуальний контент   |
| `<figcaption>` | Підпис до зображення |

#### Приклад семантики:

```html
<main>
    <article>
        <h2>Новини HTML</h2>
        <p>Вийшла нова специфікація WHATWG.</p>
    </article>
    <aside>
        <h3>Корисні посилання</h3>
        <ul>
            <li><a href="https://html.spec.whatwg.org/">WHATWG HTML</a></li>
        </ul>
    </aside>
</main>
```

---

## Вкладеність і DOM

HTML елементи формують деревоподібну структуру (Document Object Model, DOM). Це основа для маніпуляцій з JavaScript та CSS.

### Схема DOM:

```
html
 ├── head
 └── body
      ├── header
      ├── main
      │    └── section
      └── footer
```

### Взаємодія з DOM через JavaScript:

```js
// Знаходження елемента за id
const header = document.getElementById("main-header");

// Додавання класу
header.classList.add("active");

// Зміна тексту
header.textContent = "Новий заголовок";
```

#### Візуалізація структури DOM

![DOM parsing diagram](https://www.guvi.in/blog/wp-content/uploads/2024/07/5-2048x1072.png)

---

## Мультимедіа

HTML підтримує зображення, відео, аудіо та SVG.

```html
<img src="logo.svg" alt="Логотип" width="100" />
<video controls width="400">
    <source src="movie.mp4" type="video/mp4" />
    Вибачте, ваш браузер не підтримує відео.
</video>
<audio controls>
    <source src="sound.mp3" type="audio/mpeg" />
    Ваш браузер не підтримує аудіо.
</audio>
```

### Атрибути для оптимізації:

-   `loading="lazy"` — ліниве завантаження
-   `srcset` — адаптивні зображення
-   `type` — формат файла

---

## Графіка та SVG

SVG (Scalable Vector Graphics) — векторна графіка для web.

#### Приклад SVG:

```html
<svg width="100" height="100">
    <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
</svg>
```

#### Інтеграція SVG в HTML:

-   Інлайн SVG (як вище)
-   Через тег `<img src="graphic.svg" />`
-   Через CSS як background

---

## Форми та введення даних

Форми — основний засіб для введення даних користувачем.

```html
<form action="/submit" method="POST">
    <label for="name">Ім'я:</label>
    <input
        type="text"
        id="name"
        name="name"
        required
        minlength="2"
        maxlength="20"
        autocomplete="name"
    />

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required />

    <label for="age">Вік:</label>
    <input type="number" id="age" name="age" min="18" max="100" />

    <button type="submit">Відправити</button>
</form>
```

### Нові можливості форм (HTML5+):

-   Валідація (`required`, `pattern`, `minlength`, `maxlength`)
-   Типи полів (`email`, `number`, `date`, `range`, `color`)
-   Автозаповнення (`autocomplete`)
-   Адаптивні форми для мобільних пристроїв
-   `datalist`, `inputmode`, `step`

#### Приклад використання `datalist`:

```html
<label for="browser">Вибери браузер:</label>
<input list="browsers" id="browser" name="browser" />
<datalist id="browsers">
    <option value="Chrome"></option>
    <option value="Firefox"></option>
    <option value="Edge"></option>
    <option value="Safari"></option>
</datalist>
```

---

## Accessibility (доступність)

Доступність (accessibility, a11y) — критично важлива для сучасного HTML.

### Основні принципи:

-   Використання семантичних тегів
-   Атрибути `aria-*` для опису елементів
-   Текстові альтернативи для зображень (`alt`)
-   Логічна структура документа
-   Фокусування (tabindex)
-   Контрастність контенту

#### Приклад:

```html
<img src="profile.jpg" alt="Фото профілю користувача" />
<nav aria-label="Основна навігація">
    <ul>
        <li><a href="#about">Про нас</a></li>
    </ul>
</nav>
<button aria-label="Закрити" tabindex="0">✖</button>
```

#### Перевірка доступності:

-   [axe DevTools](https://www.deque.com/axe/devtools/)
-   [Wave Evaluation Tool](https://wave.webaim.org/)
-   [MDN Accessibility](https://developer.mozilla.org/en-US/docs/Web/Accessibility)

---

## SEO-оптимізація

HTML впливає на SEO (Search Engine Optimization):

-   Семантична розмітка (`<main>`, `<article>`)
-   Коректні теги заголовків (`<h1>`, `<h2>`)
-   Мета-теги (`meta name="description"`)
-   Чисті URL та атрибути `alt`, `title`
-   Використання Open Graph, Twitter Cards

#### Приклад:

```html
<title>HTML: Конспект 2024</title>
<meta
    name="description"
    content="Глибокий конспект сучасного HTML для розробників, 2024+."
/>
<meta property="og:title" content="HTML: Конспект 2024" />
<meta
    property="og:description"
    content="Глибокий конспект сучасного HTML для розробників."
/>
<meta name="twitter:card" content="summary" />
```

---

## Безпека HTML

HTML не є джерелом небезпеки, але може спричинити уразливості при інтеграції з JavaScript.

### Ключові аспекти:

-   Escape user input (уникати XSS)
-   Використовувати `rel="noopener noreferrer"` для зовнішніх посилань
-   Валідувати дані форм на сервері
-   Не інжектити дані напряму у DOM

#### Приклад захисту від XSS:

```js
// Очистка введення користувача (коментар українською)
const safeInput = input.replace(/</g, "&lt;").replace(/>/g, "&gt;");
```

#### Кращі практики безпеки:

-   Використовуй CSP (Content Security Policy)
-   Уникай `innerHTML` для вставки даних
-   Завжди оновлюй фреймворки до останніх версій

---

## Performance (продуктивність)

HTML впливає на швидкість завантаження сторінки.

### Оптимізація:

-   Легка структура документа
-   Ліниве завантаження зображень (`loading="lazy"`)
-   Міграція до сучасних форматів (WebP, AVIF)
-   Використання CDN для ресурсів
-   Мінімізація DOM-елементів

#### Приклад:

```html
<img src="image.webp" alt="Зображення" loading="lazy" />
```

#### Performance traps:

-   Занадто глибока вкладеність DOM
-   Вставка великих inline-скриптів
-   Застарілі формати зображень

---

## Внутрішні механізми: робота HTML

### Як браузер обробляє HTML:

1. **Парсинг** — браузер перетворює HTML у DOM-дерево.
2. **Семантичний аналіз** — визначення ролей елементів.
3. **Рендеринг** — побудова візуального представлення.
4. **Інтеграція з CSS та JavaScript**.
5. **Оптимізація** — браузери оптимізують DOM для швидкої роботи JavaScript.

#### Event loop та взаємодія із JS:

-   JS-блокування рендеру (краще використовувати `defer` або `async` для скриптів).
-   Маніпуляція DOM через API.
-   Очікування подій (event listeners).

#### Memory management:

-   Кожен DOM-елемент — об'єкт у пам'яті браузера.
-   Garbage collection — автоматичне очищення непотрібних елементів.

#### Візуалізація процесу рендерингу

```
HTML -> DOM -> CSSOM -> Render Tree -> Layout -> Paint -> Composite
```

---

## Підводні камені, глибокі концепції

### Часті помилки:

-   Порушення вкладеності елементів (`<li>` тільки всередині `<ul>/<ol>`)
-   Відсутність alt у зображеннях
-   Зловживання `<div>` замість семантики
-   Дублювання id

### Глибокі концепції:

-   **Custom Elements** (Web Components): створення власних тегів
-   **Shadow DOM**: інкапсуляція стилів та логіки
-   **Template** та **Slot** для гнучкого контенту
-   **Performance traps**: великі DOM-дерева, reflow, repaint

#### Візуалізація Shadow DOM

```
<custom-element>
  #shadow-root
    <style>...</style>
    <div>Shadow content</div>
</custom-element>
```

#### Приклад Custom Element:

```js
// Коментар українською: створення власного елемента
class MyGreeting extends HTMLElement {
    connectedCallback() {
        this.innerHTML = `<p>Вітаю, це custom element!</p>`;
    }
}
customElements.define("my-greeting", MyGreeting);
```

```html
<my-greeting></my-greeting>
```

#### Приклад використання шаблонів:

```html
<template id="user-card">
    <div class="card">
        <img src="" alt="Фото" />
        <h3></h3>
    </div>
</template>
```

---

## Web Components: Custom Elements, Shadow DOM

### Основи:

-   **Custom Elements** — створення власних HTML-тегів з поведінкою.
-   **Shadow DOM** — ізольований DOM для інкапсуляції стилів і логіки.
-   **HTML Templates** — шаблони для повторного використання.

#### Приклад Web Component з Shadow DOM:

```js
class UserCard extends HTMLElement {
    constructor() {
        super();
        this.attachShadow({ mode: "open" });
        this.shadowRoot.innerHTML = `
      <style>
        .card { border: 1px solid #ccc; padding: 10px; border-radius: 8px; }
      </style>
      <div class="card">
        <img src="avatar.png" alt="Аватар" width="40">
        <h3>Ім'я користувача</h3>
      </div>
    `;
    }
}
customElements.define("user-card", UserCard);
```

```html
<user-card></user-card>
```

#### Пояснення:

-   Всі стилі й контент всередині Shadow DOM не впливають на решту сторінки.
-   Компоненти можна реюзати у фреймворках (React, Vue) або Vanilla JS.

---

## Best practices (кращі практики)

-   Використовуй семантичні елементи для структури (`header`, `main`, `nav`, `footer`, `section`, `article`)
-   Завжди додавай описові alt-тексти для зображень
-   Валідуй HTML через [validator.w3.org](https://validator.w3.org/)
-   Розділяй контент, презентацію й логіку (HTML, CSS, JS окремо)
-   Завантажуй скрипти асинхронно (`defer`, `async`)
-   Використовуй сучасні формати ресурсів (WebP, SVG)
-   Тестуй доступність (screen readers, keyboard navigation)
-   Уникай дублювання ідентифікаторів (id)
-   Дотримуйся правил вкладеності тегів
-   Всі дані з форм — валідуй на сервері, навіть якщо вже є клієнтська валідація

---

## Корисні ресурси та документація

-   [WHATWG HTML Living Standard](https://html.spec.whatwg.org/)
-   [MDN HTML Reference](https://developer.mozilla.org/en-US/docs/Web/HTML)
-   [HTML5 Accessibility](https://www.w3.org/WAI/)
-   [Google Web Fundamentals](https://web.dev/)
-   [HTML5 Security Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html)
-   [HTML Validator](https://validator.w3.org/)
-   [Web Components Guide](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
-   [SVG Basics](https://developer.mozilla.org/en-US/docs/Web/SVG)

---

## Короткий підсумок

HTML — це не просто набір тегів, а фундамент для створення сучасних web-додатків. Семантика, доступність, продуктивність та безпека — ключові принципи HTML у 2024 році. Вивчення внутрішніх механізмів (DOM, рендеринг, Web Components, Shadow DOM) дозволяє писати професійний, масштабований і безпечний код. Дотримуйся best practices, оновлюй знання та використовуй офіційні ресурси для зростання як web-розробник!

---
