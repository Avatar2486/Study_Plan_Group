# Angular — Answer Bank

---

**Q: How does Angular change detection work?**

**Short:** Angular checks every component in the tree for changes on each browser event, HTTP response, or timer. Default strategy checks all; OnPush checks only when inputs change or async pipe emits.

**Detailed:**
- Zone.js patches browser APIs (`setTimeout`, `addEventListener`, XHR) — notifies Angular when anything async completes.
- Angular walks the component tree top-down and checks each component's bindings against previous values.
- **Default strategy:** re-checks every component on every cycle (safe but slow for large trees).
- **OnPush strategy:** skips component unless:
  - An `@Input()` reference changes (not just mutation)
  - An Observable emits through the `async` pipe
  - An event originates inside the component
  - `markForCheck()` is called explicitly

```typescript
@Component({
  selector: 'app-list',
  changeDetection: ChangeDetectionStrategy.OnPush,
  template: `<li *ngFor="let item of items">{{ item.name }}</li>`
})
export class ListComponent {
  @Input() items: Item[]; // must reassign array, not push() into it
}

// Parent must do this (new reference):
this.items = [...this.items, newItem]; // ✅ triggers OnPush
this.items.push(newItem);              // ❌ same reference, no check
```

---

**Q: What is the NgRx data flow?**

**Short:** Action dispatched → Reducer produces new state → Store holds state → Selector reads slice → Component displays via `async` pipe. Side effects (API calls) happen in Effects.

**Detailed:**
```typescript
// 1. Define action
export const loadUsers = createAction('[Users] Load');
export const loadUsersSuccess = createAction('[Users] Load Success', props<{ users: User[] }>());

// 2. Effect — handles side effects
@Injectable()
export class UsersEffects {
  loadUsers$ = createEffect(() =>
    this.actions$.pipe(
      ofType(loadUsers),
      switchMap(() => this.userService.getAll().pipe(
        map(users => loadUsersSuccess({ users })),
        catchError(err => of(loadUsersFailure({ error: err.message })))
      ))
    )
  );
  constructor(private actions$: Actions, private userService: UserService) {}
}

// 3. Reducer — pure function, immutable update
export const usersReducer = createReducer(
  initialState,
  on(loadUsersSuccess, (state, { users }) => ({ ...state, users, loading: false }))
);

// 4. Selector — memoized slice
export const selectUsers = createSelector(selectUsersState, state => state.users);

// 5. Component — dispatch + select
@Component({...})
export class UsersComponent {
  users$ = this.store.select(selectUsers);
  constructor(private store: Store) { this.store.dispatch(loadUsers()); }
}
```

---

**Q: What is the difference between switchMap, mergeMap, concatMap, and exhaustMap?**

**Short:** `switchMap` cancels previous (search box). `mergeMap` runs all in parallel (fire and forget). `concatMap` queues sequentially (ordered ops). `exhaustMap` ignores new until current completes (login button).

**Detailed:**
| Operator | Behavior | Use Case |
|----------|----------|----------|
| `switchMap` | Cancels previous inner observable when new outer value arrives | Search autocomplete, live filters |
| `mergeMap` | All inner observables run concurrently | Independent parallel requests |
| `concatMap` | Queues — waits for each to complete before starting next | Sequential uploads, ordered operations |
| `exhaustMap` | Ignores new outer values while inner is active | Login button (ignore double-click) |

```typescript
// switchMap — cancels in-flight search on each keystroke
this.searchControl.valueChanges.pipe(
  debounceTime(300),
  switchMap(term => this.api.search(term))  // cancels previous if user keeps typing
).subscribe(results => this.results = results);

// exhaustMap — login: ignore clicks until request completes
fromEvent(loginBtn, 'click').pipe(
  exhaustMap(() => this.authService.login(credentials))
).subscribe();
```

---

**Q: What is the difference between Subject, BehaviorSubject, and ReplaySubject?**

**Short:** `Subject` = no initial value, only future values. `BehaviorSubject` = holds current value, new subscribers get it immediately. `ReplaySubject(n)` = replays last n emissions to new subscribers.

**Detailed:**
```typescript
// Subject — no stored value
const s = new Subject<number>();
s.subscribe(v => console.log('A:', v));
s.next(1); // A: 1
// new subscriber misses past values
s.subscribe(v => console.log('B:', v));
s.next(2); // A: 2, B: 2

// BehaviorSubject — stores current value
const b = new BehaviorSubject<number>(0); // initial = 0
b.subscribe(v => console.log('A:', v));  // A: 0 (immediately)
b.next(1); // A: 1
b.subscribe(v => console.log('B:', v));  // B: 1 (gets current)
console.log(b.getValue()); // 1

// ReplaySubject — replays last N emissions
const r = new ReplaySubject<number>(2);
r.next(1); r.next(2); r.next(3);
r.subscribe(v => console.log(v)); // 2, 3 (last 2)
```
Use `BehaviorSubject` in services for shared state. Use `ReplaySubject` when late subscribers need history.

