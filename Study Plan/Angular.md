# Angular

---

## 🔰 **1. Angular Foundations**

### 🧱 Core Concepts

- What is Angular? Platform vs Framework, Angular vs AngularJS
- Angular CLI — `ng new`, `ng generate`, `ng serve`, `ng build`, `ng test`
- Workspace structure — `angular.json`, `tsconfig.json`, `src/app/`
- Angular compilation — JIT vs AOT (Ahead-of-Time)
- Ivy renderer — what it is, benefits over View Engine
- Angular versioning and update path (`ng update`)
- Standalone components (Angular 14+) — no NgModule required
- Angular Signals (Angular 16+) — `signal()`, `computed()`, `effect()`

---

## 🧩 **2. Components & Templates**

### 🏗️ Component Basics

- `@Component` decorator — `selector`, `templateUrl`, `styleUrls`, `standalone`
- Component class — properties, methods, constructor
- Template syntax — interpolation `{{ }}`, property binding `[ ]`, event binding `( )`
- Two-way binding `[(ngModel)]` — requires `FormsModule`
- Template reference variables `#ref`
- `ng-template`, `ng-container`, `ng-content` (content projection)
- Dynamic components — `ViewContainerRef`, `createComponent()`

### 📋 Directives

- Structural directives — `*ngIf`, `*ngFor`, `*ngSwitch`
- New control flow syntax — `@if`, `@for`, `@switch` (Angular 17+)
- Attribute directives — `[ngClass]`, `[ngStyle]`, `[ngModel]`
- Custom structural directive — `TemplateRef`, `ViewContainerRef`
- Custom attribute directive — `@Directive`, `@HostListener`, `@HostBinding`

### 🔧 Pipes

- Built-in pipes — `date`, `currency`, `decimal`, `uppercase`, `json`, `async`
- `async` pipe — auto-subscribes/unsubscribes Observables
- Custom pipe — `@Pipe`, `PipeTransform`, `transform()`
- Pure vs impure pipes — when Angular re-runs the pipe

---

## 🔗 **3. Component Communication**

- `@Input()` — pass data from parent to child
- `@Output()` + `EventEmitter` — emit events from child to parent
- `@ViewChild` / `@ViewChildren` — access child component/element from parent
- `@ContentChild` / `@ContentChildren` — access projected content
- Service as shared state (dependency injection)
- RxJS `Subject` / `BehaviorSubject` in a service for cross-component comms

---

## 💉 **4. Services & Dependency Injection**

### 🔌 DI Fundamentals

- `@Injectable({ providedIn: 'root' })` — singleton service, tree-shakable
- `@Injectable({ providedIn: 'platform' })` vs module-level providers
- Hierarchical injectors — root → module → component (each level creates new instance)
- `providers` array in `@Component` — component-scoped instance
- Injection tokens — `InjectionToken<T>`, `useValue`, `useFactory`, `useExisting`
- `inject()` function (Angular 14+) — alternative to constructor injection
- Circular dependency and how to resolve it (`forwardRef`)

---

## 🗂️ **5. Modules (NgModule)**

- `@NgModule` — `declarations`, `imports`, `exports`, `providers`, `bootstrap`
- Root module (`AppModule`) vs feature modules
- `SharedModule` pattern — re-export common directives/pipes
- `CoreModule` pattern — singleton services, import once
- Lazy loaded modules — `loadChildren` in routing
- Standalone component imports — replacing NgModule
- `BrowserModule` vs `CommonModule` — when to use each

---

## 🔀 **6. Routing & Navigation**

### 🛣️ Router Basics

- `RouterModule.forRoot()` vs `RouterModule.forChildren()`
- `Routes` array — `path`, `component`, `redirectTo`, `pathMatch`
- `<router-outlet>` — where routed component renders
- `RouterLink`, `RouterLinkActive` directives
- Programmatic navigation — `Router.navigate()`, `Router.navigateByUrl()`
- Route parameters — `:id`, `ActivatedRoute.params`, `ActivatedRoute.snapshot`
- Query parameters — `queryParams`, `ActivatedRoute.queryParams`

### 🔒 Route Guards

- `CanActivate` — protect route from unauthorized access
- `CanDeactivate` — prevent leaving unsaved form
- `CanActivateChild` — protect child routes
- `CanLoad` / `CanMatch` — prevent lazy module from loading
- Functional guards (Angular 15+) — `canActivate: [() => inject(AuthService).isLoggedIn()]`
- `Resolve` — pre-fetch data before route activates

### ⚡ Lazy Loading

- `loadChildren: () => import('./feature/feature.module').then(m => m.FeatureModule)`
- Standalone lazy loading — `loadComponent`
- Preloading strategies — `NoPreloading`, `PreloadAllModules`, custom strategy
- Route-level code splitting and bundle analysis

---

## 📡 **7. RxJS in Angular**

### 🔧 Core RxJS

- `Observable`, `Observer`, `Subscription` — subscribe/unsubscribe lifecycle
- Creating observables — `of()`, `from()`, `interval()`, `timer()`, `fromEvent()`
- Subjects — `Subject`, `BehaviorSubject`, `ReplaySubject`, `AsyncSubject`
- Operators — `map`, `filter`, `tap`, `take`, `takeUntil`, `debounceTime`, `distinctUntilChanged`
- Flattening operators — `switchMap` vs `mergeMap` vs `concatMap` vs `exhaustMap`
- Error handling — `catchError`, `retry`, `retryWhen`
- Combination — `combineLatest`, `forkJoin`, `zip`, `withLatestFrom`
- `shareReplay(1)` — multicast and cache last value

### 🚿 Subscription Management

