# 🟨 JavaScript — Complete Learning Path

---

## 🔰 1. JavaScript Foundations (The Basics)

### 🧱 1.1 Variables & Scoping
- [ ] **Variable Declarations** — `var`, `let`, `const`.
- [ ] **Scoping** — Global scope, Function scope, Block scope.
- [ ] **Hoisting** — How declarations move to the top; Function hoisting vs. Variable hoisting.
- [ ] **Temporal Dead Zone (TDZ)** — Why you can't access `let`/`const` before declaration.
- [ ] **Shadowing** — Declaring variables with the same name in different scopes.

### 💎 1.2 Data Types & Values
- [ ] **Primitive Types** — `string`, `number`, `boolean`, `undefined`, `null`, `symbol`, `bigint`.
- [ ] **Reference Types** — `Object`, `Array`, `Function`.
- [ ] **`typeof` operator** — Checking types and its quirks (e.g., `typeof null`).
- [ ] **Type Coercion** — Implicit vs Explicit conversion (`==` vs `===`).
- [ ] **Truthy & Falsy** — What values evaluate to `false` (0, "", null, undefined, NaN).

### 🕹️ 1.3 Operators & Expressions
- [ ] Arithmetic, Comparison, and Logical operators.
- [ ] **Short-circuiting** (`&&`, `||`).
- [ ] **Nullish Coalescing** (`??`) — Handling null/undefined specifically.
- [ ] **Optional Chaining** (`?.`) — Safely accessing nested properties.
- [ ] Ternary Operator (`condition ? true : false`).

### 🔁 1.4 Control Flow
- [ ] `if`, `else if`, `else`.
- [ ] `switch` statements.
- [ ] **Loops** — `for`, `while`, `do...while`.
- [ ] **Modern Iteration** — `for...of` (values) and `for...in` (keys/index).
- [ ] `break` and `continue`.

---

## ⚙️ 2. Functions & Execution Context

### ⚡ 2.1 Function Mastery
- [ ] **Function Declarations vs. Expressions**.
- [ ] **Arrow Functions** — Syntax and `this` binding differences.
- [ ] **Parameters** — Default parameters, Rest parameters (`...args`).
- [ ] **Return values** — Implicit vs. Explicit returns.
- [ ] **IIFE** (Immediately Invoked Function Expressions).

### 🧠 2.2 Advanced Scope & Closures
- [ ] **Lexical Scoping** — How nested functions access outer variables.
- [ ] **Closures** — Functions remembering their birth environment.
- [ ] **Use Cases for Closures** — Data privacy (private variables), Function factories, Memoization.
- [ ] **The "Module Pattern"** using closures.

### 🎯 2.3 The `this` Keyword
- [ ] **Implicit Binding** — `this` inside an object method.
- [ ] **Explicit Binding** — `call()`, `apply()`, and `bind()`.
- [ ] **New Binding** — `this` inside constructor functions.
- [ ] **Global/Default Binding** — `this` in the global scope or strict mode.
- [ ] **Arrow Function `this`** — Lexical binding (inherits from parent).

---

## 🗃️ 3. Objects, Prototypes & Classes

### 📦 3.1 Object Manipulation
- [ ] Object literals and Property shorthand.
- [ ] **Destructuring** — Extracting values from objects and arrays.
- [ ] **Spread/Rest Operator** (`...`) — Merging objects, cloning arrays.
- [ ] `Object.keys()`, `Object.values()`, `Object.entries()`.
- [ ] `Object.freeze()` vs `Object.seal()`.

### 🧬 3.2 Prototypes (Under the Hood)
- [ ] **The Prototype Chain** — How inheritance works in JS.
- [ ] `__proto__` vs `prototype`.
- [ ] Prototypal Inheritance — Creating objects based on others.
- [ ] `Object.create()`.

### 🏛️ 3.3 ES6 Classes
- [ ] `class` syntax, `constructor`.
- [ ] **Inheritance** — `extends` and `super()`.
- [ ] **Static Methods & Properties**.
- [ ] **Private Fields** (`#variable`) — Encapsulation in modern JS.
- [ ] Getters and Setters (`get`/`set`).

---

## 🌪️ 4. Asynchronous JavaScript

### ⏳ 4.1 The Event Loop
- [ ] **Call Stack** — How JS executes code line by line.
- [ ] **Web APIs / Node APIs** — Offloading tasks (timers, fetch).
- [ ] **Callback Queue (Macrotask)** — `setTimeout`, `setInterval`.
- [ ] **Microtask Queue** — `Promises`, `queueMicrotask`.
- [ ] How the Event Loop prioritizes Microtasks over Macrotasks.

### 🤝 4.2 Promises
- [ ] **Promise States** — Pending, Fulfilled, Rejected.
- [ ] Consuming Promises — `.then()`, `.catch()`, `.finally()`.
- [ ] **Chaining Promises** — Avoiding "Callback Hell".
- [ ] **Promise Static Methods** — `Promise.all`, `Promise.allSettled`, `Promise.any`, `Promise.race`.

### 🚀 4.3 Async / Await
- [ ] `async` functions — Always returning a promise.
- [ ] `await` keyword — Pausing execution without blocking the thread.
- [ ] **Error Handling** — `try...catch` in async functions.
- [ ] Parallel vs Sequential execution with `await`.

---

## 🛠️ 5. Modern Features & Tooling

### 🧪 5.1 Arrays & Iterables
- [ ] **Higher-Order Array Methods** — `map`, `filter`, `reduce`, `forEach`, `find`, `some`, `every`.
- [ ] **Immutability** — Why we don't mutate the original array.
- [ ] **Map & Set** — Modern data structures for unique values and key-value pairs.

### 📦 5.2 Modules (ESM)
- [ ] `export` vs `export default`.
- [ ] `import` statements and Aliasing.
- [ ] Dynamic Imports — `import()`.

### 🌐 5.3 Web APIs (Browser focused)
- [ ] **DOM Manipulation** — `querySelector`, Event Listeners, Bubbling vs Capturing.
- [ ] **Fetch API** — Making network requests.
- [ ] **Web Storage** — `localStorage`, `sessionStorage`, `Cookies`.

---

## 🏁 Recap — JavaScript Foundations Self-Test
- [ ] What is the difference between `null` and `undefined`?
- [ ] Explain the difference between `==` and `===`.
- [ ] What is a closure and why is it useful?
- [ ] How does `hoisting` work for `var` vs `let`?
- [ ] What is the difference between the Microtask queue and the Callback queue?

---

### 🔗 Recommended Resources
- [JavaScript.info](https://javascript.info/)
- [MDN Web Docs - JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [You Don't Know JS (Book Series)](https://github.com/getify/You-Dont-Know-JS)