---

**Q: How does lazy loading work in Angular?**

**Short:** Route config uses `loadChildren` (or `loadComponent`) to split the module/component into a separate JS chunk. The browser only downloads it when the route is first visited.

**Detailed:**
```typescript
// app-routing.module.ts
const routes: Routes = [
  { path: '', component: HomeComponent },
  {
    path: 'dashboard',
    loadChildren: () => import('./dashboard/dashboard.module')
      .then(m => m.DashboardModule)  // separate chunk: dashboard.js
  },
  // Standalone (Angular 14+) — no module needed
  {
    path: 'profile',
    loadComponent: () => import('./profile/profile.component')
      .then(c => c.ProfileComponent)
  }
];

// Preload strategy — download lazy chunks after initial load
RouterModule.forRoot(routes, { preloadingStrategy: PreloadAllModules })
```
- Each lazy route becomes a separate webpack chunk.
- Combine with `PreloadAllModules` to preload in the background after initial render.
- Auth guards (`CanLoad`/`CanMatch`) can prevent even the download of unauthorized chunks.

---

**Q: How do Angular Route Guards work?**

**Short:** Guards are functions (or classes) that return `true`/`false`/`UrlTree`. Angular checks them before activating a route and blocks navigation if they return false.

**Detailed:**
```typescript
// Functional guard (Angular 15+) — preferred
export const authGuard: CanActivateFn = (route, state) => {
  const auth = inject(AuthService);
  const router = inject(Router);
  return auth.isLoggedIn()
    ? true
    : router.createUrlTree(['/login'], { queryParams: { returnUrl: state.url } });
};

// Apply to route
{ path: 'admin', component: AdminComponent, canActivate: [authGuard] }

// CanDeactivate — unsaved changes warning
export const unsavedChangesGuard: CanDeactivateFn<EditComponent> = (component) => {
  return component.hasUnsavedChanges()
    ? confirm('You have unsaved changes. Leave?')
    : true;
};
```

Guard types:
| Guard | Purpose |
|-------|---------|
| `canActivate` | Block access to route |
| `canActivateChild` | Block access to child routes |
| `canDeactivate` | Prevent leaving a route (unsaved form) |
| `canMatch` | Prevent route matching (also blocks lazy load) |
| `resolve` | Pre-fetch data before route activates |

---

**Q: What is the difference between Reactive Forms and Template-Driven Forms?**

**Short:** Reactive forms are defined in the component class (explicit, testable, synchronous). Template-driven forms are defined in the HTML with directives (simpler, less boilerplate, hard to test).

**Detailed:**
```typescript
// Reactive Form
@Component({ template: `
  <form [formGroup]="form" (ngSubmit)="submit()">
    <input formControlName="email" />
    <span *ngIf="form.get('email').hasError('email')">Invalid email</span>
  </form>
`})
export class LoginComponent {
  form = this.fb.group({
    email: ['', [Validators.required, Validators.email]],
    password: ['', [Validators.required, Validators.minLength(8)]]
  });
  constructor(private fb: FormBuilder) {}
  submit() { if (this.form.valid) this.auth.login(this.form.value); }
}

// Custom async validator
const emailExists = (service: UserService): AsyncValidatorFn => (control) =>
  service.checkEmail(control.value).pipe(
    map(exists => exists ? { emailTaken: true } : null)
  );
```

| | Reactive | Template-Driven |
|--|----------|----------------|
| Definition | TypeScript class | HTML template |
| Validation | `Validators` functions | `required`, `ngModel` directives |
| Testing | Easy (no DOM needed) | Requires `fakeAsync` + fixture |
| Dynamic fields | Easy (`FormArray.push()`) | Harder |
| Best for | Complex forms | Simple forms |

---

**Q: How do Angular HTTP Interceptors work?**

**Short:** Interceptors sit between `HttpClient` and the network. They can modify every request (add auth header) and every response (handle 401) globally.

