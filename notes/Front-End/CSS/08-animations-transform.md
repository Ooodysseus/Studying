# Анімації та трансформації: transition, keyframes, transform

## Вступ

Анімації та трансформації — це інструменти CSS для створення динаміки, інтерактивності, акцентів, покращення UX. Вони дозволяють плавно змінювати властивості, переміщати, масштабувати, обертати елементи.

## Історія/Походження

Перші анімації реалізовувалися через JS. З появою CSS3 з’явилися transition, transform, keyframes, animation, що дозволило створювати складні ефекти без JS.

### Віхи розвитку анімацій

-   **CSS2:** прості transition через JS
-   **CSS3:** transition, transform, animation, keyframes
-   **2020+:** motion-path, prefers-reduced-motion, custom properties

## Основний матеріал

### Transition

-   transition — плавна зміна властивостей
-   Властивості: transition-property, transition-duration, transition-timing-function, transition-delay

#### Приклад transition

```css
.button {
    background: #0077cc;
    transition: background 0.3s ease;
}
.button:hover {
    background: #00cc77;
}
```

### Transform

-   transform — зміна положення, розміру, обертання, нахилу
-   Функції: translate, scale, rotate, skew, matrix

#### Приклад transform

```css
.box {
    transform: translateX(50px) scale(1.2) rotate(15deg);
}
```

### Animation та keyframes

-   animation — складні анімації через keyframes
-   Властивості: animation-name, animation-duration, animation-timing-function, animation-delay, animation-iteration-count, animation-direction, animation-fill-mode, animation-play-state

#### Приклад animation

```css
@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}
.fade {
    animation: fadeIn 1s ease-in;
}
```

### Неочевидний приклад: animation-fill-mode

```css
@keyframes slide {
    from {
        transform: translateX(-100px);
    }
    to {
        transform: translateX(0);
    }
}
.slide {
    animation: slide 0.5s ease-out forwards;
}
```

### Неочевидний приклад: prefers-reduced-motion

```css
@media (prefers-reduced-motion: reduce) {
    .fade,
    .slide {
        animation: none;
        transition: none;
    }
}
```

### Неочевидний приклад: motion-path

```css
@keyframes move {
    to {
        offset-distance: 100%;
    }
}
.ball {
    offset-path: path("M0,0 L100,100");
    animation: move 2s linear;
}
```

### Неочевидний приклад: анімація через custom properties

```css
:root {
    --duration: 0.8s;
}
.bounce {
    animation: bounce var(--duration) infinite;
}
@keyframes bounce {
    0%,
    100% {
        transform: translateY(0);
    }
    50% {
        transform: translateY(-30px);
    }
}
```

## Пояснення під капотом

Браузер парсить CSS, створює CSSOM, застосовує transition, transform, animation, оптимізує рендеринг, інтегрує з DOM, API (Web Animations, prefers-reduced-motion).

### Як працюють анімації у рушії

Анімації інтегруються з DOM, впливають на layout, продуктивність, доступність, UX, можуть керуватися через JS.

## Нюанси та підводні камені

-   Надмірна кількість анімацій — погана продуктивність
-   Відсутність prefers-reduced-motion — поганий UX для людей з вадами
-   Відсутність forwards — елемент повертається у початковий стан
-   Відсутність transition-delay — неочікувана поведінка
-   Відсутність custom properties — негнучкі анімації
-   Відсутність motion-path — обмежені ефекти

## Діаграми

```mermaid
graph TD
    TRANSITION[transition] --> PROPERTY[transition-property]
    TRANSITION --> DURATION[transition-duration]
    TRANSITION --> TIMING[transition-timing-function]
    TRANSITION --> DELAY[transition-delay]
    TRANSFORM[transform] --> TRANSLATE[translate]
    TRANSFORM --> SCALE[scale]
    TRANSFORM --> ROTATE[rotate]
    TRANSFORM --> SKEW[skew]
    ANIMATION[animation] --> KEYFRAMES[keyframes]
    ANIMATION --> DURATIONA[animation-duration]
    ANIMATION --> FILL[animation-fill-mode]
    ANIMATION --> ITER[animation-iteration-count]
    ANIMATION --> PLAY[animation-play-state]
    ANIMATION --> DIRECTION[animation-direction]
    ANIMATION --> DELAYA[animation-delay]
    ANIMATION --> CUSTOM[var(--duration)]
    ANIMATION --> MOTION[motion-path]
```

## Приклад застосування в реальних проєктах

-   Кнопки — transition, transform, animation
-   Модальні вікна — fadeIn, slide, forwards
-   Галереї — motion-path, custom properties
-   SPA — prefers-reduced-motion, анімації через JS
-   Корпоративні сайти — акцентні анімації, bounce

### Кейс: доступність

prefers-reduced-motion, forwards, оптимізація ефектів.

### Кейс: продуктивність

Мінімізація анімацій, hardware acceleration, custom properties.

## Крос-посилання

-   [CSS: змінні](./07-custom-properties.md)
-   [CSS: layout](./04-layout.md)
-   [Best practices](../HTML/10-best-practices.md)
-   [HTML: медіа](../HTML/05-media.md)

## Підсумок

-   Анімації та трансформації — основа сучасного CSS
-   transition, transform, keyframes — ключові механізми
-   Неочевидні приклади — для гнучкості, доступності, продуктивності
