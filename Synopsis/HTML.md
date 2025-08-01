# Ultimate HTML Cheat Sheet

## ⭐ Description

HTML (HyperText Markup Language) is the standard markup language for creating web pages. It defines the structure of content and is the foundation of every website.

## ⭐ Relationship With Other Technologies

-   CSS/SCSS styles HTML elements.
-   JS/TS manipulates the DOM, created by HTML.
-   Vue, Angular, Nuxt, Electron use HTML-based templates for UI.
-   Express/Node serve/generate HTML.
-   Django/Python render HTML via templates.
-   Electron uses HTML for desktop app windows.

---

## 1. Document Structure

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>Page Title</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <link rel="stylesheet" href="styles.css" />
        <script src="main.js" defer></script>
    </head>
    <body>
        <!-- Page content -->
    </body>
</html>
```

### Key Tags

-   `<!DOCTYPE html>`: Declares HTML5.
-   `<html lang="en">`: Root element. `lang` for accessibility/SEO.
-   `<head>`: Metadata, links, scripts.
-   `<body>`: Visible content.

---

## 2. Text, Headings & Formatting

### Headings

```html
<h1>Title</h1>
<h2>Subtitle</h2>
<h3>Section</h3>
```

-   Use only one `<h1>` per page for SEO.

### Paragraphs & Formatting

```html
<p>Paragraph text</p>
<strong>Bold</strong>
<em>Italic</em>
<u>Underline</u>
<s>Strikethrough</s>
<mark>Highlight</mark>
<sub>Subscript</sub>
<sup>Superscript</sup>
<small>Small print</small>
<abbr title="HyperText Markup Language">HTML</abbr>
<blockquote cite="https://example.com">Quote</blockquote>
<pre>
  Preformatted text
</pre>
<code>inline code</code>
```

---

## 3. Lists

### Unordered, Ordered, Definition

```html
<ul>
    <li>Item</li>
</ul>
<ol type="I" reversed>
    <li>First</li>
    <li>Second</li>
</ol>
<dl>
    <dt>Term</dt>
    <dd>Definition</dd>
</dl>
```

-   Nest lists for complex structures.

---

## 4. Links & Navigation

```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer"
    >External Link</a
>
<nav>
    <ul>
        <li><a href="/">Home</a></li>
    </ul>
</nav>
```

-   Use `rel="noopener noreferrer"` for security with `target="_blank"`.

---

## 5. Images, Audio, Video

```html
<img src="pic.jpg" alt="Description" width="400" height="300" loading="lazy" />
<picture>
    <source srcset="pic.webp" type="image/webp" />
    <img src="pic.jpg" alt="Fallback" />
</picture>

<audio src="audio.mp3" controls loop></audio>
<video src="video.mp4" controls poster="poster.jpg" width="600"></video>
```

-   Always set `alt` for images.
-   Use `<picture>` for responsive images.

---

## 6. Tables

```html
<table>
    <caption>
        Monthly Sales
    </caption>
    <thead>
        <tr>
            <th>Month</th>
            <th>Sales</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Jan</td>
            <td>$1000</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>Total</td>
            <td>$1000</td>
        </tr>
    </tfoot>
</table>
```

-   Use `<thead>`, `<tbody>`, `<tfoot>` for accessibility and clarity.

---

## 7. Forms

```html
<form action="/submit" method="post" autocomplete="on" novalidate>
    <fieldset>
        <legend>Login</legend>
        <label for="user">Name:</label>
        <input type="text" id="user" name="user" required />
        <input type="email" name="email" placeholder="Email" />
        <input type="password" name="pwd" />
        <input type="checkbox" name="remember" /> Remember Me
        <input type="radio" name="gender" value="male" /> Male
        <input type="radio" name="gender" value="female" /> Female
        <select name="country" multiple>
            <option value="us">USA</option>
            <option value="uk">UK</option>
        </select>
        <textarea name="message" rows="4"></textarea>
        <input type="file" name="avatar" accept="image/png, image/jpeg" />
        <button type="submit">Login</button>
        <button type="reset">Reset</button>
    </fieldset>
