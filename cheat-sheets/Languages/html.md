# HTML

HTML — мова розмітки для створення структури веб-сторінок.

## Категорія: Основні теги та структура

| Команда/метод           | Опис              | Приклад/Аутпут                           |
| ----------------------- | ----------------- | ---------------------------------------- |
| <!DOCTYPE html>         | тип документа     | <!DOCTYPE html>                          |
| <html>...</html>        | кореневий елемент | <html>...</html>                         |
| <head>...</head>        | метадані          | <head><title>Title</title></head>        |
| <body>...</body>        | вміст сторінки    | <body>...</body>                         |
| <title>                 | заголовок вкладки | <title>My Page</title>                   |
| <meta charset="utf-8">  | кодування         | <meta charset="utf-8">                   |
| <link rel="stylesheet"> | підключення CSS   | <link rel="stylesheet" href="style.css"> |
| <script src="...">      | підключення JS    | <script src="app.js"></script>           |

## Категорія: Текст і структура

| Команда/метод  | Опис                | Приклад/Аутпут          |
| -------------- | ------------------- | ----------------------- |
| <h1>…<h6>      | заголовки           | <h1>Заголовок</h1>      |
| <p>            | абзац               | <p>Текст</p>            |
| <a href="url"> | посилання           | <a href="/">Головна</a> |
| <ul>/<ol>/<li> | списки              | <ul><li>Пункт</li></ul> |
| <div>          | блок                | <div>...</div>          |
| <span>         | рядковий елемент    | <span>текст</span>      |
| <br>           | перенесення         | Текст<br>Новий рядок    |
| <hr>           | горизонтальна лінія | <hr>                    |

## Категорія: Зображення, медіа, таблиці

| Команда/метод           | Опис                 | Приклад/Аутпут                                        |
| ----------------------- | -------------------- | ----------------------------------------------------- |
| <img src="...">         | зображення           | <img src="img.png" alt="desc">                        |
| <figure>/<figcaption>   | підпис до зображення | <figure><img><figcaption>Підпис</figcaption></figure> |
| <audio>/<video>         | медіа                | <audio src="a.mp3" controls></audio>                  |
| <table>/<tr>/<td>       | таблиця              | <table><tr><td>1</td></tr></table>                    |
| <thead>/<tbody>/<tfoot> | частини таблиці      | <thead>...</thead>                                    |
| <th>                    | заголовок таблиці    | <th>Заголовок</th>                                    |

## Категорія: Форми

| Команда/метод           | Опис              | Приклад/Аутпут                              |
| ----------------------- | ----------------- | ------------------------------------------- |
| <form>                  | форма             | <form action="/" method="post"></form>      |
| <input type="text">     | текстове поле     | <input type="text">                         |
| <input type="checkbox"> | чекбокс           | <input type="checkbox">                     |
| <input type="radio">    | радіокнопка       | <input type="radio">                        |
| <select>/<option>       | випадаючий список | <select><option>1</option></select>         |
| <textarea>              | багато тексту     | <textarea>Текст</textarea>                  |
| <button>                | кнопка            | <button>OK</button>                         |
| <label>                 | підпис до поля    | <label for="id">Текст</label>               |
| <fieldset>/<legend>     | групування полів  | <fieldset><legend>Група</legend></fieldset> |

## Категорія: Семантичні теги

| Команда/метод | Опис               | Приклад/Аутпут         |
| ------------- | ------------------ | ---------------------- |
| <header>      | шапка              | <header>...</header>   |
| <nav>         | навігація          | <nav>...</nav>         |
| <main>        | основний контент   | <main>...</main>       |
| <section>     | секція             | <section>...</section> |
| <article>     | стаття             | <article>...</article> |
| <aside>       | додатковий контент | <aside>...</aside>     |
| <footer>      | підвал             | <footer>...</footer>   |

## Категорія: Атрибути та інше

| Команда/метод     | Опис                       | Приклад/Аутпут                      |
| ----------------- | -------------------------- | ----------------------------------- |
| id/class          | ідентифікатор/клас         | <div id="main" class="box">         |
| data-\*           | дата-атрибут               | <div data-id="1">                   |
| alt/title         | опис/підказка              | <img alt="desc" title="підказка">   |
| tabindex/aria-\*  | доступність                | <button tabindex="0" aria-label=""> |
| hidden/disabled   | приховано/неактивно        | <input hidden disabled>             |
| required/readonly | обов'язково/тільки читання | <input required readonly>           |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
