# CSS/SCSS

CSS — мова стилів для оформлення веб-сторінок. SCSS — надмножина CSS з підтримкою змінних, вкладеності, міксинів, функцій.

## Категорія: Основи CSS

| Команда/метод        | Опис                 | Приклад/Аутпут                    |
| -------------------- | -------------------- | --------------------------------- |
| color                | колір тексту         | color: red;                       |
| background-color     | фон                  | background-color: #fff;           |
| font-size            | розмір шрифту        | font-size: 16px;                  |
| font-family          | шрифт                | font-family: Arial, sans-serif;   |
| font-weight          | товщина шрифту       | font-weight: bold;                |
| text-align           | вирівнювання тексту  | text-align: center;               |
| line-height          | міжрядковий інтервал | line-height: 1.5;                 |
| margin/padding       | зовн./внутр. відступ | margin: 10px; padding: 5px;       |
| border               | рамка                | border: 1px solid #000;           |
| border-radius        | скруглення           | border-radius: 8px;               |
| box-shadow           | тінь                 | box-shadow: 0 2px 8px #0003;      |
| width/height         | розміри              | width: 100px; height: 50px;       |
| min/max-width/height | мін/макс розмір      | min-width: 200px;                 |
| display              | тип відображення     | display: flex;                    |
| visibility/opacity   | видимість/прозорість | opacity: 0.5; visibility: hidden; |
| cursor               | курсор               | cursor: pointer;                  |
| overflow             | обрізка контенту     | overflow: hidden;                 |
| object-fit           | обрізка зображення   | object-fit: cover;                |

## Категорія: Позиціонування

| Команда/метод         | Опис               | Приклад/Аутпут             |
| --------------------- | ------------------ | -------------------------- |
| position              | тип позиціонування | position: absolute;        |
| top/right/bottom/left | координати         | top: 0; left: 10px;        |
| z-index               | шарування          | z-index: 10;               |
| float/clear           | обтікання          | float: right; clear: both; |
| vertical-align        | вирівнювання по Y  | vertical-align: middle;    |

## Категорія: Селектори та специфічність

| Команда/метод         | Опис           | Приклад/Аутпут               |
| --------------------- | -------------- | ---------------------------- |
| .class                | клас           | .btn { ... }                 |
| #id                   | ідентифікатор  | #main { ... }                |
| element               | тег            | p { ... }                    |
| [attr=value]          | атрибут        | input[type="text"] { ... }   |
| :hover/:active/:focus | псевдокласи    | a:hover { ... }              |
| :nth-child(2n)        | n-й елемент    | li:nth-child(2n) { ... }     |
| ::before/::after      | псевдоелементи | p::before {content:"-";}     |
| >, +, ~               | комбінатори    | div > p { ... }              |
| \*, :not(), :root     | універсальні   | \* {box-sizing: border-box;} |

## Категорія: Flexbox

| Команда/метод          | Опис                | Приклад/Аутпут                |
| ---------------------- | ------------------- | ----------------------------- |
| display: flex          | flex-контейнер      | display: flex;                |
| flex-direction         | напрямок            | flex-direction: row;          |
| justify-content        | вирівнювання по X   | justify-content: center;      |
| align-items            | вирівнювання по Y   | align-items: center;          |
| flex-wrap              | перенесення         | flex-wrap: wrap;              |
| align-content          | вирівнювання рядків | align-content: space-between; |
| gap                    | відступи            | gap: 10px;                    |
| flex-grow/shrink/basis | розміри елементів   | flex: 1 0 100px;              |
| order                  | порядок елементів   | order: 2;                     |

## Категорія: Grid

| Команда/метод             | Опис             | Приклад/Аутпут                  |
| ------------------------- | ---------------- | ------------------------------- |
| display: grid             | grid-контейнер   | display: grid;                  |
| grid-template-columns     | колонки          | grid-template-columns: 1fr 2fr; |
| grid-template-rows        | рядки            | grid-template-rows: 100px auto; |
| grid-gap                  | відступи         | grid-gap: 10px;                 |
| grid-column/row           | позиція елемента | grid-column: 1/3;               |
| grid-area                 | область          | grid-area: header;              |
| justify-items/align-items | вирівнювання     | justify-items: center;          |