</form>
```

-   Use `<fieldset>` & `<legend>` for grouping.
-   Always use `<label>` for accessibility.

---

## 8. Semantic Elements

```html
<header>Site header</header>
<nav>Main navigation</nav>
<main>Main content</main>
<aside>Sidebar</aside>
<article>Blog post</article>
<section>Section of content</section>
<figure>
    <img src="img.jpg" alt="" />
    <figcaption>Image caption</figcaption>
</figure>
<footer>Footer</footer>
<time datetime="2025-08-01">August 1, 2025</time>
```

-   Improves SEO and accessibility.

---

## 9. Metadata & SEO

```html
<meta charset="UTF-8" />
<meta name="description" content="Ultimate HTML Cheat Sheet" />
<meta name="keywords" content="HTML, Cheat Sheet, Web Development" />
<meta name="author" content="Ooodysseus" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<meta property="og:title" content="HTML Cheat Sheet" />
<meta property="og:image" content="preview.jpg" />
<link rel="icon" type="image/png" href="favicon.png" />
<link rel="canonical" href="https://example.com/html-cheat-sheet" />
```

---

## 10. Accessibility

-   Use semantic elements (`<main>`, `<nav>`, `<footer>`, etc.)
-   Label all form elements.
-   Use `alt` attributes for images.
-   ARIA roles for complex widgets:
    ```html
    <div role="dialog" aria-labelledby="dialog1Title"></div>
    <button aria-label="Close"></button>
    ```
-   Use keyboard-accessible elements.

---

## 11. Custom Data Attributes

```html
<div data-user-id="42" data-role="admin"></div>
```

-   Useful for passing extra info to JS.

---

## 12. Embedding & Integration

```html
<iframe
    src="https://www.youtube.com/embed/xyz"
    width="560"
    height="315"
></iframe>
<embed src="file.pdf" type="application/pdf" />
<object data="file.swf"></object>
<canvas id="draw"></canvas>
```

---

## 13. Entities

| Entity | Code      | Output |
| ------ | --------- | ------ |
| Space  | `&nbsp;`  |        |
| <      | `&lt;`    | <      |
| >      | `&gt;`    | >      |
| &      | `&amp;`   | &      |
| "      | `&quot;`  | "      |
| '      | `&apos;`  | '      |
| ©      | `&copy;`  | ©      |
| ®      | `&reg;`   | ®      |
| ™      | `&trade;` | ™      |

---

## 14. Comments

```html
<!-- This is an HTML comment -->
```

---

## 15. Advanced Features

-   `<template>`: Invisible content for client-side rendering.
-   `<noscript>`: Fallback when JS is disabled.
-   `<dialog>`: Native modal dialogs.
-   `<details>` & `<summary>`: Expand/collapse sections.

---

## 16. Best Practices

-   Use semantic tags for structure and SEO.
-   Accessibility: label everything, test with screen readers.
-   Separate HTML (structure), CSS (style), JS (behavior).
-   Validate your HTML markup (W3C validator).
-   Use proper indentation and comments.
-   Avoid inline styles/scripts.

---

## 17. Tools & Resources

-   [MDN HTML Reference](https://developer.mozilla.org/en-US/docs/Web/HTML)
-   [W3C Validator](https://validator.w3.org/)
-   [Can I use](https://caniuse.com/)
-   [Google Lighthouse](https://developers.google.com/web/tools/lighthouse)

---

## 18. Comparison Table

| Feature        | HTML | CSS/SCSS | JS/TS | Vue/Angular/Nuxt | Express/Node | Django/Python  | Electron |
| -------------- | ---- | -------- | ----- | ---------------- | ------------ | -------------- | -------- |
| Structure      | ✔️   |          |       | ✔️ (templates)   | ✔️ (serve)   | ✔️ (templates) | ✔️ (UI)  |
| Styling        |      | ✔️       |       | ✔️ (scoped)      | (static)     | (static)       | ✔️       |
| Logic/Behavior |      |          | ✔️    | ✔️               | ✔️           | ✔️             | ✔️       |
| Desktop        |      | ✔️       | ✔️    |                  |              |                | ✔️       |
