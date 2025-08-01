# ПОВНИЙ HTML КУРС: ВІД НОВАЧКА ДО ПРО

---

## Зміст

1. [Вступ до HTML](#вступ)
2. [Структура HTML-документа](#структура)
3. [Основні теги та робота з текстом](#текст)
4. [Гіперпосилання, зображення, списки](#гіперпосилання)
5. [Таблиці: створення та оформлення](#таблиці)
6. [Форми: основи та валідація](#форми)
7. [Семантична розмітка](#семантика)
8. [Медіа: відео, аудіо, iFrame, SVG](#медіа)
9. [Атрибути та глобальні атрибути](#атрибути)
10. [Інтеграція з CSS та JavaScript](#css-js)
11. [Адаптивний дизайн та мета-теги](#адаптив)
12. [SEO і мікророзмітка](#seo)
13. [Просунуті фішки HTML5](#про)
14. [Типові помилки та FAQ](#помилки)
15. [Практика: завдання та проєкти](#практика)
16. [Тести для самоперевірки](#тести)
17. [Корисні ресурси](#ресурси)

---

<a name="вступ"></a>

## 1. Вступ до HTML

**HTML (HyperText Markup Language)** — це “скелет” будь-якої веб-сторінки.  
Він визначає структуру, а зовнішній вигляд забезпечує CSS, а функціонал — JavaScript.

**HTML5** — найактуальніший стандарт.  
Сайти без HTML не існують!

---

<a name="структура"></a>

## 2. Структура HTML-документа

```html
<!DOCTYPE html>
<html lang="uk">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width,initial-scale=1.0" />
        <title>Назва сторінки</title>
    </head>
    <body>
        <!-- Контент сайту тут -->
    </body>
</html>
```

**Розбір:**

-   `<!DOCTYPE html>` — вказує на HTML5
-   `<html lang="uk">` — основний контейнер, мова документа
-   `<head>` — службова інфо (мета, стилі, скрипти)
-   `<body>` — те, що бачить користувач

---

<a name="текст"></a>

## 3. Основні теги та робота з текстом

### Заголовки

```html
<h1>Головний заголовок</h1>
<h2>Підзаголовок</h2>
...
<h6>Найменший заголовок</h6>
```

### Абзаци, перенос, лінія

```html
<p>Це абзац.</p>
<br />
<hr />
```

### Форматування тексту

```html
<strong>Жирний</strong>
<em>Курсив</em>
<u>Підкреслення (не рекомендується для простої розмітки)</u>
<mark>Виділено</mark>
<del>Закреслено</del>
<code>Код</code>
<pre>Збереження форматування</pre>
<blockquote>Цитата</blockquote>
```

### Спецсимволи

```html
&copy; &nbsp; &gt; &lt; &amp; &quot;
```

---

<a name="гіперпосилання"></a>

## 4. Гіперпосилання, зображення, списки

### Гіперпосилання

```html
<a href="https://example.com" target="_blank" title="Відкрити в новій вкладці"
    >Сайт</a
>
<a href="#section3">Перехід до секції 3 (якір)</a>
```

### Зображення

```html
<img src="logo.png" alt="Логотип" width="200" height="100" />
```

### Списки

**Ненумерований:**

```html
<ul>
    <li>Перший</li>
    <li>Другий</li>
</ul>
```

**Нумерований:**

```html
<ol>
    <li>Перший</li>
    <li>Другий</li>
</ol>
```

**Описовий:**

```html
<dl>
    <dt>Термін</dt>
    <dd>Пояснення</dd>
</dl>
```

---

<a name="таблиці"></a>

## 5. Таблиці: створення та оформлення

```html
<table>
    <caption>
        Розклад
    </caption>
    <thead>
        <tr>
            <th>День</th>
            <th>Час</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Пн</td>
            <td>10:00</td>
        </tr>
        <tr>
            <td>Вт</td>
            <td>12:00</td>
        </tr>
    </tbody>
</table>
```

### Об’єднання комірок

```html
<td colspan="2">Об'єднано 2 колонки</td>
<td rowspan="2">Об'єднано 2 рядки</td>
```

---

<a name="форми"></a>

## 6. Форми: основи та валідація

```html
<form action="/submit" method="post">
    <label for="name">Ім'я:</label>
    <input type="text" id="name" name="name" required />

    <label>
        <input type="checkbox" name="agree" /> Погоджуюсь з правилами
    </label>

    <input type="submit" value="Відправити" />
</form>
```

### Типи `<input>`

-   text, password, email, number, date, file, radio, checkbox, submit, reset, hidden, color, range, tel, url, search

### textarea, select

```html
<textarea name="message" rows="4"></textarea>
<select name="city">
    <option value="kyiv">Київ</option>
    <option value="lviv">Львів</option>
</select>
```

### Валідація HTML5

-   `required`, `min`, `max`, `pattern`, `maxlength`, `minlength`, `step`

---

<a name="семантика"></a>

## 7. Семантична розмітка

**Для кращого SEO та доступності використовуй семантичні теги:**

```html
<header>Шапка</header>
<nav>Головне меню</nav>
<main>Основний контент</main>
<article>Окрема стаття</article>
<section>Секція</section>
<aside>Бічна панель</aside>
<footer>Підвал</footer>
```

---

<a name="медіа"></a>

## 8. Медіа: відео, аудіо, iFrame, SVG

### Відео

```html
<video src="movie.mp4" controls poster="preview.jpg" width="400">
    Ваш браузер не підтримує відео.
</video>
```

### Аудіо

```html
<audio src="audio.mp3" controls></audio>
```

### iFrame

```html
<iframe
    src="https://www.youtube.com/embed/ID"
    width="560"
    height="315"
    allowfullscreen
></iframe>
```

### SVG

```html
<svg width="100" height="100">
    <circle cx="50" cy="50" r="40" fill="blue" />
</svg>
```

---

<a name="атрибути"></a>

## 9. Атрибути та глобальні атрибути

-   `id`, `class`, `style`, `title`, `lang`, `tabindex`, `hidden`, `data-*` (кастомні дані)
-   Приклад:

```html
<div id="main" class="container" style="color:red;" data-user="12"></div>
```

---

<a name="css-js"></a>

## 10. Інтеграція з CSS та JavaScript

### CSS

-   Внутрішній стиль:
    ```html
    <style>
        body {
            background: #eee;
        }
    </style>
    ```
-   Зовнішній файл:
    ```html
    <link rel="stylesheet" href="style.css" />
    ```

### JavaScript

-   Внутрішній код:
    ```html
    <script>
        alert("Привіт!");
    </script>
    ```
-   Підключення файлу:
    ```html
    <script src="script.js"></script>
    ```

---

<a name="адаптив"></a>

## 11. Адаптивний дизайн та мета-теги

-   Мета-тег для адаптивності:

    ```html
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    ```

-   Контейнер для адаптиву: `<div class="container">...</div>`

-   Для адаптивності використовуй media queries у CSS (приклад):
    ```css
    @media (max-width: 600px) {
        body {
            font-size: 16px;
        }
    }
    ```

---

<a name="seo"></a>

## 12. SEO і мікророзмітка

-   **Заголовки**: `<h1>` лише один на сторінці!
-   **title** та **meta description** повинні бути унікальні
-   **alt** у зображень
-   **robots.txt, sitemap.xml** — для пошуковиків

### Open Graph (для соцмереж):

```html
<meta property="og:title" content="Заголовок сторінки" />
<meta property="og:description" content="Опис" />
<meta property="og:image" content="link.png" />
<meta property="og:type" content="website" />
<meta property="og:url" content="https://site.com" />
```

### schema.org (JSON-LD):

```html
<script type="application/ld+json">
    {
        "@context": "https://schema.org",
        "@type": "Article",
        "headline": "Заголовок статті",
        "datePublished": "2025-08-01"
    }
</script>
```

---

<a name="про"></a>

## 13. Просунуті фішки HTML5

-   **localStorage/sessionStorage**: збереження даних у браузері (JS)
-   **Canvas**: малювання графіки
-   **progress/meter**: індикатори

```html
<progress value="70" max="100"></progress> <meter value="0.6">60%</meter>
```

-   **details/summary**: прихований текст

```html
<details>
    <summary>Деталі</summary>
    Тут прихований текст!
</details>
```

-   **template**: заготовка для JS

```html
<template id="tmpl">
    <p>Шаблонний текст</p>
</template>
```

---

<a name="помилки"></a>

## 14. Типові помилки та FAQ

-   Відсутність DOCTYPE
-   Відсутній/дубльований `<h1>`
-   Неунікальні id
-   Відсутній alt у картинках
-   Використання `<b>` замість `<strong>`, `<i>` замість `<em>`
-   Некоректна вкладеність тегів
-   Відсутність мета-тегів для мобільних пристроїв

### FAQ

-   **Чи можна вкладати `<div>` у `<span>`?**

    -   Ні, `<span>` — стрічковий елемент, не містить блочних.

-   **Чи можна декілька `<h1>`?**
    -   Рекомендовано лише один `<h1>` на сторінці.

---

<a name="практика"></a>

## 15. Практика: завдання та проєкти

### 1. Візитка

Створи просту сторінку з:

-   Фото
-   Привітанням
-   Переліком навичок (список)
-   Формою для контакту

### 2. Таблиця розкладу

Створи таблицю з розкладом тижня.

### 3. Галерея

Зроби сторінку з кількома зображеннями у різних форматах.

### 4. Мультимедіа

Встав відео з YouTube, SVG-графіку, iFrame з Google Maps.

### 5. Адаптивна сторінка

Додай мета-тег viewport, зроби адаптивний макет для мобільних.

---

<a name="тести"></a>

## 16. Тести для самоперевірки

1. Навіщо потрібен DOCTYPE?
2. В чому різниця між `<strong>` і `<b>`?
3. Як створити описовий список?
4. Який атрибут зробить поле обов’язковим для заповнення?
5. Як вставити SVG-графіку?
6. Для чого потрібен мета-тег viewport?
7. Який тег використовується для статей?
8. Що таке alt у зображеннях?

---

<a name="ресурси"></a>

## 17. Корисні ресурси

-   [MDN HTML](https://developer.mozilla.org/uk/docs/Web/HTML)
-   [w3schools HTML](https://www.w3schools.com/html/)
-   [htmlreference.io](https://htmlreference.io/)
-   [validator.w3.org](https://validator.w3.org/)
-   [freecodecamp.org (ukr)](https://uk.freecodecamp.org/)

---

**Успіхів у вивченні HTML! Це лише початок — опановуй практикою!**
