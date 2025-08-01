# Angular 15+: сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке Angular 15+](#що-таке-angular-15)
-   [Історія та роль Angular](#історія-та-роль-angular)
-   [Встановлення та старт проекту](#встановлення-та-старт-проекту)
-   [Структура проєкту Angular](#структура-проекту-angular)
-   [Основи синтаксису та архітектури](#основи-синтаксису-та-архітектури)
-   [Компоненти (Components)](#компоненти-components)
-   [Модулі (Modules), Standalone Components](#модулі-modules-standalone-components)
-   [Сервіси (Services) та Dependency Injection](#сервіси-services-та-dependency-injection)
-   [Роутінг (Routing) та lazy loading](#роутінг-routing-та-lazy-loading)
-   [Директиви (Directives)](#директиви-directives)
-   [Пайпи (Pipes)](#пайпи-pipes)
-   [Форми (Forms): Template-driven vs Reactive Forms](#форми-forms-template-driven-vs-reactive-forms)
-   [RxJS та реактивне програмування](#rxjs-та-реактивне-програмування)
-   [HTTP, робота з API, Interceptors](#http-робота-з-api-interceptors)
-   [State Management: Signals, NGXS, NGRX](#state-management-signals-ngxs-ngrx)
-   [Change Detection, Zone.js, Signals](#change-detection-zonejs-signals)
-   [Внутрішні механізми: DI, Zone.js, CD, Garbage Collection](#внутрішні-механізми-di-zonejs-cd-garbage-collection)
-   [Performance traps, оптимізація, підводні камені](#performance-traps-оптимізація-підводні-камені)
-   [Тестування: Jest, Jasmine, Cypress](#тестування-jest-jasmine-cypress)
-   [Безпека (Security), XSS, CSRF, Auth Guards](#безпека-security-xss-csrf-auth-guards)
-   [Best practices](#best-practices)
-   [Корисні ресурси та документація](#корисні-ресурси-та-документація)
-   [Поглиблено: RxJS](#поглиблено-rxjs)
-   [Поглиблено: NgRx](#поглиблено-ngrx)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**Angular 15+** — це сучасний фреймворк для створення великих, швидких, масштабованих SPA, PWA та корпоративних web-додатків.  
Розроблений та підтримуваний Google, Angular став стандартом для enterprise UI, з потужною типовою системою (TypeScript), DI, RxJS, Signals, оптимізованим рендерингом і тестуванням.

---

## Що таке Angular 15+

-   **Angular** — фреймворк на TypeScript для побудови складних веб-додатків.
-   Надає структуру, модульність, реактивність та інструменти для масштабованості.
-   В Angular 15+ з’явились Standalone Components, Signals, новий Change Detection, покращена продуктивність, сучасний синтаксис.

---

## Історія та роль Angular

-   **2010:** AngularJS (1.x) — перший фреймворк (MVC).
-   **2016:** Angular (2+) — переписаний на TypeScript, сучасна архітектура.
-   **2022-2024:** Angular 15+ — Standalone Components, Signals, покращений DI, Zone.js v0, іновації у рендерингу.
-   **2024+:** Angular — вибір для enterprise, fintech, healthcare, CRM, PWA.

---

## Встановлення та старт проекту

### Встановлення CLI

```bash
npm install -g @angular/cli
```

### Створення нового проекту

```bash
ng new my-angular-app --standalone
cd my-angular-app
ng serve
```

---

## Структура проєкту Angular

```
my-angular-app/
├─ src/
│   ├─ app/
│   │   ├─ components/
│   │   ├─ services/
│   │   ├─ pipes/
│   │   ├─ models/
│   │   ├─ app.config.ts
│   │   └─ app.routes.ts
│   ├─ assets/
│   ├─ environments/
│   ├─ index.html
│   ├─ main.ts
│   └─ styles.scss
├─ angular.json
├─ package.json
└─ tsconfig.json
```

-   **Standalone Components:** більше не потрібен AppModule!
-   **app.config.ts:** точка конфігурації.
-   **app.routes.ts:** маршрутизація.

---

## Основи синтаксису та архітектури

### Компонент

```typescript
import { Component } from "@angular/core";

@Component({
    selector: "app-demo",
    template: `<h1>{{ title }}</h1>`,
    styles: [
        `
            h1 {
                color: #1976d2;
            }
        `,
    ],
})
export class DemoComponent {
    title = "Demo Angular 15+";
}
```

### Standalone Component

```typescript
import { Component } from "@angular/core";

@Component({
    selector: "app-standalone",
    standalone: true,
    template: `<p>Standalone!</p>`,
})
export class StandaloneComponent {}
```

---

## Компоненти (Components)

-   Основний будівельний блок UI.
-   Має шаблон (template), стилі, логіку.
-   Декларація через @Component.
-   Використання Input, Output для зв'язку.

```typescript
import { Component, Input, Output, EventEmitter } from "@angular/core";

@Component({
    selector: "app-counter",
    template: `
        <button (click)="decrement()">-</button>
        {{ count }}
        <button (click)="increment()">+</button>
    `,
})
export class CounterComponent {
    @Input() count = 0;
    @Output() countChange = new EventEmitter<number>();
    increment() {
        this.countChange.emit(this.count + 1);
    }
    decrement() {
        this.countChange.emit(this.count - 1);
    }
}
```

---

## Модулі (Modules), Standalone Components

-   **Модулі (modules)** — групують компоненти, сервіси, пайпи.
-   **Standalone Components** — новий підхід без AppModule.

```typescript
export const routes = [
    { path: "", component: HomeComponent, pathMatch: "full" },
    { path: "about", component: AboutComponent },
];
```

```typescript
// app.config.ts
import { provideRouter } from "@angular/router";
import { routes } from "./app.routes";

export const appConfig = {
    providers: [provideRouter(routes)],
};
```

---

## Сервіси (Services) та Dependency Injection

-   **Сервіси** — логіка, що не стосується UI (API, State).
-   **DI** — інжекція залежностей.

```typescript
import { Injectable } from "@angular/core";

@Injectable({ providedIn: "root" })
export class ApiService {
    getData() {
        /* ... */
    }
}
```

Використання у компоненті:

```typescript
constructor(private api: ApiService) {}
```

---

## Роутінг (Routing) та lazy loading

-   **Router** — маршрутизація сторінок.
-   **Lazy loading** — асинхронне підключення модулів/компонентів.

```typescript
// app.routes.ts
import { Routes } from "@angular/router";

export const routes: Routes = [
    { path: "", component: HomeComponent },
    {
        path: "admin",
        loadComponent: () =>
            import("./admin/admin.component").then((m) => m.AdminComponent),
    },
];
```

---

## Директиви (Directives)

-   **Structural:** *ngIf, *ngFor, \*ngSwitch.
-   **Attribute:** [ngClass], [ngStyle], custom.

```html
<div *ngIf="isVisible">Видимий блок</div>
<ul>
    <li *ngFor="let item of items">{{ item }}</li>
</ul>
```

---

## Пайпи (Pipes)

-   Трансформують дані у шаблоні.

```typescript
{{ amount | currency:'UAH':'symbol':'1.2-2' }}
{{ date | date:'shortDate' }}
```

Створення custom pipe:

```typescript
import { Pipe, PipeTransform } from "@angular/core";
@Pipe({ name: "capitalize" })
export class CapitalizePipe implements PipeTransform {
    transform(value: string) {
        return value.charAt(0).toUpperCase() + value.slice(1);
    }
}
```

---

## Форми (Forms): Template-driven vs Reactive Forms

-   **Template-driven:** прості, декларативні.
-   **Reactive Forms:** для складної валідації, динаміки.

### Reactive Form приклад

```typescript
import { FormControl, FormGroup, Validators } from "@angular/forms";

form = new FormGroup({
    email: new FormControl("", [Validators.required, Validators.email]),
    password: new FormControl("", Validators.required),
});
```

```html
<form [formGroup]="form">
    <input formControlName="email" />
    <input formControlName="password" type="password" />
</form>
```

---

## RxJS та реактивне програмування

-   **RxJS** — бібліотека для роботи з потоками (Observable).
-   Використовується для async API, event streams, state.

```typescript
import { Observable, of } from "rxjs";
of(1, 2, 3).subscribe((val) => console.log(val));
```

```typescript
import { HttpClient } from "@angular/common/http";
this.http.get<User[]>("/api/users").subscribe((users) => (this.list = users));
```

---

## HTTP, робота з API, Interceptors

-   **HttpClientModule** — модуль для роботи з API.
-   **Interceptors** — глобальна обробка запитів/відповідей (логування, токени).

```typescript
import {
    HttpInterceptor,
    HttpRequest,
    HttpHandler,
} from "@angular/common/http";
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
    intercept(req: HttpRequest<any>, next: HttpHandler) {
        const clone = req.clone({
            setHeaders: { Authorization: "Bearer TOKEN" },
        });
        return next.handle(clone);
    }
}
```

---

## State Management: Signals, NGXS, NGRX

-   **Signals (Angular 16+)** — сучасний API для реактивного state.
-   **NGXS, NGRX** — Redux-style state management.

```typescript
import { signal } from "@angular/core";
const count = signal(0);
count.update((v) => v + 1);
```

---

## Change Detection, Zone.js, Signals

-   **Change Detection (CD)** — слідкування за змінами.
-   **Zone.js** — патчить async операції для CD.
-   **Signals** — новий механізм CD без Zone.js.

```typescript
@Component({
    selector: "app-demo",
    template: `{{ count() }}`,
})
export class DemoComponent {
    count = signal(0);
}
```

---

## Внутрішні механізми: DI, Zone.js, CD, Garbage Collection

### Dependency Injection (DI)

-   Angular створює граф залежностей, інжектує їх у компоненти/сервіси.
-   Scope: root, component-level, platform.

### Zone.js

-   Перехоплює асинхронні операції, запускає change detection.

### Change Detection

-   Two strategies: Default (Zone.js) та OnPush (manual).
-   Signals — ще швидше!

### Garbage Collection

-   Angular не керує пам'яттю напряму, але важливо відписуватись від Observable та знищувати ресурси (ngOnDestroy).

---

## Performance traps, оптимізація, підводні камені

-   **Велика кількість необмежених підписок (memory leak).**
-   **Неправильне використання ChangeDetectionStrategy (Default vs OnPush).**
-   **Великі бандли — оптимізуй через lazy loading, Standalone Components.**
-   **Передача великих об’єктів через @Input — краще використовувати Signals.**
-   **Багато логіки в шаблоні — винось у компоненти/пайпи.**

### Best practices:

-   Використовуй OnPush там, де можливо.
-   Відписуйся від Observable (takeUntil, async pipe).
-   Використовуй Standalone Components.
-   Діли UI на дрібні компоненти.
-   Винось логіку у сервіси.
-   Кешуй API.

---

## Тестування: Jest, Jasmine, Cypress

-   **Jest/Jasmine:** unit-тести.
-   **Cypress:** E2E-тести, інтеграція з Angular CLI.

```typescript
import { ComponentFixture, TestBed } from "@angular/core/testing";
import { DemoComponent } from "./demo.component";

describe("DemoComponent", () => {
    let fixture: ComponentFixture<DemoComponent>;
    beforeEach(() => {
        TestBed.configureTestingModule({ declarations: [DemoComponent] });
        fixture = TestBed.createComponent(DemoComponent);
    });
    it("має правильний title", () => {
        fixture.componentInstance.title = "Test";
        fixture.detectChanges();
        expect(fixture.nativeElement.querySelector("h1").textContent).toContain(
            "Test"
        );
    });
});
```

---

## Безпека (Security), XSS, CSRF, Auth Guards

-   **XSS:** Використовуйте [DomSanitizer](https://angular.io/api/platform-browser/DomSanitizer) для v-html.
-   **CSRF:** Для API — токени, серверна перевірка.
-   **Auth Guards:** Захист роутів, перевірка ролей.

```typescript
import { CanActivate } from "@angular/router";
@Injectable({ providedIn: "root" })
export class AuthGuard implements CanActivate {
    canActivate() {
        return this.authService.isLoggedIn;
    }
}
```

---

## Best practices

-   Пиши код на TypeScript, використовуй сучасний синтаксис.
-   Використовуй Standalone Components та Signals.
-   Оптимізуй Change Detection (OnPush, Signals).
-   Розбивай додаток на дрібні компоненти.
-   Використовуй DI для сервісів, пайпів, директив.
-   Кешуй запити, оптимізуй API.
-   Тестуй компоненти та сервіси.
-   Валідуй дані на сервері.
-   Дотримуйся Official Style Guide ([Angular Style Guide](https://angular.io/guide/styleguide)).

---

## Корисні ресурси та документація

-   [Офіційна документація Angular](https://angular.io/docs)
-   [Angular Signals](https://angular.io/guide/signals)
-   [RxJS Docs](https://rxjs.dev/)
-   [NGXS Docs](https://www.ngxs.io/)
-   [NGRX Docs](https://ngrx.io/)
-   [Angular CLI](https://angular.io/cli)
-   [Angular Testing](https://angular.io/guide/testing)
-   [Angular Security](https://angular.io/guide/security)
-   [Angular Style Guide](https://angular.io/guide/styleguide)
-   [Cypress Docs](https://docs.cypress.io/)

---

## Поглиблено: RxJS

### Внутрішні механізми та архітектура RxJS

-   **Observable** — lazy, push-based потік, створюється через конструктор або фабричні методи (`of`, `from`, `interval`).
-   **Observer** — отримувач даних (next, error, complete).
-   **Subscription** — керує життєвим циклом потоку (відписка через `unsubscribe()`).
-   **Subject** — multicast stream, як джерело і підписник одночасно.
-   **BehaviorSubject** — завжди має останнє значення, підписник отримує його при підписці.
-   **ReplaySubject** — кешує кілька останніх значень для нових підписників.

#### Схема потоку RxJS

```
[Observable] --pipe(Operators)--> [Observer/Subscriber]
           |                         |
      (source)                (next/error/complete)
```

### Основні оператори

-   **map, filter, switchMap, mergeMap, concatMap, debounceTime, take, takeUntil, catchError, tap**
-   Для складної бізнес-логіки — комбінування операторів у pipe.

#### Приклади

```typescript
import { of, filter, map } from "rxjs";

of(1, 2, 3, 4, 5)
    .pipe(
        filter((n) => n % 2 === 0),
        map((n) => n * 10)
    )
    .subscribe((val) => console.log("Результат:", val)); // 20, 40
```

#### Subject/BehaviorSubject

```typescript
import { BehaviorSubject } from "rxjs";

const user$ = new BehaviorSubject<User | null>(null);
user$.next({ name: "Олег", role: "admin" });
user$.subscribe((user) => console.log("Поточний юзер:", user));
```

### Типові підводні камені та performance traps

-   **Memory leaks:** не забувай відписуватись (`unsubscribe`, `takeUntil`, async pipe).
-   **Великі потокові дерева:** оптимізуй кількість операторів, уникай зайвих підписок.
-   **Зайва логіка у subscribe:** винось у оператори, сервіси або async pipe.

### Кращі практики RxJS

-   Завжди відписуйся від потоків у `ngOnDestroy` або через async pipe.
-   Використовуй оператори для трансформації даних, не обробляй дані напряму у subscribe.
-   Для потоків даних у сервісах — використовуй BehaviorSubject/ReplaySubject.
-   Для UI-логіки — async pipe (автоматична відписка).
-   Не передавай складні обʼєкти через Subject — краще використовуй окремі потоки для кожної сутності.

### Корисні ресурси

-   [RxJS Docs](https://rxjs.dev/)
-   [RxJS Deep Dive](https://blog.angular-university.io/rxjs-angular-reactive-programming-tutorial/)
-   [RxJS Patterns](https://www.learnrxjs.io/)
-   [RxJS Marbles](https://rxmarbles.com/)

---

## Поглиблено: NgRx

### Внутрішні механізми та архітектура NgRx

-   **Store** — глобальний immutable state у вигляді обʼєкта.
-   **Action** — подія, яка змінює state (type, payload).
-   **Reducer** — pure function, яка описує як Action трансформує Store.
-   **Selector** — функція для отримання частини стану.
-   **Effect** — логіка для асинхронних дій (API, роутінг) через RxJS.

#### Схема NgRx

```
[Component] --dispatch(Action)--> [Store] --(Reducer)--> [New State]
        |                                   |
     (select)                          (Effect) --dispatch(Action)-->
```

### Приклад конфігурації Store

```typescript
// store/counter.actions.ts
import { createAction, props } from "@ngrx/store";
export const increment = createAction("[Counter] Increment");
export const set = createAction("[Counter] Set", props<{ value: number }>());

// store/counter.reducer.ts
import { createReducer, on } from "@ngrx/store";
export const initialState = 0;
export const counterReducer = createReducer(
    initialState,
    on(increment, (state) => state + 1),
    on(set, (state, { value }) => value)
);

// app.config.ts
import { provideStore } from "@ngrx/store";
import { counterReducer } from "./store/counter.reducer";
export const appConfig = {
    providers: [provideStore({ counter: counterReducer })],
};
```

### Ефекти (Effects)

-   Для роботи з API, навігацією, сайд-ефектами.

```typescript
// store/counter.effects.ts
import { Injectable } from "@angular/core";
import { Actions, createEffect, ofType } from "@ngrx/effects";
import { increment, set } from "./counter.actions";
import { tap, map } from "rxjs/operators";

@Injectable()
export class CounterEffects {
    logIncrement$ = createEffect(
        () =>
            this.actions$.pipe(
                ofType(increment),
                tap(() => console.log("Інкрементовано!"))
            ),
        { dispatch: false }
    );
    constructor(private actions$: Actions) {}
}
```

### Selectors

```typescript
import { createSelector } from "@ngrx/store";
export const selectCounter = (state: AppState) => state.counter;
export const selectIsEven = createSelector(
    selectCounter,
    (counter) => counter % 2 === 0
);
```

### Типові підводні камені та performance traps

-   Не зберігай великі обʼєкти в Store — використовуй нормалізацію.
-   Не давай компонентам напряму мутувати state — все тільки через Actions.
-   Ефекти мають бути pure — уникай сайд-ефектів у reducers.
-   Відписуйся від потоків, якщо використовуєш select без async pipe.

### Кращі практики NgRx

-   Діли Store на фічі, використовуй селектори.
-   Використовуй createAction, createReducer, createSelector.
-   Пиши ефекти для асинхронних дій.
-   Тестуй редюсери та ефекти окремо.
-   Документуй структуру Store, Action, Selector.

### Корисні ресурси

-   [NgRx Docs](https://ngrx.io/)
-   [NgRx Deep Dive](https://blog.angular-university.io/ngrx-store-effects/)
-   [NgRx Patterns](https://dev.to/burkeholland/ngrx-best-practices-1b2h)
-   [NgRx Schematics](https://ngrx.io/guide/schematics)

---

## Короткий підсумок

**Angular 15+ — це потужний, типізований, реактивний фреймворк для сучасних великих web-додатків.**  
Signals, Standalone Components, RxJS, NgRx, оптимізований рендеринг, тестування та безпека — це основа для професійної розробки у 2024+ році.  
Дотримуйся best practices, оптимізуй продуктивність, тестуй і розвивайся разом із сучасним Angular!

---
