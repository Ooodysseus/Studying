# Angular 15+ Cheatsheet

## CLI Commands
ng new my-app  
ng serve  
ng build  
ng test  
ng lint  
ng add @angular/material  
ng g c my-component  
ng g s my-service  
ng g m my-module  
ng g pipe my-pipe  
ng g directive my-directive  
ng g guard my-guard  
ng g interface my-interface  
ng update  
ng e2e  
ng generate component my-comp  
ng generate service my-svc  
ng generate module my-mod  
ng generate directive my-dir  
ng generate pipe my-pipe  
ng generate guard my-guard  

## Component
```typescript
@Component({ selector: 'app-root', templateUrl: './app.component.html' })
export class AppComponent {}
```

## Module
```typescript
@NgModule({
  imports: [BrowserModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

## Data Binding
```html
{{ title }}
<input [value]="title">
<button (click)="onClick()">Click</button>
<input [(ngModel)]="value">
<span [class.active]="isActive"></span>
<img [src]="imgUrl">
<app-child [data]="parentData"></app-child>
<input [disabled]="isDisabled">
<button (dblclick)="doDouble()">
<input (input)="onInput($event)">
```

## Structural Directives
```html
*ngIf="isTrue"
*ngFor="let item of items"
*ngSwitchCase="case1"
*ngSwitchDefault
```

## Attribute Directives
```html
[ngClass]="{active: isActive}"
[ngStyle]="{color:'red'}"
[hidden]="!isVisible"
[required]="true"
[readonly]="isReadonly"
```

## Service
```typescript
@Injectable({ providedIn: 'root' })
export class MyService {}
```

## Dependency Injection
```typescript
constructor(private myService: MyService) {}
constructor(private http: HttpClient) {}
constructor(private fb: FormBuilder) {}
```

## Routing
```typescript
const routes: Routes = [{ path: '', component: HomeComponent }]
```
```html
<router-outlet></router-outlet>
<a routerLink="/about">About</a>
```
```typescript
routerLinkActive="active"
router.navigate(['/home'])
{ path: 'user/:id', component: UserComponent }
this.route.snapshot.paramMap.get('id')
{ path: '**', component: PageNotFoundComponent }
```

## HttpClient
```typescript
http.get('/api/data').subscribe(data => ...)
http.post('/api', body).subscribe(...)
http.put('/api', body).subscribe(...)
http.delete('/api/id').subscribe(...)
http.patch('/api/id', body).subscribe(...)
http.get<User[]>('/api/users')
http.get('/api/data', { params: { id: 42 } })
http.get('/api/data').pipe(map(res => res))
```

## Pipes
```html
{{ myDate | date:'short' }}
{{ price | currency:'USD' }}
{{ name | uppercase }}
{{ name | lowercase }}
{{ value | percent }}
{{ arr | json }}
{{ text | slice:0:5 }}
{{ items | async }}
{{ phone | customPipe }}
```

## Custom Pipe
```typescript
@Pipe({ name: 'capitalize' })
export class CapitalizePipe implements PipeTransform {
  transform(value: string): string {
    return value.charAt(0).toUpperCase() + value.slice(1);
  }
}
```

## Built-in Directives
```html
<div *ngIf="isVisible"></div>
<div *ngFor="let item of items"></div>
<div [ngSwitch]="condition">
  <div *ngSwitchCase="'A'">A</div>
  <div *ngSwitchDefault>Default</div>
</div>
```

## Custom Directive
```typescript
@Directive({ selector: '[appHighlight]' })
export class HighlightDirective {
  constructor(el: ElementRef) {
    el.nativeElement.style.backgroundColor = 'yellow';
  }
}
```

## Template-driven Form
```html
<form #f="ngForm" (ngSubmit)="submit(f.value)">
  <input name="email" ngModel required>
  <button type="submit">Send</button>
</form>
```

## Reactive Form
```typescript
form = new FormGroup({ name: new FormControl('') });
```
```html
<form [formGroup]="form" (ngSubmit)="submit()">
  <input formControlName="name">
  <button>OK</button>
