# Адаптивність і респонсивність: media queries, mobile-first, одиниці виміру

## Вступ

Адаптивність і респонсивність — ключові принципи сучасного вебу. Вони забезпечують коректне відображення сайту на різних пристроях, роздільних здатностях, орієнтаціях, підвищують UX і доступність.

## Історія/Походження

Перші сайти були фіксованими. З розвитком мобільних пристроїв з’явилися медіа-запити, гнучкі layout, нові одиниці виміру, підходи mobile-first, container queries.

### Віхи розвитку адаптивності

-   **CSS2:** медіа-типи (screen, print)
-   **CSS3:** media queries, viewport units, flexible units
-   **2020+:** container queries, clamp, min/max

## Основний матеріал

### Media queries

-   @media — основний синтаксис
-   Властивості: min-width, max-width, orientation, resolution, aspect-ratio
-   Можна комбінувати умови через and, not, only

#### Приклад media queries

```css
@media (max-width: 600px) {
    .container {
        padding: 8px;
        font-size: 16px;
    }
}
@media (orientation: landscape) {
    .gallery {
        grid-template-columns: 1fr 1fr 1fr;
    }
}
```

### Mobile-first

-   Спочатку стилі для мобільних, потім для більших екранів
-   Краще для продуктивності, UX, підтримки

#### Приклад mobile-first

```css
.container {
    padding: 8px;
}
@media (min-width: 600px) {
    .container {
        padding: 24px;
    }
}
```

### Одиниці виміру

-   px — пікселі
-   em, rem — відносно шрифту
-   % — відсотки
-   vw, vh — viewport width/height
-   vmin, vmax — мін/макс viewport
-   fr — фракція для Grid
-   ch, ex — ширина символу, висота x
-   clamp, min, max — гнучкі обмеження

#### Приклад одиниць виміру

```css
.box {
    width: 80vw;
    font-size: 2rem;
    padding: 2em;
    max-width: 600px;
}
```

### Неочевидний приклад: container queries

```css
@container (min-width: 400px) {
    .card {
        font-size: 1.2em;
    }
}
```

### Неочевидний приклад: clamp

```css
.title {
    font-size: clamp(1.2rem, 2vw, 2.4rem);
}
```

### Неочевидний приклад: aspect-ratio

```css
.img {
    aspect-ratio: 16/9;
}
```

### Неочевидний приклад: prefers-color-scheme

```css
@media (prefers-color-scheme: dark) {
    body {
        background: #222;
        color: #eee;
    }
}
```

## Пояснення під капотом

Браузер парсить CSS, створює CSSOM, застосовує media queries, одиниці виміру, оптимізує рендеринг, інтегрує з DOM, API (ResizeObserver, Container Queries).

### Як працює адаптивність у рушії

Media queries, viewport units, container queries інтегруються з DOM, визначають layout, розміри, стилі для різних пристроїв, впливають на продуктивність, UX, доступність.

## Нюанси та підводні камені

-   Відсутність mobile-first — поганий UX на мобільних
-   Надмірне використання px — погана адаптивність
-   Відсутність clamp/min/max — некоректні розміри
-   Відсутність aspect-ratio — неправильне відображення
-   Відсутність prefers-color-scheme — некоректна тема
-   Відсутність container queries — складна підтримка

## Діаграми

```mermaid
graph TD
    MEDIA[@media] --> WIDTH[min/max-width]
    MEDIA --> ORIENT[orientation]
    MEDIA --> RES[resolution]
    MEDIA --> COLOR[prefers-color-scheme]
    UNITS[Одиниці] --> PX[px]
    UNITS --> EM[em]
    UNITS --> REM[rem]
    UNITS --> VW[vw]
    UNITS --> VH[vh]
    UNITS --> FR[fr]
    UNITS --> CLAMP[clamp]
    UNITS --> ASPECT[aspect-ratio]
    UNITS --> CONTAINER[container queries]
```

## Приклад застосування в реальних проєктах

-   Блоги — mobile-first, clamp, prefers-color-scheme
-   E-commerce — media queries, aspect-ratio, viewport units
-   SPA — container queries, гнучкі layout
-   Галереї — grid, minmax, aspect-ratio
-   Корпоративні сайти — адаптивність, темізація

### Кейс: UX

Mobile-first, clamp, viewport units — для зручності користувача.

### Кейс: продуктивність

Гнучкі одиниці, container queries, оптимізація стилів.

## Крос-посилання

-   [CSS: layout](./04-layout.md)
-   [CSS: бокс-модель](./03-box-model.md)
-   [Best practices](../HTML/10-best-practices.md)
-   [HTML: медіа](../HTML/05-media.md)

## Підсумок

-   Адаптивність і респонсивність — основа сучасного CSS
-   Media queries, mobile-first, одиниці виміру — ключові механізми
-   Неочевидні приклади — для гнучкості, продуктивності, доступності