- Memory leak from forgotten subscriptions
- `takeUntil(destroy$)` pattern with `ngOnDestroy`
- `takeUntilDestroyed()` (Angular 16+) — auto unsubscribe
- `async` pipe — preferred way (auto-unsubscribes)
- `SubSink` or `Subscription` array pattern

---

## 🗃️ **8. NgRx State Management**

### 🏪 Store Core

- NgRx data flow — Action → Reducer → Store → Selector → Component
- `createAction()` — action creator with optional props
- `createReducer()` + `on()` — pure function, immutable state update
- `createSelector()` + `createFeatureSelector()` — memoized selectors
- `Store.dispatch()` — trigger action
- `Store.select()` — read state slice as Observable

### ⚡ Effects

- `createEffect()` — side effects (API calls, routing, logging)
- `Actions` stream + `ofType()` — listen to specific actions
- `switchMap` in effects — cancel in-flight requests on new dispatch
- Effect error handling — `catchError` returning `EMPTY` or error action
- Non-dispatching effects — `{ dispatch: false }`

### 🔧 NgRx Extras

- `NgRx Entity` — `EntityState`, `EntityAdapter`, CRUD helpers
- `NgRx ComponentStore` — local component state (no global store)
- `NgRx SignalStore` (NgRx 17+) — signal-based state
- `@ngrx/router-store` — sync router state to store
- Redux DevTools — time-travel debugging, action log

---

## 📋 **9. Forms**

### 📝 Template-Driven Forms

- `FormsModule`, `ngModel`, two-way binding
- `#form="ngForm"`, `ngSubmit`
- Built-in validators — `required`, `minlength`, `email`, `pattern`
- Template-driven form validation and error display

### ⚙️ Reactive Forms

- `ReactiveFormsModule`, `FormControl`, `FormGroup`, `FormArray`
- `FormBuilder` — `fb.group()`, `fb.control()`, `fb.array()`
- `Validators` — `required`, `minLength`, `pattern`, `compose()`
- Custom validators — sync and async
- `valueChanges` / `statusChanges` Observables
- Dynamic forms — adding/removing controls at runtime
- `patchValue()` vs `setValue()` — partial vs full update

---

## 🌐 **10. HTTP & API Communication**

- `HttpClientModule` / `provideHttpClient()` (standalone)
- `HttpClient` — `get`, `post`, `put`, `delete`, `patch`
- Request options — headers, params, `observe: 'response'`, `responseType`
- `HttpInterceptor` — add auth token, handle errors globally, loading state
- Functional interceptors (Angular 15+)
- Retry on error — `retry()`, `retryWhen()` with backoff
- Cancellable requests — `switchMap` + `takeUntil`
- Environment-based API URLs — `environment.ts`, `environment.prod.ts`

---

## ♻️ **11. Lifecycle Hooks**

- `ngOnChanges` — called when `@Input` changes (before `ngOnInit`)
- `ngOnInit` — initialize component, API calls here
- `ngDoCheck` — custom change detection (called every cycle)
- `ngAfterContentInit` / `ngAfterContentChecked` — after `ng-content` projected
- `ngAfterViewInit` / `ngAfterViewChecked` — after view + child views init
- `ngOnDestroy` — cleanup: unsubscribe, clear timers
- Order: `OnChanges → OnInit → DoCheck → AfterContentInit → AfterContentChecked → AfterViewInit → AfterViewChecked → OnDestroy`

---

## ⚡ **12. Change Detection**

- Default change detection — checks entire tree on every event/async
- `ChangeDetectionStrategy.OnPush` — only checks when:
  - `@Input` reference changes
  - Observable emits via `async` pipe
  - Event handler inside component fires
  - `markForCheck()` is called
- `ChangeDetectorRef` — `markForCheck()`, `detectChanges()`, `detach()`, `reattach()`
- `NgZone` — `runOutsideAngular()` for performance-heavy tasks
- Signals — fine-grained reactivity without zone.js (Angular 16+)
- Zone.js and `zone-flags.ts` — disable for zoneless Angular

---

## 🚀 **13. Performance Optimization**

- `OnPush` change detection strategy
- `trackBy` in `*ngFor` — prevent full list re-render
- Lazy loading modules + preloading strategy
- Virtual scrolling — `CdkVirtualScrollViewport` (CDK)
- `Pure pipes` over methods in templates
- Bundle analysis — `ng build --stats-json` + `webpack-bundle-analyzer`
- `@defer` block (Angular 17+) — defer component loading until visible/idle/interaction
- Tree-shaking — avoid barrel imports for large libraries
- `NgOptimizedImage` directive — Core Web Vitals optimization

---

## 🧪 **14. Testing**

- `TestBed` — Angular testing module
- `ComponentFixture` — access component instance + DOM
- `detectChanges()` — trigger change detection in tests
- `DebugElement` — `query()`, `triggerEventHandler()`
- `HttpClientTestingModule` + `HttpTestingController` — mock HTTP
- Mocking services — `jasmine.createSpyObj()`, `providedIn` override
- Testing NgRx — `MockStore`, `provideMockStore()`
- Testing Observables — `fakeAsync`, `tick`, `marbles`
- E2E testing — Cypress or Playwright (Protractor deprecated)

---

## 🖥️ **15. Angular Universal (SSR)**

- What is Angular Universal — server-side rendering with Node.js Express
- `ng add @nguniversal/express-engine`
- Transfer State — avoid double-fetching data on client hydration
- SEO benefits — meta tags, `Meta` service, `Title` service
- Hydration (Angular 16+) — non-destructive hydration
- Deployment — Node server vs static pre-render

---

## 🔗 Links

- [[Study Plan/Answer Bank/Angular]] — answers to all questions above
- [[Study Plan]] — back to full study plan