</form>
```
```typescript
form.get('name').setValue('John');
form.valueChanges.subscribe(val => ...)
form.reset();
Validators.required
Validators.minLength(3)
Validators.email
this.form.controls['name'].hasError('required')
```

## Lifecycle Hooks
ngOnInit()  
ngOnDestroy()  
ngOnChanges()  
ngAfterViewInit()  
ngAfterContentInit()  
ngDoCheck()  
ngAfterViewChecked()  
ngAfterContentChecked()  

## ViewChild & ContentChild
@ViewChild('ref') ref: ElementRef;  
@ContentChild(ChildComponent) child: ChildComponent;  

## Imports
import { FormsModule } from '@angular/forms';  
import { ReactiveFormsModule } from '@angular/forms';  
import { HttpClientModule } from '@angular/common/http';  
import { RouterModule } from '@angular/router';  
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';  

## Angular Material
import { MatButtonModule } from '@angular/material/button';  
<button mat-raised-button>Click</button>  
<mat-form-field>
  <input matInput>
</mat-form-field>
<mat-table [dataSource]="data"></mat-table>
<mat-icon>home</mat-icon>
<mat-toolbar></mat-toolbar>
<mat-card></mat-card>
<mat-dialog></mat-dialog>

## RxJS
of(1,2,3).pipe(map(x=>x*2)).subscribe()  
interval(1000).subscribe(v => ...)  
subject = new Subject<number>();  
behavior = new BehaviorSubject<number>(0);  
observable.pipe(filter(x=>x>5))  
from([1,2,3]).subscribe()  
merge(a$, b$).subscribe()  
forkJoin([a$, b$]).subscribe()  
combineLatest([a$, b$]).subscribe()  
switchMap(val => ...)  
debounceTime(300)  
catchError(err => of([]))  

## Error Handling
.subscribe({ next:x=>..., error:e=>... })  
catchError(err => of([]))  

## Guards
@Injectable({ providedIn: 'root' })  
export class AuthGuard implements CanActivate {  
  canActivate(): boolean { return true; }  
}  
{ path: 'admin', canActivate: [AuthGuard], component: AdminComponent }  

## Lazy Loading
{ path: 'admin', loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule) }  

## Animations
```typescript
import { trigger, state, style, animate, transition } from '@angular/animations';
@Component({
  animations: [
    trigger('openClose', [
      state('open', style({ height: '200px' })),
      state('closed', style({ height: '100px' })),
      transition('open <=> closed', [animate('0.5s')])
    ])
  ]
})
```

## Observables
import { Observable } from 'rxjs';  
myObservable = new Observable(observer => {  
  observer.next('Hello');  
  observer.complete();  
});  
myObservable.subscribe(val => ...)  

## Error Handling Http
http.get('/api/data').subscribe({  
  next: data => {},  
  error: err => { console.error(err); }  
});  

## Testing
import { TestBed } from '@angular/core/testing';  
TestBed.configureTestingModule({ declarations: [MyComponent] });  
it('should create', () => { ... });  
expect(service.getData()).toEqual(['a', 'b']);  

## Internationalization
<span i18n="@@welcome">Welcome!</span>  

## Environment Variables
import { environment } from '../environments/environment';  
console.log(environment.production);  

## Angular CLI commands
ng lint  
ng build --prod  
ng test  
ng e2e  

## RxJS Operators
import { map, filter, switchMap } from 'rxjs/operators';  
observable.pipe(map(x => x * 2), filter(x => x > 10))  

## Change Detection
@Component({ changeDetection: ChangeDetectionStrategy.OnPush })  

## TrackBy
<li *ngFor="let item of items; trackBy: trackById">{{item.name}}</li>  
trackById(index, item) { return item.id; }  

## Custom Validators
function customValidator(control: AbstractControl) {  
  return control.value === 'valid' ? null : { invalid: true };  
}  

## Interceptors
@Injectable()  
export class AuthInterceptor implements HttpInterceptor {  
  intercept(req: HttpRequest<any>, next: HttpHandler) {  
    const cloned = req.clone({ setHeaders: { Authorization: 'Bearer token' } });  
    return next.handle(cloned);  
  }  
}  

## Resolver
@Injectable({ providedIn: 'root' })  
export class DataResolver implements Resolve<any> {  
  resolve() { return this.service.getData(); }  
}  

## Standalone Component (Angular 15+)
@Component({  
  standalone: true,  
  selector: 'app-standalone',  
  template: `<div>Standalone!</div>`  
})  
export class StandaloneComponent {}  

## Signals (Angular 16+)
import { signal } from '@angular/core';  
count = signal(0);  
count.update(n => n + 1);  

## Common Errors  
ExpressionChangedAfterItHasBeenCheckedError  
NG0100: Expression has changed after it was checked  
NullInjectorError  
Template parse errors  

## Useful Links  
https://angular.io/docs  
https://angular.io/cli  
https://rxjs.dev/  

## Best Practices  
Use OnPush change detection  
Use trackBy for *ngFor  
Keep services stateless  
Use modules for feature separation  
Lazy load heavy modules  
Use environment variables  
Avoid logic in templates  
Use interfaces for data types  
Use Angular Material for UI consistency  
Write unit tests for services and components  
Prefer observables to promises  
Handle unsubscribe for subscriptions  
Use pipes for formatting  
Keep templates clean  
Document APIs  
Use custom error handling  
Validate forms  
Use guards for routes  
Prefer reactive forms for complex logic  
Use CSS encapsulation  
Use ViewChild for DOM access  
Split logic into small functions  
Reuse components  
Use constants for magic values  
Organize routes in separate routing modules  
Use enums for fixed sets  
Use HttpInterceptor for auth  
Secure API requests  
Use Angular Universal for SSR  
Optimize bundle size  
Monitor performance  
Use strict type checking  
Leverage IDE tools  
Update dependencies regularly  
Keep code DRY  
Avoid using any type  
Prefer readonly properties  
Use async pipe in templates  
Handle loading states  
Implement pagination  
Use debounce for input  
Use shared modules  
Handle errors gracefully  
Avoid circular dependencies  
Use feature flags  
Use modules for scalability  
Test edge cases  
Use Angular schematics  
Use custom pipes for repeated logic  
Document components  
Handle edge cases in forms  
Use BehaviorSubject for state  
Share data via services  
Use ContentChild for projected content  
Prefer template over inline HTML  
Use SVG icons  
Use theme support  
Prefer SCSS over CSS  
Use Angular Animations  
Use AOT compilation  
Optimize change detection  
Avoid direct DOM manipulation  
Keep assets organized  
Use lazy loading images  
Use async/await with observables  
Prefer strong typing  
Use strictNullChecks  
Handle 404 routes  
Use fallback UI  
Implement SEO  
Check accessibility  
Use ARIA attributes  
Use cypress or protractor for E2E tests  
Use Angular DevTools  
Profile memory usage  
Use server-side rendering for SEO  
Document environment setup  
Automate deployment  
Use CI/CD pipelines  
Monitor error logs  
Keep dependencies up-to-date  
Use code reviews  
Keep code readable  
Write comments for complex logic  
Avoid global styles  
Use encapsulated styles  
Implement dark mode  
Use custom themes  
Support localization  
Optimize for mobile  
Use responsive layouts  
Minimize bundle size  
Use tree-shakable modules  
Prefer ES modules  
Use code splitting  
Leverage service workers  
Use PWA features  
Cache static assets  
Handle API rate limits  
Use retry for failed requests  
Avoid blocking UI  
Prefer stateless components  
Handle side effects in effects  
Use NgRx for state management  
Keep selectors pure  
Avoid mutating state  
Prefer immutable data  
Use selectors for derived state  
Organize actions  
Use effects for async  
Handle errors in effects  
Use feature modules  
Write integration tests  
Automate code formatting  
Lint code before commit  
Use Husky for git hooks  
Keep test coverage high  
Avoid dead code  
Refactor old code  
Archive unused modules  
Review dependencies  
Update to latest Angular  
Use Ivy renderer  
Report bugs  
Track performance metrics  
Use SourceMaps  
Minimize polyfills  
Prefer native APIs  
Follow Angular style guide  
