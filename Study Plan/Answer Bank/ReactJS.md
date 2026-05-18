# ReactJS — Answer Bank

---

**Q: How does React reconciliation work?**

**Short:** React compares the new virtual DOM tree with the previous one (diffing) and updates only the changed parts in the real DOM.

**Detailed:**
- React creates a virtual DOM (lightweight JS objects representing the UI).
- On state/prop change: renders new virtual DOM tree → diffs against previous.
- **Diffing rules:** Same element type → update. Different type → unmount old, mount new. Lists → use `key` to match elements.
- **Fiber:** React 16+ splits rendering into small units (fibers). Can pause/resume work → enables concurrent features.
- `key` prop is critical for lists — tells React which items changed, moved, or were removed.

---

**Q: What is the difference between useState and useReducer?**

**Short:** `useState` for simple independent state. `useReducer` for complex state with multiple sub-values or when next state depends on previous.

**Detailed:**
```javascript
// useState — simple
const [count, setCount] = useState(0);
setCount(prev => prev + 1);

// useReducer — complex state / multiple actions
const reducer = (state, action) => {
  switch (action.type) {
    case 'increment': return { ...state, count: state.count + 1 };
    case 'reset': return initialState;
    default: return state;
  }
};
const [state, dispatch] = useReducer(reducer, { count: 0, loading: false });
dispatch({ type: 'increment' });
```
`useReducer` is also better when logic needs to be tested separately from the component.

---

**Q: What are the rules of useEffect dependency array?**

**Short:** Empty array `[]` = run once on mount. No array = run every render. `[val]` = run when `val` changes. Always include all variables used inside the effect.

**Detailed:**
```javascript
useEffect(() => { fetchData(); }, []);           // once on mount
useEffect(() => { document.title = title; });    // every render
useEffect(() => { fetchUser(id); }, [id]);       // when id changes

// Cleanup — return a function
useEffect(() => {
  const sub = subscribe(event, handler);
  return () => sub.unsubscribe();               // cleanup on unmount or before re-run
}, [event]);
```
ESLint `react-hooks/exhaustive-deps` rule catches missing dependencies. Missing deps = stale closures.

---

**Q: What is the difference between useMemo and useCallback?**

**Short:** `useMemo` memoizes a computed value. `useCallback` memoizes a function reference.

**Detailed:**
```javascript
// useMemo — recompute only when deps change
const expensiveResult = useMemo(() => heavyComputation(data), [data]);

// useCallback — stable function reference across renders
const handleClick = useCallback((id) => {
  dispatch({ type: 'select', id });
}, [dispatch]);

// Both prevent unnecessary child re-renders when passed as props
<ExpensiveChild data={expensiveResult} onClick={handleClick} />
```
Don't overuse — memoization has its own cost. Use only for expensive computations or functions passed as props to `React.memo` children.

---

**Q: Why does a component re-render even after using React.memo?**

**Short:** Because a prop is a new object/array/function reference on every parent render — even if the data is the same. Use `useMemo`/`useCallback` to stabilize references.

**Detailed:**
```javascript
// Problem: new function object every render
function Parent() {
  const handleClick = () => console.log("clicked"); // new ref each render
  return <Child onClick={handleClick} />; // Child re-renders despite React.memo
}

// Fix: stable reference
function Parent() {
  const handleClick = useCallback(() => console.log("clicked"), []); // same ref
  return <Child onClick={handleClick} />;
}

const Child = React.memo(({ onClick }) => <button onClick={onClick}>Click</button>);
```

---

**Q: What is Context API and when should you use Redux instead?**

**Short:** Context = built-in, simple, good for low-frequency updates (theme, auth, locale). Redux = external, better for frequent updates, complex state, time-travel debugging.

**Detailed:**
- **Context:** Every consumer re-renders when context value changes. Fine for app-wide config.
- **Redux Toolkit:** Normalized state, selectors, DevTools, middleware (thunk/saga). Use for: shopping cart, complex form state, real-time data.
- **Zustand:** Lightweight Redux alternative, no boilerplate. Good middle ground.
- Rule: start with `useState`/`useReducer` + lifting state. Add Context for cross-tree sharing. Add Redux/Zustand when Context causes too many re-renders.

---

**Q: What is the difference between SSR, CSR, and ISR?**

**Short:** CSR = JS renders in browser (slow first load). SSR = server renders HTML per request (fast first load, high server cost). ISR = pre-rendered + revalidated periodically (best of both).

**Detailed:**
| | CSR | SSR | ISR |
|--|--|--|--|
| Rendering | Client (browser) | Server (per request) | Server (build + revalidate) |
| First load | Slow (JS download + execute) | Fast (HTML ready) | Fast (pre-built HTML) |
| SEO | Poor | Excellent | Excellent |
| Dynamic data | Always fresh | Always fresh | Stale by `revalidate` seconds |
| Framework | React SPA | Next.js `getServerSideProps` | Next.js `getStaticProps` + `revalidate` |

ISR: page built at deploy + rebuilt in background when someone requests it after `revalidate` seconds. Best for pages that change but don't need real-time data.

---

**Q: How do you handle code splitting and lazy loading in React?**

**Short:** Use `React.lazy()` + `Suspense` to load components only when needed — reduces initial bundle size.

**Detailed:**
```javascript
import { lazy, Suspense } from 'react';

// Only loads Dashboard.js when this route is visited
const Dashboard = lazy(() => import('./Dashboard'));

function App() {
  return (
    <Suspense fallback={<Spinner />}>
      <Routes>
        <Route path="/dashboard" element={<Dashboard />} />
      </Routes>
    </Suspense>
  );
}
```
- Route-based splitting: most impactful — load each page's JS only when navigating there.
- Component-level: split heavy components (charts, editors) behind a user action.

---

**Q: What are React portals and when to use them?**

**Short:** Portals render a component outside the parent DOM hierarchy while keeping it inside React's component tree (events still bubble up).

**Detailed:**
```javascript
// Renders modal at document.body even though it's in a deeply nested component
function Modal({ children }) {
  return ReactDOM.createPortal(
    <div className="modal">{children}</div>,
    document.getElementById('modal-root')
  );
}
```
Use for: modals, tooltips, dropdowns, toasts — anything that needs to visually escape overflow:hidden or z-index stacking contexts of parent.

---

**Q: How does React Query handle caching and stale data?**

**Short:** Cached data is served immediately (stale), then a background refetch happens. `staleTime` controls how long data is considered fresh. `cacheTime` controls how long cached data is kept.

**Detailed:**
```javascript
const { data, isLoading } = useQuery({
  queryKey: ['users', userId],
  queryFn: () => fetchUser(userId),
  staleTime: 5 * 60 * 1000, // 5 min — don't refetch if data is < 5 min old
  cacheTime: 10 * 60 * 1000, // 10 min — keep in cache for 10 min after unmount
  refetchOnWindowFocus: true, // refetch when tab regains focus
});
```
- `staleTime: 0` (default) = always stale → always refetches in background on mount.
- Invalidate manually: `queryClient.invalidateQueries(['users'])` — triggers refetch.

---

## Links
- [[Study Plan/ReactJS]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
