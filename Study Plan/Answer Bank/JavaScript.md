# JavaScript — Answer Bank

---

**Q: What is the difference between `var`, `let`, and `const`?**

**Short:** `var` is function-scoped and hoisted. `let` and `const` are block-scoped with TDZ. `const` can't be reassigned.

**Detailed:**
```javascript
var x = 1;    // function-scoped, hoisted as undefined
let y = 2;    // block-scoped, not accessible before declaration
const z = 3;  // block-scoped, can't be reassigned (object props can still change)

if (true) {
  var a = 10;   // leaks out of block
  let b = 20;   // stays in block
}
console.log(a); // 10
console.log(b); // ReferenceError
```

---

**Q: What is hoisting?**

**Short:** JavaScript moves declarations to the top of their scope before execution. `var` is hoisted as `undefined`. `let`/`const` are hoisted but not initialized (TDZ).

**Detailed:**
```javascript
console.log(x); // undefined — var is hoisted
var x = 5;

console.log(y); // ReferenceError — TDZ
let y = 5;

greet(); // Works — function declarations fully hoisted
function greet() { return "hi"; }

hello(); // TypeError — function expression, only var is hoisted
var hello = () => "hi";
```

---

**Q: What is the Temporal Dead Zone (TDZ)?**

**Short:** The period between entering a block scope and the `let`/`const` declaration being initialized — accessing the variable in this window throws `ReferenceError`.

**Detailed:**
```javascript
{
  // TDZ for x starts here
  console.log(x); // ReferenceError
  let x = 5;      // TDZ ends here
  console.log(x); // 5
}
```
This prevents the confusing `undefined` behavior of `var` — forces you to declare before use.

---

**Q: What is a closure?**

**Short:** A function that remembers and accesses variables from its outer scope even after the outer function has returned.

**Detailed:**
```javascript
function counter() {
  let count = 0;
  return {
    increment: () => ++count,
    get: () => count
  };
}
const c = counter();
c.increment(); // 1
c.increment(); // 2
c.get();       // 2
// count is private — only accessible through the returned object
```
Closures enable data privacy, factory functions, and memoization. Each call to `counter()` creates a fresh `count`.

---

**Q: Explain the four rules of `this`.**

**Short:** `this` depends on HOW a function is called, not where it's defined.

**Detailed:**
1. **Default binding:** `this` = global object (`window`) or `undefined` (strict mode) when called as a plain function.
2. **Implicit binding:** `this` = the object before the dot — `obj.method()` → `this` is `obj`.
3. **Explicit binding:** `call(obj)`, `apply(obj)`, `bind(obj)` — force `this` to be `obj`.
4. **New binding:** `new Fn()` → `this` is the newly created object.
5. **Arrow functions:** No own `this` — lexically inherits from parent scope. `call/apply/bind` can't override it.

```javascript
const obj = { name: "A", greet() { console.log(this.name); } };
obj.greet();         // "A" — implicit
const fn = obj.greet;
fn();                // undefined — default (lost context)
fn.call(obj);        // "A" — explicit
```

---

**Q: What is the difference between `==` and `===`?**

**Short:** `===` (strict equality) checks type AND value. `==` (loose equality) coerces types first.

**Detailed:**
```javascript
1 == "1"    // true  — string "1" coerced to number 1
1 === "1"   // false — different types
null == undefined  // true  — special case
null === undefined // false
0 == false  // true
0 === false // false
```
Always use `===` unless you specifically need type coercion. `typeof null === "object"` is a famous bug in JS.

---

**Q: What is the difference between `null` and `undefined`?**

**Short:** `undefined` = variable declared but no value assigned. `null` = intentionally empty value assigned by code.

**Detailed:**
```javascript
let x;           // undefined — declared, no value
let y = null;    // null — explicitly set to "nothing"
typeof undefined // "undefined"
typeof null      // "object" ← famous JS bug
null == undefined   // true
null === undefined  // false
```

---

**Q: How does the Event Loop work? Microtask vs Macrotask?**

**Short:** Microtasks (Promises) run before the next macrotask (setTimeout). The event loop always drains the microtask queue first.