**Detailed:**
```typescript
// Functional interceptor (Angular 15+)
export const authInterceptor: HttpInterceptorFn = (req, next) => {
  const token = inject(AuthService).getToken();
  const authReq = token
    ? req.clone({ setHeaders: { Authorization: `Bearer ${token}` } })
    : req;
  return next(authReq);
};

// Error handling interceptor
export const errorInterceptor: HttpInterceptorFn = (req, next) => {
  return next(req).pipe(
    catchError((error: HttpErrorResponse) => {
      if (error.status === 401) inject(Router).navigate(['/login']);
      if (error.status === 500) inject(ToastService).error('Server error');
      return throwError(() => error);
    })
  );
};

// Register in app.config.ts (standalone)
export const appConfig: ApplicationConfig = {
  providers: [
    provideHttpClient(withInterceptors([authInterceptor, errorInterceptor]))
  ]
};
```

---

**Q: What is the correct order of Angular lifecycle hooks?**

**Short:** `ngOnChanges → ngOnInit → ngDoCheck → ngAfterContentInit → ngAfterContentChecked → ngAfterViewInit → ngAfterViewChecked → ngOnDestroy`

**Detailed:**
```typescript
@Component({ selector: 'app-demo', template: `<child [data]="data"></child>` })
export class DemoComponent implements OnInit, AfterViewInit, OnDestroy {
  private destroy$ = new Subject<void>();

  ngOnChanges(changes: SimpleChanges) {
    // Called BEFORE ngOnInit when @Input changes
    // Also called on every subsequent @Input change
    console.log('Previous:', changes['data'].previousValue);
  }

  ngOnInit() {
    // Called once after first ngOnChanges
    // Best place for: API calls, setup subscriptions
    this.dataService.getData().pipe(
      takeUntil(this.destroy$)
    ).subscribe(data => this.data = data);
  }

  ngAfterViewInit() {
    // @ViewChild is available here
    // DOM is fully rendered
  }

  ngOnDestroy() {
    // Cleanup: unsubscribe, clear intervals
    this.destroy$.next();
    this.destroy$.complete();
  }
}
```

Key rules: Don't call APIs in `ngDoCheck` (runs every cycle). Always cleanup in `ngOnDestroy`.

---

**Q: How do you optimize Angular application performance?**

**Short:** Use `OnPush` everywhere, `trackBy` in lists, lazy load routes, `async` pipe over manual subscribe, `@defer` blocks, and avoid function calls in templates.

**Detailed:**
```typescript
// 1. OnPush + trackBy
@Component({
  changeDetection: ChangeDetectionStrategy.OnPush,
  template: `
    <li *ngFor="let item of items; trackBy: trackById">{{ item.name }}</li>
    <!-- Angular 17+ -->
    @for (item of items; track item.id) { <li>{{ item.name }}</li> }
  `
})

// 2. Avoid function calls in templates (called every cycle)
// BAD:
// {{ getFullName(user) }}
// GOOD:
get fullName() { return `${this.user.first} ${this.user.last}`; }  // cached property
// Or use pure pipe

// 3. @defer (Angular 17+) — load heavy component only when visible
@defer (on viewport) {
  <app-heavy-chart />
} @placeholder {
  <div>Loading chart...</div>
}

// 4. Use async pipe — auto-unsubscribes
// BAD: manual subscribe (memory leak risk)
// GOOD:
users$ = this.store.select(selectUsers);
// template: {{ users$ | async }}

// 5. Lazy load images
<img ngSrc="/hero.jpg" width="800" height="400" priority />
```

---

**Q: How do Angular Signals work and how do they differ from RxJS?**

**Short:** Signals are synchronous reactive primitives — `signal()` holds a value, `computed()` derives from signals, `effect()` runs side effects. No subscription management needed.

**Detailed:**
```typescript
import { signal, computed, effect } from '@angular/core';

@Component({ template: `
  <p>Count: {{ count() }}</p>
  <p>Double: {{ double() }}</p>
  <button (click)="increment()">+</button>
` })
export class CounterComponent {
  count = signal(0);
  double = computed(() => this.count() * 2);  // auto-tracks count

  constructor() {
    effect(() => {
      console.log('Count changed:', this.count()); // runs when count changes
    });
  }

  increment() { this.count.update(v => v + 1); }
}

// Signals vs RxJS
// Signals: sync, simple primitives, no subscribe/unsubscribe
// RxJS: async streams, operators, better for event sequences & HTTP
// Together: toSignal(observable$) / toObservable(signal)
import { toSignal } from '@angular/core/rxjs-interop';
users = toSignal(this.http.get<User[]>('/api/users'), { initialValue: [] });
```

Signals enable zoneless Angular (no zone.js), which gives fine-grained DOM updates.

---

## Links
- [[Study Plan/Angular]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