## Категорія: Адаптивність та медіа-запити

| Команда/метод | Опис                | Приклад/Аутпут                       |
| ------------- | ------------------- | ------------------------------------ |
| @media        | медіа-запит         | @media (max-width:600px) { ... }     |
| vw/vh/%       | відносні розміри    | width: 50vw; height: 30vh;           |
| clamp()       | гнучкий розмір      | font-size: clamp(12px,2vw,20px);     |
| @supports     | перевірка підтримки | @supports (display: grid) { ... }    |
| @container    | контейнер-запит     | @container (min-width:400px) { ... } |

## Категорія: Анімації та трансформації

| Команда/метод | Опис          | Приклад/Аутпут                      |
| ------------- | ------------- | ----------------------------------- |
| transition    | плавна зміна  | transition: all 0.3s;               |
| transform     | трансформація | transform: scale(1.2) rotate(5deg); |
| animation     | анімація      | animation: fade 1s infinite;        |
| @keyframes    | ключові кадри | @keyframes fade {0%{opacity:0}}     |
| will-change   | оптимізація   | will-change: transform;             |

## Категорія: Робота з background

| Команда/метод       | Опис              | Приклад/Аутпут                 |
| ------------------- | ----------------- | ------------------------------ |
| background-image    | фонове зображення | background-image: url(bg.png); |
| background-size     | розмір фону       | background-size: cover;        |
| background-position | позиція фону      | background-position: center;   |
| background-repeat   | повторення        | background-repeat: no-repeat;  |

## Категорія: Робота зі шрифтами

| Команда/метод  | Опис                  | Приклад/Аутпут                               |
| -------------- | --------------------- | -------------------------------------------- |
| @font-face     | підключення шрифту    | @font-face {font-family:My;src:url(a.woff);} |
| text-transform | регістр               | text-transform: uppercase;                   |
| letter-spacing | інтервал між літерами | letter-spacing: 2px;                         |
| word-break     | перенесення слів      | word-break: break-all;                       |

## Категорія: SCSS — змінні, вкладеність, міксини, функції

| Команда/метод        | Опис                | Приклад/Аутпут                       |
| -------------------- | ------------------- | ------------------------------------ |
| $color: #333;        | змінна              | $color: #333;                        |
| .parent { .child {}} | вкладеність         | .nav { .item { ... } }               |
| @mixin name { ... }  | міксин              | @mixin btn { ... }                   |
| @include name;       | підключити міксин   | @include btn;                        |
| @extend .class;      | наслідування стилів | @extend .btn;                        |
| @function name($a)   | функція             | @function pow($x) { @return $x*$x; } |
| @return              | повернути значення  | @return $a + 1;                      |
| @if/@else            | умовні конструкції  | @if $a > 0 { ... }                   |
| @for/@each           | цикли               | @for $i from 1 through 3 { ... }     |
| @import              | імпорт файлу        | @import 'vars';                      |
| #{...}               | інтерполяція        | .icon-#{$name} { ... }               |

## Категорія: Best practices та інше

| Команда/метод          | Опис                  | Приклад/Аутпут               |
| ---------------------- | --------------------- | ---------------------------- |
| box-sizing: border-box | універсальний розмір  | \* {box-sizing: border-box;} |
| :root { --var: ... }   | CSS-змінні            | :root {--main: #333;}        |
| var(--main)            | використання змінної  | color: var(--main);          |
| outline                | обводка (доступність) | outline: 2px solid blue;     |
| user-select            | заборона виділення    | user-select: none;           |
| pointer-events         | події миші            | pointer-events: none;        |
| content                | вміст псевдоелемента  | content: "→";                |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
> | .parent { .child {}} | вкладеність | .nav { .item { ... } } |
> | @mixin name { ... } | міксин | @mixin btn { ... } |
> | @include name; | підключити міксин | @include btn; |
> | @extend .class; | наслідування стилів | @extend .btn; |
> | @if/@else | умовні конструкції | @if $a > 0 { ... } |
> | @for/@each | цикли | @for $i from 1 through 3 { ... }|

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