**Detailed:**
```javascript
console.log("1");
setTimeout(() => console.log("2"), 0);   // macrotask
Promise.resolve().then(() => console.log("3")); // microtask
console.log("4");
// Output: 1, 4, 3, 2
```
- **Call stack:** executes synchronous code
- **Microtask queue:** Promises `.then()`, `queueMicrotask()` — drained AFTER each task, BEFORE next macrotask
- **Macrotask queue:** `setTimeout`, `setInterval`, I/O — one at a time

---

**Q: What are the Promise static methods and when to use each?**

**Short:** `all` (all succeed), `allSettled` (all finish regardless), `race` (first settles), `any` (first succeeds).

**Detailed:**
```javascript
Promise.all([p1, p2])         // resolves when ALL resolve, rejects if ANY rejects
Promise.allSettled([p1, p2])  // resolves when ALL finish (never rejects), gives {status, value/reason}
Promise.race([p1, p2])        // settles when FIRST settles (resolve or reject)
Promise.any([p1, p2])         // resolves when FIRST resolves, rejects if ALL reject (AggregateError)
```
Use `allSettled` when you need results from all even if some fail (e.g., dashboard widgets).

---

**Q: What is optional chaining (`?.`) and nullish coalescing (`??`)?**

**Short:** `?.` safely accesses nested properties without throwing on null/undefined. `??` returns right side only if left is null/undefined (unlike `||` which catches all falsy).

**Detailed:**
```javascript
const user = null;
user?.address?.city   // undefined (no error)
user.address.city     // TypeError

const val = 0;
val || "default"      // "default" — 0 is falsy
val ?? "default"      // 0 — only null/undefined triggers ??
```

---

**Q: How does the prototype chain work?**

**Short:** Every object has a `[[Prototype]]` link to another object. Property lookup walks up this chain until it finds the property or reaches `null`.

**Detailed:**
```javascript
const animal = { breathe() { return "breathing"; } };
const dog = Object.create(animal);  // dog's prototype = animal
dog.bark = () => "woof";

dog.bark();     // found on dog directly
dog.breathe();  // not on dog → look at prototype (animal) → found
dog.fly();      // not on dog, not on animal, not on Object.prototype → undefined

dog.__proto__ === animal    // true
animal.__proto__ === Object.prototype  // true
```

---

**Q: What are higher-order array methods? Explain map, filter, reduce.**

**Short:** Functions that take/return functions. `map` transforms, `filter` selects, `reduce` accumulates.

**Detailed:**
```javascript
const nums = [1, 2, 3, 4, 5];

nums.map(x => x * 2)         // [2, 4, 6, 8, 10] — new array, same length
nums.filter(x => x % 2 === 0) // [2, 4] — new array, smaller/equal length
nums.reduce((acc, x) => acc + x, 0) // 15 — single accumulated value
```
None of these mutate the original array. Chain them: `nums.filter(x => x > 2).map(x => x * 3)`.

---

**Q: What is the difference between `async/await` and Promises?**

**Short:** `async/await` is syntactic sugar over Promises — same underlying mechanism, cleaner syntax for sequential async code.

**Detailed:**
```javascript
// Promise chain
fetch(url).then(r => r.json()).then(data => process(data)).catch(err => handle(err));

// async/await — equivalent, reads like sync code
async function load() {
  try {
    const r = await fetch(url);
    const data = await r.json();
    process(data);
  } catch (err) {
    handle(err);
  }
}
```
Parallel execution: `const [a, b] = await Promise.all([fetchA(), fetchB()])` — don't use sequential `await` when tasks are independent.

---

**Q: What is the Module Pattern and ES Modules?**

**Short:** Module Pattern uses closures for private state. ES Modules (`import`/`export`) are native browser/Node.js modules with static analysis.

**Detailed:**
```javascript
// ES Module
// math.js
export const add = (a, b) => a + b;
export default function multiply(a, b) { return a * b; }

// app.js
import multiply, { add } from './math.js';
import('./heavy.js').then(m => m.doSomething()); // dynamic import — lazy load
```
Named exports vs default export: prefer named for tree-shaking. Dynamic `import()` returns a Promise — useful for code splitting.

---

## Links
- [[Study Plan/JavaScript]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
