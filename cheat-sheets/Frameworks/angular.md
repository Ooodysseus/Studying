# ANGULAR

Angular — фреймворк для створення SPA-додатків на TypeScript, з підтримкою компонентів, сервісів, DI, роутингу та реактивних форм.

## Категорія: Основні CLI-команди

| Команда/метод              | Опис               | Приклад/Аутпут           |
| -------------------------- | ------------------ | ------------------------ |
| ng new app                 | створити проект    | ng new my-app            |
| ng serve                   | запуск dev-сервера | ng serve --open          |
| ng generate component name | створити компонент | ng g c header            |
| ng generate service name   | створити сервіс    | ng g s api               |
| ng build                   | зібрати проект     | ng build --prod          |
| ng test                    | тести              | ng test                  |
| ng add @angular/material   | додати пакет       | ng add @angular/material |

## Категорія: Структура проекту

| Команда/метод              | Опис               | Приклад/Аутпут                   |
| -------------------------- | ------------------ | -------------------------------- |
| app.module.ts              | головний модуль    | @NgModule({imports: [...]})      |
| app.component.ts/html/scss | головний компонент | selector: 'app-root'             |
| \*.service.ts              | сервіс             | @Injectable()                    |
| \*.module.ts               | модуль             | @NgModule({declarations: [...]}) |
| \*.routing.module.ts       | роутинг            | RouterModule.forRoot([...])      |

## Категорія: Основи компонентів

| Команда/метод        | Опис                 | Приклад/Аутпут                      |
| -------------------- | -------------------- | ----------------------------------- |
| @Component({...})    | декоратор компонента | @Component({selector:'app-x'})      |
| selector             | селектор             | selector: 'app-header'              |
| templateUrl/template | шаблон/inline-шаблон | templateUrl: './x.html'             |
| styleUrls/styles     | стилі                | styleUrls: ['./x.scss']             |
| @Input()             | вхідний параметр     | @Input() user: User                 |
| @Output()            | вихідна подія        | @Output() save = new EventEmitter() |
| [(ngModel)]          | двосторонній зв'язок | <input [(ngModel)]="name">          |
| *ngIf, *ngFor        | директиви            | *ngIf="cond" *ngFor="let x of arr"  |
| (click), [value]     | подія/прив'язка      | (click)="fn()" [value]="val"        |

## Категорія: Сервіси, DI, HTTP

| Команда/метод                 | Опис              | Приклад/Аутпут                      |
| ----------------------------- | ----------------- | ----------------------------------- |
| @Injectable()                 | декоратор сервісу | @Injectable({providedIn:'root'})    |
| constructor(private s:Api)    | DI (інжекція)     | constructor(private api:ApiService) |
| HttpClient                    | HTTP-запити       | this.http.get('/api')               |
| subscribe/pipe/map/catchError | RxJS-оператори    | .pipe(map(x=>x),catchError(...))    |

## Категорія: Роутинг

| Команда/метод                | Опис                 | Приклад/Аутпут                                |
| ---------------------------- | -------------------- | --------------------------------------------- |
| RouterModule.forRoot         | оголошення маршрутів | RouterModule.forRoot([{path:'',component:X}]) |
| <router-outlet>              | місце для роута      | <router-outlet></router-outlet>               |
| routerLink, routerLinkActive | навігація            | <a [routerLink]="['/home']">                  |
| this.router.navigate         | програмна навігація  | this.router.navigate(['/users'])              |

## Категорія: Форми

| Команда/метод          | Опис                  | Приклад/Аутпут                            |
| ---------------------- | --------------------- | ----------------------------------------- |
| ReactiveFormsModule    | реактивні форми       | imports: [ReactiveFormsModule]            |
| FormGroup, FormControl | група/контрол         | new FormGroup({name:new FormControl('')}) |
| formControlName        | прив'язка до контролю | <input formControlName="name">            |
| Validators.required    | валідація             | Validators.required                       |
| (ngSubmit)             | подія submit          | <form (ngSubmit)="onSubmit()">            |

## Категорія: Інше

| Команда/метод   | Опис               | Приклад/Аутпут                    |
| --------------- | ------------------ | --------------------------------- | -------- |
| ngOnInit()      | хук ініціалізації  | ngOnInit() { ... }                |
| ngOnDestroy()   | хук знищення       | ngOnDestroy() { ... }             |
| @ViewChild()    | доступ до елемента | @ViewChild('ref') ref!:ElementRef |
| @HostListener() | обробка подій      | @HostListener('window:scroll')    |
| async pipe      | асинхронний пайп   | {{ obs$                           | async }} |
| environment.ts  | змінні оточення    | environment.apiUrl                |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
