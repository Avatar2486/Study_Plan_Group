## Node JS

## 📋 Table of Contents

1. [What is Node.js?](#what-is-nodejs)
2. [Level 1: Basics (Foundation)](#level-1-basics)
3. [Level 2: Intermediate (Core Engineering)](#level-2-intermediate)
4. [Level 3: Advanced (Pro Level)](#level-3-advanced)
5. [OOP in Node.js](#oop-in-nodejs)
6. [Top 50 Interview Questions](#top-50-interview-questions)
7. [Quick Revision Cheatsheet](#quick-revision-cheatsheet)
8. [Learning Resources](#learning-resources)

---

## What is Node.js?

- **Node.js** is a JavaScript runtime built on Chrome's **V8 engine**
- It lets you run JavaScript **outside the browser** — on servers, CLIs, scripts, etc.
- It uses a **non-blocking, event-driven** architecture — meaning it can handle thousands of requests without waiting
- Built on a **single-threaded event loop** (but can use worker threads for CPU-heavy tasks)

### Why Node.js?

- Same language (JS) on frontend and backend
- Extremely fast for I/O operations (file reads, API calls, DB queries)
- Massive npm ecosystem (2M+ packages)
- Used by: Netflix, LinkedIn, Uber, PayPal, NASA

### Node.js vs Browser JS

|Feature|Browser JS|Node.js|
|---|---|---|
|`window` object|✅ Yes|❌ No|
|`document` / DOM|✅ Yes|❌ No|
|`fs` (file system)|❌ No|✅ Yes|
|`http` module|❌ No|✅ Yes|
|`process` object|❌ No|✅ Yes|

---

# Level 1: Basics

## 1.1 Installing Node.js

```bash
# Check if installed
node --version
npm --version

# Run a file
node app.js

# Interactive REPL
node
```

---

## 1.2 Your First Node.js Program

```javascript
// hello.js
console.log("Hello, Node.js!");
console.log("Node version:", process.version);
```

```bash
node hello.js
# Output: Hello, Node.js!
# Output: Node version: v20.x.x
```

---

## 1.3 Variables

```javascript
// var — old, function-scoped, avoid in modern code
var name = "Alice";

// let — block-scoped, can be reassigned
let age = 25;
age = 26; // OK

// const — block-scoped, cannot be reassigned
const PI = 3.14;
// PI = 3.15; // ERROR

// Block scope example
{
  let blockVar = "inside block";
  console.log(blockVar); // Works
}
// console.log(blockVar); // ReferenceError
```

### Common Mistake ⚠️

```javascript
// var leaks outside blocks (not loops/ifs)
if (true) {
  var leaked = "I escape!";
}
console.log(leaked); // "I escape!" — unexpected!

// Fix: use let or const
if (true) {
  let safe = "I stay here";
}
// console.log(safe); // ReferenceError — correct behavior
```

---

## 1.4 Data Types

```javascript
// Primitive types
let str = "Hello";           // String
let num = 42;                // Number
let float = 3.14;            // Number (no separate float type)
let bool = true;             // Boolean
let nothing = null;          // Null (intentional absence)
let undef = undefined;       // Undefined (unassigned)
let big = 9007199254740991n; // BigInt
let sym = Symbol("id");      // Symbol (unique identifier)

// Reference types
let arr = [1, 2, 3];        // Array
let obj = { name: "Bob" };  // Object
let fn = function() {};     // Function

// Type checking
console.log(typeof str);    // "string"
console.log(typeof num);    // "number"
console.log(typeof null);   // "object" — famous JS bug!
console.log(typeof undef);  // "undefined"
console.log(Array.isArray(arr)); // true
```

### Type Coercion (Tricky!)

```javascript
console.log("5" + 2);   // "52"  — string concatenation
console.log("5" - 2);   // 3    — numeric subtraction
console.log("5" * "2"); // 10   — numeric multiplication
console.log(true + 1);  // 2    — true becomes 1
console.log(false + 1); // 1    — false becomes 0
console.log(null + 1);  // 1    — null becomes 0

// Strict equality avoids coercion
console.log(5 == "5");  // true  — loose equality (coerces)
console.log(5 === "5"); // false — strict equality (no coercion)
// ALWAYS use === in real code
```

---

## 1.5 Operators

```javascript
// Arithmetic
let a = 10, b = 3;
console.log(a + b);  // 13
console.log(a - b);  // 7
console.log(a * b);  // 30
console.log(a / b);  // 3.333...
console.log(a % b);  // 1 (remainder)
console.log(a ** b); // 1000 (exponent)

// Assignment
let x = 5;
x += 3;  // x = x + 3 = 8
x -= 2;  // x = x - 2 = 6
x *= 4;  // x = x * 4 = 24
x /= 6;  // x = x / 6 = 4

// Comparison
console.log(5 > 3);   // true
console.log(5 < 3);   // false
console.log(5 >= 5);  // true
console.log(5 !== 4); // true

// Logical
console.log(true && false); // false (AND)
console.log(true || false); // true  (OR)
console.log(!true);         // false (NOT)

// Nullish Coalescing (??) — returns right side only if left is null/undefined
let val = null ?? "default"; // "default"
let val2 = 0 ?? "default";  // 0 (because 0 is not null/undefined)

// Optional Chaining (?.) — safely access nested properties
let user = { profile: { name: "Alice" } };
console.log(user?.profile?.name);   // "Alice"
console.log(user?.address?.city);   // undefined (no error)
```

---

## 1.6 Strings

```javascript
let name = "Alice";
let greeting = `Hello, ${name}!`; // Template literal

// Common string methods
console.log("hello".toUpperCase());       // "HELLO"
console.log("HELLO".toLowerCase());       // "hello"
console.log("  hello  ".trim());          // "hello"
console.log("hello world".split(" "));    // ["hello", "world"]
console.log("hello".includes("ell"));     // true
console.log("hello".startsWith("hel"));  // true
console.log("hello".replace("l", "r"));  // "herlo" (first only)
console.log("hello".replaceAll("l","r")); // "herro"
console.log("hello".slice(1, 3));         // "el"
console.log("hello".indexOf("l"));        // 2
console.log("ha".repeat(3));              // "hahaha"
console.log("hello".length);              // 5
```

---

## 1.7 Arrays

```javascript
let fruits = ["apple", "banana", "cherry"];

// Access
console.log(fruits[0]);       // "apple"
console.log(fruits.length);   // 3

// Modify
fruits.push("date");          // Add to end
fruits.pop();                 // Remove from end
fruits.unshift("avocado");    // Add to start
fruits.shift();               // Remove from start

// Find
console.log(fruits.indexOf("banana"));        // 1
console.log(fruits.includes("cherry"));       // true
console.log(fruits.find(f => f.length > 5)); // "banana"
console.log(fruits.findIndex(f => f === "cherry")); // 2

// Transform
let upper = fruits.map(f => f.toUpperCase());
// ["APPLE", "BANANA", "CHERRY"]

let long = fruits.filter(f => f.length > 5);
// ["banana", "cherry"]

let total = [1,2,3,4].reduce((acc, val) => acc + val, 0);
// 10

// Iterate
fruits.forEach((fruit, index) => {
  console.log(`${index}: ${fruit}`);
});

// Spread
let more = [...fruits, "elderberry", "fig"];

// Destructuring
let [first, second, ...rest] = fruits;
```

---

## 1.8 Objects

```javascript
// Creating objects
let person = {
  name: "Alice",
  age: 30,
  city: "Mumbai",
  greet() {
    return `Hi, I'm ${this.name}`;
  }
};

// Access
console.log(person.name);         // "Alice"
console.log(person["age"]);       // 30

// Modify
person.email = "alice@email.com"; // Add
person.age = 31;                  // Update
delete person.city;               // Delete

// Destructuring
let { name, age } = person;
let { name: fullName } = person;  // Rename

// Spread
let updated = { ...person, age: 32 };

// Object methods
console.log(Object.keys(person));   // ["name", "age", "email", ...]
console.log(Object.values(person)); // ["Alice", 31, ...]
console.log(Object.entries(person));// [["name","Alice"], ...]

// Check property exists
console.log("name" in person);      // true
```

---

## 1.9 Control Flow

```javascript
// if / else if / else
let score = 75;
if (score >= 90) {
  console.log("A grade");
} else if (score >= 75) {
  console.log("B grade");
} else if (score >= 60) {
  console.log("C grade");
} else {
  console.log("Fail");
}

// Ternary operator
let status = score >= 60 ? "Pass" : "Fail";

// Switch
let day = "Monday";
switch (day) {
  case "Monday":
  case "Tuesday":
    console.log("Weekday");
    break;
  case "Saturday":
  case "Sunday":
    console.log("Weekend");
    break;
  default:
    console.log("Unknown");
}
```

---

## 1.10 Loops

```javascript
// for loop
for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}

// while loop
let count = 0;
while (count < 3) {
  console.log(count);
  count++;
}

// do...while (runs at least once)
let n = 0;
do {
  console.log(n);
  n++;
} while (n < 3);

// for...of (iterate values — arrays, strings, Maps, Sets)
let colors = ["red", "green", "blue"];
for (let color of colors) {
  console.log(color);
}

// for...in (iterate keys — objects)
let obj = { a: 1, b: 2, c: 3 };
for (let key in obj) {
  console.log(`${key}: ${obj[key]}`);
}

// break and continue
for (let i = 0; i < 10; i++) {
  if (i === 3) continue; // Skip 3
  if (i === 7) break;    // Stop at 7
  console.log(i);
}
```

---

## 1.11 Functions

```javascript
// Function Declaration (hoisted — can call before definition)
function add(a, b) {
  return a + b;
}
console.log(add(2, 3)); // 5

// Function Expression (NOT hoisted)
const multiply = function(a, b) {
  return a * b;
};

// Arrow Function (shorter syntax, no own 'this')
const divide = (a, b) => a / b;
const square = x => x * x; // Single param, no parens needed
const greet = () => "Hello!"; // No params

// Default Parameters
function greetUser(name = "Guest") {
  return `Hello, ${name}!`;
}
console.log(greetUser());        // "Hello, Guest!"
console.log(greetUser("Alice")); // "Hello, Alice!"

// Rest Parameters
function sum(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}
console.log(sum(1, 2, 3, 4)); // 10

// Spread in function calls
let nums = [1, 2, 3];
console.log(Math.max(...nums)); // 3

// Higher-order functions
function applyTwice(fn, value) {
  return fn(fn(value));
}
console.log(applyTwice(x => x * 2, 3)); // 12

// Callback functions
function doWork(callback) {
  console.log("Working...");
  callback();
}
doWork(() => console.log("Done!"));
```

### Common Mistake ⚠️ — `this` in Arrow vs Regular Functions

```javascript
const obj = {
  name: "Alice",
  // Arrow function — 'this' refers to outer scope (wrong here)
  greetArrow: () => {
    console.log(this.name); // undefined!
  },
  // Regular function — 'this' refers to the object (correct)
  greetRegular() {
    console.log(this.name); // "Alice"
  }
};
obj.greetArrow();   // undefined
obj.greetRegular(); // "Alice"
```

---

## 1.12 Scope and Closures

```javascript
// Scope
let globalVar = "I'm global";

function outer() {
  let outerVar = "I'm in outer";

  function inner() {
    let innerVar = "I'm in inner";
    console.log(globalVar); // Accessible
    console.log(outerVar);  // Accessible (closure)
    console.log(innerVar);  // Accessible
  }
  inner();
  // console.log(innerVar); // Error — not accessible
}

// Closure — function remembers its outer scope even after outer function returns
function makeCounter() {
  let count = 0; // Private variable
  return {
    increment() { count++; },
    decrement() { count--; },
    getCount() { return count; }
  };
}

const counter = makeCounter();
counter.increment();
counter.increment();
counter.increment();
counter.decrement();
console.log(counter.getCount()); // 2
// count is not directly accessible — data hiding via closure
```

---

## 1.13 The `process` Object (Node.js Specific)

```javascript
console.log(process.version);      // Node.js version
console.log(process.platform);     // "linux", "win32", "darwin"
console.log(process.env.NODE_ENV); // Environment variable
console.log(process.argv);         // Command line arguments
console.log(process.cwd());        // Current working directory
console.log(process.memoryUsage()); // Memory stats

// Exit the process
// process.exit(0); // 0 = success, 1 = error
```

---

## 1.14 Beginner Interview Questions

**Q1: What is Node.js and why is it single-threaded?**

> Node.js is a JavaScript runtime built on V8. It's single-threaded in terms of JS execution but uses libuv under the hood for async I/O via a thread pool and event loop. This design allows handling many concurrent connections efficiently.

**Q2: What is the difference between `var`, `let`, and `const`?**

> `var` is function-scoped and hoisted (initialized as `undefined`). `let` is block-scoped and hoisted but not initialized (Temporal Dead Zone). `const` is block-scoped, hoisted but not initialized, and cannot be reassigned (though object contents can be mutated).

**Q3: What is the difference between `==` and `===`?**

> `==` performs type coercion before comparison (e.g., `"5" == 5` is `true`). `===` checks both value and type without coercion (`"5" === 5` is `false`). Always use `===`.

**Q4: What is a closure?**

> A closure is a function that remembers variables from its outer scope even after that outer function has returned. It enables data privacy and stateful functions.

**Q5: What is `typeof null`?**

> `"object"` — this is a historic bug in JavaScript that has never been fixed for backward compatibility.

---

## 1.15 Beginner Practice Problems

**Easy:**

1. Write a function that reverses a string
2. Write a function that checks if a number is prime
3. Write a function that returns the factorial of a number

**Medium:** 4. FizzBuzz: Print 1–100, but "Fizz" for multiples of 3, "Buzz" for 5, "FizzBuzz" for both 5. Find the most frequently occurring element in an array 6. Flatten a nested array one level deep

**Hard:** 7. Implement a `debounce` function 8. Deep clone a JavaScript object without using `JSON.parse/stringify`

---

## 1.16 Mini Project Ideas (Beginner)

1. **CLI Calculator** — Takes two numbers and an operator as command line args, returns result
2. **Number Guessing Game** — Node.js CLI game with readline to guess a random number
3. **To-Do List (in memory)** — Add, remove, list tasks using a JavaScript array

---

# Level 2: Intermediate

## 2.1 Asynchronous JavaScript

Node.js is built for async. You MUST understand this deeply.

### The Event Loop

```
   ┌─────────────────────────────┐
   │        Call Stack           │  ← JS runs here (sync code)
   └──────────────┬──────────────┘
                  │
   ┌──────────────▼──────────────┐
   │         Event Loop          │  ← Watches call stack + queues
   └──────────────┬──────────────┘
          ┌───────┴────────┐
          ▼                ▼
   Microtask Queue    Macrotask Queue
   (Promises,         (setTimeout,
    queueMicrotask)    setInterval,
                       I/O callbacks)
```

**Key Rule:** Microtasks (Promises) always run before Macrotasks (setTimeout).

```javascript
console.log("1 - Start");

setTimeout(() => console.log("4 - setTimeout"), 0);

Promise.resolve().then(() => console.log("3 - Promise"));

console.log("2 - End");

// Output: 1, 2, 3, 4
// Why? Sync first, then microtasks (Promise), then macrotasks (setTimeout)
```

---

### Callbacks

```javascript
// Old-school async pattern
const fs = require("fs");

fs.readFile("./data.txt", "utf8", (error, data) => {
  if (error) {
    console.error("Error:", error.message);
    return;
  }
  console.log("File content:", data);
});

console.log("This runs before file is read!"); // Non-blocking
```

### Callback Hell (The Problem)

```javascript
// Nested callbacks = "Pyramid of Doom"
getUser(userId, (err, user) => {
  if (err) return handleError(err);
  getOrders(user.id, (err, orders) => {
    if (err) return handleError(err);
    getOrderDetails(orders[0].id, (err, details) => {
      if (err) return handleError(err);
      // Getting hard to read...
      processPayment(details, (err, result) => {
        // Even worse!
      });
    });
  });
});
```

---

### Promises

```javascript
// Creating a Promise
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = true;
      if (success) {
        resolve({ data: "Here's your data" });
      } else {
        reject(new Error("Failed to fetch"));
      }
    }, 1000);
  });
};

// Using .then() / .catch() / .finally()
fetchData()
  .then(result => {
    console.log("Got:", result.data);
    return result.data.toUpperCase(); // Chain further
  })
  .then(upper => console.log("Uppercase:", upper))
  .catch(err => console.error("Error:", err.message))
  .finally(() => console.log("Always runs"));

// Promise combinators
Promise.all([fetch1(), fetch2(), fetch3()])
  .then(([r1, r2, r3]) => console.log(r1, r2, r3));
// Fails if ANY promise fails

Promise.allSettled([fetch1(), fetch2(), fetch3()])
  .then(results => results.forEach(r => console.log(r.status)));
// Never fails — gives status of each

Promise.race([fetch1(), fetch2()])
  .then(first => console.log("First resolved:", first));
// Returns whichever resolves/rejects first

Promise.any([fail1(), fetch2(), fetch3()])
  .then(first => console.log("First SUCCESS:", first));
// Returns first SUCCESSFUL result
```

---

### Async/Await (Modern & Clean)

```javascript
const fs = require("fs").promises;

async function readAndProcess() {
  try {
    // await pauses execution until promise resolves
    const data = await fs.readFile("./data.txt", "utf8");
    console.log("Data:", data);

    const processed = data.toUpperCase();
    await fs.writeFile("./output.txt", processed);
    console.log("Written successfully");

  } catch (error) {
    console.error("Something went wrong:", error.message);
  } finally {
    console.log("Cleanup here");
  }
}

readAndProcess();

// Parallel execution with async/await
async function fetchAll() {
  // Sequential (slow — waits for each)
  const a = await fetch1();
  const b = await fetch2();

  // Parallel (fast — runs simultaneously)
  const [x, y] = await Promise.all([fetch1(), fetch2()]);
}
```

---

## 2.2 Modules (CommonJS vs ES Modules)

### CommonJS (Default in Node.js)

```javascript
// math.js — exporting
function add(a, b) { return a + b; }
function subtract(a, b) { return a - b; }
const PI = 3.14159;

module.exports = { add, subtract, PI };
// OR export a single thing:
// module.exports = add;

// app.js — importing
const { add, subtract, PI } = require("./math");
// OR:
const math = require("./math");
math.add(2, 3);

// Built-in modules
const fs = require("fs");
const path = require("path");
const http = require("http");
const os = require("os");
```

### ES Modules (Modern — requires `"type": "module"` in package.json)

```javascript
// math.mjs or with "type": "module" in package.json
export function add(a, b) { return a + b; }
export const PI = 3.14159;
export default function multiply(a, b) { return a * b; }

// app.mjs
import multiply, { add, PI } from "./math.js";
import * as math from "./math.js"; // Import everything
```

### CommonJS vs ES Modules

|Feature|CommonJS|ES Modules|
|---|---|---|
|Syntax|`require()` / `module.exports`|`import` / `export`|
|Loading|Synchronous|Asynchronous|
|Default in Node.js|✅ Yes|With config|
|Tree shaking|❌ No|✅ Yes|
|Top-level await|❌ No|✅ Yes|

---

## 2.3 npm & package.json

```bash
# Initialize a project
npm init -y

# Install a package
npm install express          # Production dependency
npm install nodemon --save-dev # Dev dependency only
npm install -g nodemon       # Global install

# Remove package
npm uninstall express

# Run scripts
npm start
npm test
npm run dev
```

```json
// package.json
{
  "name": "my-app",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.2"
  },
  "devDependencies": {
    "nodemon": "^3.0.0",
    "jest": "^29.0.0"
  }
}
```

### Semantic Versioning

```
^4.18.2  →  Compatible with 4.x.x  (major locked)
~4.18.2  →  Compatible with 4.18.x (major + minor locked)
4.18.2   →  Exact version only
```

---

## 2.4 File System Module

```javascript
const fs = require("fs");
const fsPromises = require("fs").promises;
const path = require("path");

// --- Synchronous (blocks execution — avoid in production servers) ---
const data = fs.readFileSync("./file.txt", "utf8");
fs.writeFileSync("./out.txt", "Hello");

// --- Async with callbacks ---
fs.readFile("./file.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});

// --- Async with Promises (recommended) ---
async function fileOps() {
  // Read
  const content = await fsPromises.readFile("./file.txt", "utf8");

  // Write (overwrites)
  await fsPromises.writeFile("./out.txt", "New content");

  // Append
  await fsPromises.appendFile("./out.txt", "\nMore content");

  // Delete
  await fsPromises.unlink("./temp.txt");

  // Create directory
  await fsPromises.mkdir("./newFolder", { recursive: true });

  // List directory
  const files = await fsPromises.readdir("./");
  console.log(files);

  // Check if file exists
  try {
    await fsPromises.access("./file.txt");
    console.log("File exists");
  } catch {
    console.log("File not found");
  }

  // Get file stats
  const stats = await fsPromises.stat("./file.txt");
  console.log(stats.size, stats.isFile(), stats.isDirectory());
}

// Path module
console.log(path.join(__dirname, "files", "data.txt")); // Safe path joining
console.log(path.basename("/foo/bar/file.txt"));         // "file.txt"
console.log(path.extname("file.txt"));                   // ".txt"
console.log(path.dirname("/foo/bar/file.txt"));           // "/foo/bar"
console.log(path.resolve("./relative"));                  // Absolute path
```

---

## 2.5 HTTP Module & Building a Server

```javascript
const http = require("http");

const server = http.createServer((req, res) => {
  // req = incoming request
  // res = outgoing response

  console.log(`${req.method} ${req.url}`);

  // Route handling
  if (req.url === "/" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "text/html" });
    res.end("<h1>Welcome!</h1>");

  } else if (req.url === "/api/users" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "application/json" });
    res.end(JSON.stringify({ users: ["Alice", "Bob"] }));

  } else if (req.url === "/api/users" && req.method === "POST") {
    let body = "";
    req.on("data", chunk => { body += chunk; });
    req.on("end", () => {
      const user = JSON.parse(body);
      res.writeHead(201, { "Content-Type": "application/json" });
      res.end(JSON.stringify({ created: user }));
    });

  } else {
    res.writeHead(404, { "Content-Type": "application/json" });
    res.end(JSON.stringify({ error: "Not found" }));
  }
});

server.listen(3000, () => {
  console.log("Server running on http://localhost:3000");
});
```

---

## 2.6 Express.js (The Standard Web Framework)

```bash
npm install express
```

```javascript
const express = require("express");
const app = express();

// Middleware — runs on every request
app.use(express.json());                     // Parse JSON bodies
app.use(express.urlencoded({ extended: true })); // Parse form data

// Custom middleware
app.use((req, res, next) => {
  console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
  next(); // MUST call next() to continue to next middleware/route
});

// Routes
app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.get("/users/:id", (req, res) => {
  const { id } = req.params;         // URL params
  const { page } = req.query;        // Query string (?page=2)
  res.json({ userId: id, page });
});

app.post("/users", (req, res) => {
  const user = req.body;             // Request body
  // ... save to DB
  res.status(201).json({ created: user });
});

app.put("/users/:id", (req, res) => {
  res.json({ updated: req.params.id });
});

app.delete("/users/:id", (req, res) => {
  res.json({ deleted: req.params.id });
});

// Error handling middleware (MUST have 4 params)
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: err.message });
});

app.listen(3000, () => console.log("Server on port 3000"));
```

### Express Router (Organizing Routes)

```javascript
// routes/users.js
const express = require("express");
const router = express.Router();

router.get("/", (req, res) => res.json({ users: [] }));
router.get("/:id", (req, res) => res.json({ user: req.params.id }));
router.post("/", (req, res) => res.status(201).json({ created: true }));

module.exports = router;

// app.js
const usersRouter = require("./routes/users");
app.use("/api/users", usersRouter);
// Now: GET /api/users, GET /api/users/123, POST /api/users
```

---

## 2.7 Error Handling

```javascript
// Types of errors in Node.js

// 1. Synchronous errors — use try/catch
try {
  JSON.parse("invalid json");
} catch (error) {
  console.error("Type:", error.constructor.name); // SyntaxError
  console.error("Message:", error.message);
  console.error("Stack:", error.stack);
}

// 2. Async errors with Promises
fetchData()
  .then(data => process(data))
  .catch(err => console.error("Promise error:", err));

// 3. Async/await errors — use try/catch
async function main() {
  try {
    const data = await fetchData();
  } catch (err) {
    if (err.code === "ENOENT") {
      console.error("File not found");
    } else if (err.code === "EACCES") {
      console.error("Permission denied");
    } else {
      throw err; // Re-throw unexpected errors
    }
  }
}

// 4. Custom error classes
class ValidationError extends Error {
  constructor(message, field) {
    super(message);
    this.name = "ValidationError";
    this.field = field;
    this.statusCode = 400;
  }
}

class NotFoundError extends Error {
  constructor(resource) {
    super(`${resource} not found`);
    this.name = "NotFoundError";
    this.statusCode = 404;
  }
}

// Usage
function validateUser(user) {
  if (!user.email) throw new ValidationError("Email required", "email");
  if (!user.name)  throw new ValidationError("Name required", "name");
}

// 5. Unhandled rejections — always catch these!
process.on("unhandledRejection", (reason, promise) => {
  console.error("Unhandled Promise Rejection:", reason);
  // In production: log and gracefully shutdown
  process.exit(1);
});

process.on("uncaughtException", (error) => {
  console.error("Uncaught Exception:", error);
  process.exit(1);
});
```

---

## 2.8 Streams

Streams let you handle large data in chunks without loading everything into memory.

```javascript
const fs = require("fs");
const zlib = require("zlib");

// Types: Readable, Writable, Duplex (both), Transform (modify data)

// Reading large file in chunks
const readStream = fs.createReadStream("bigfile.txt", { encoding: "utf8" });
readStream.on("data", chunk => console.log("Chunk:", chunk.length));
readStream.on("end", () => console.log("Done"));
readStream.on("error", err => console.error(err));

// Piping streams (most powerful pattern)
// Read file → compress → write compressed file
fs.createReadStream("input.txt")
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream("output.txt.gz"))
  .on("finish", () => console.log("Compressed!"));

// HTTP response IS a writable stream
const http = require("http");
http.createServer((req, res) => {
  const fileStream = fs.createReadStream("bigfile.txt");
  fileStream.pipe(res); // Stream file directly to HTTP response
}).listen(3000);
```

---

## 2.9 Events (EventEmitter)

```javascript
const EventEmitter = require("events");

class OrderSystem extends EventEmitter {
  placeOrder(order) {
    console.log("Processing order...");
    // Emit events for different stages
    this.emit("order:placed", order);
    setTimeout(() => this.emit("order:shipped", order), 1000);
    setTimeout(() => this.emit("order:delivered", order), 3000);
  }
}

const orders = new OrderSystem();

// Listen to events
orders.on("order:placed", (order) => {
  console.log(`Email sent for order ${order.id}`);
});

orders.on("order:shipped", (order) => {
  console.log(`SMS: Order ${order.id} is on the way!`);
});

orders.on("order:delivered", (order) => {
  console.log(`Order ${order.id} delivered. Requesting review.`);
});

// One-time listener
orders.once("order:placed", () => {
  console.log("First order placed ever!");
});

// Trigger
orders.placeOrder({ id: "ORD-001", item: "Laptop" });
```

---

## 2.10 Environment Variables

```bash
npm install dotenv
```

```javascript
// .env file (NEVER commit to git!)
// PORT=3000
// DB_URL=mongodb://localhost:27017/mydb
// JWT_SECRET=supersecretkey123
// NODE_ENV=development

// app.js
require("dotenv").config(); // Load .env file

const port = process.env.PORT || 3000;
const dbUrl = process.env.DB_URL;
const env = process.env.NODE_ENV || "development";

console.log(`Running in ${env} mode on port ${port}`);
```

---

## 2.11 Debugging Node.js

```bash
# Built-in debugger
node --inspect app.js
# Open chrome://inspect in Chrome

# With breakpoint in code
# Add: debugger; anywhere in your code

# Debug with VS Code
# Add launch.json configuration

# Useful debug logging
node --trace-warnings app.js
node --trace-deprecation app.js

# Environment-based logging
const DEBUG = process.env.DEBUG === "true";
function log(...args) {
  if (DEBUG) console.log(...args);
}
```

---

## 2.12 Intermediate Interview Questions

**Q1: What is the difference between `process.nextTick()`, `setImmediate()`, and `setTimeout(fn, 0)`?**

> `process.nextTick()` runs before any I/O events, before Promises, at the end of the current operation. `Promise.then`(microtask queue) runs next. `setImmediate()` runs in the check phase of the event loop after I/O. `setTimeout(fn, 0)`runs in the timers phase. Order: `nextTick` → `Promise` → `setImmediate` ≈ `setTimeout(0)`.

**Q2: What is middleware in Express?**

> Middleware is a function with `(req, res, next)` signature that has access to request and response objects. It can execute code, modify req/res, end the request-response cycle, or call `next()` to pass control to the next middleware. Used for logging, auth, parsing bodies, error handling.

**Q3: What is the difference between `require()` and `import`?**

> `require()` is CommonJS — synchronous, can be conditional, returns cached module. `import` is ES Module — static analysis, async, better tree-shaking. Node.js supports both but they cannot be freely mixed.

**Q4: What are streams and why use them?**

> Streams process data in chunks rather than loading it all into memory. Use them for large files, HTTP responses, real-time data. Without streams, reading a 4GB file would require 4GB of RAM. With streams, you use minimal memory.

**Q5: How does Node.js handle concurrent requests despite being single-threaded?**

> Node.js delegates I/O operations (file system, network, DB) to the OS or libuv thread pool. While those complete in the background, the JS thread handles other requests. Callbacks/Promises resume execution when async operations complete. CPU-bound work would block — use Worker Threads for that.

---

## 2.13 Intermediate Practice Problems

**Real-world:**

1. Build a URL shortener API (Express + in-memory storage)
2. Create a file watcher that logs changes using `fs.watch`
3. Build a rate limiter middleware for Express
4. Create a custom EventEmitter-based pub/sub system

---

## 2.14 Intermediate Project Ideas

1. **REST API with Express** — CRUD for a blog (posts, comments, users) with proper routing and error handling
2. **File Upload & Processing** — Accept file uploads, stream to disk, and report stats
3. **Real-time Chat Server** — Using `ws` (WebSocket) package and EventEmitter

---

# Level 3: Advanced

## 3.1 Node.js Internals — The Event Loop in Depth

```
 ┌───────────────────────────────────────┐
 │           Event Loop Phases           │
 │                                       │
 │  1. timers      → setTimeout/Interval │
 │  2. pending I/O → previous I/O errors │
 │  3. idle/prepare→ internal only       │
 │  4. poll        → new I/O events      │
 │  5. check       → setImmediate        │
 │  6. close       → socket.on("close")  │
 │                                       │
 │  Between each phase:                  │
 │    - process.nextTick queue (drained) │
 │    - Promise microtask queue (drained)│
 └───────────────────────────────────────┘
```

```javascript
// Execution order demonstration
setImmediate(() => console.log("5 - setImmediate"));
setTimeout(() => console.log("4 - setTimeout"), 0);
process.nextTick(() => console.log("2 - nextTick"));
Promise.resolve().then(() => console.log("3 - Promise"));
console.log("1 - Synchronous");

// Output: 1, 2, 3, 4 or 5 (timer order varies), 5 or 4
```

---

## 3.2 Worker Threads (CPU-Bound Tasks)

```javascript
// main.js
const { Worker, isMainThread, parentPort, workerData } = require("worker_threads");

if (isMainThread) {
  // Main thread — spawn workers for CPU tasks
  function runWorker(data) {
    return new Promise((resolve, reject) => {
      const worker = new Worker(__filename, { workerData: data });
      worker.on("message", resolve);
      worker.on("error", reject);
      worker.on("exit", code => {
        if (code !== 0) reject(new Error(`Worker exited with code ${code}`));
      });
    });
  }

  async function main() {
    console.log("Starting heavy computation...");
    const [r1, r2] = await Promise.all([
      runWorker({ start: 0, end: 1_000_000 }),
      runWorker({ start: 1_000_000, end: 2_000_000 })
    ]);
    console.log("Result:", r1 + r2);
  }
  main();

} else {
  // Worker thread — does the CPU work
  const { start, end } = workerData;
  let sum = 0;
  for (let i = start; i < end; i++) sum += i;
  parentPort.postMessage(sum);
}
```

---

## 3.3 Cluster Module (Multi-Process)

```javascript
const cluster = require("cluster");
const os = require("os");
const http = require("http");

if (cluster.isPrimary) {
  const numCPUs = os.cpus().length;
  console.log(`Primary ${process.pid} forking ${numCPUs} workers`);

  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on("exit", (worker, code, signal) => {
    console.log(`Worker ${worker.process.pid} died. Restarting...`);
    cluster.fork(); // Auto-restart dead workers
  });

} else {
  // Worker processes — each runs this
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end(`Handled by worker ${process.pid}`);
  }).listen(3000);

  console.log(`Worker ${process.pid} started`);
}
```

---

## 3.4 Caching Strategies

```javascript
// In-memory cache (simple)
class Cache {
  constructor(ttlSeconds = 300) {
    this.store = new Map();
    this.ttl = ttlSeconds * 1000;
  }

  set(key, value) {
    this.store.set(key, {
      value,
      expires: Date.now() + this.ttl
    });
  }

  get(key) {
    const item = this.store.get(key);
    if (!item) return null;
    if (Date.now() > item.expires) {
      this.store.delete(key);
      return null;
    }
    return item.value;
  }

  delete(key) { this.store.delete(key); }
  clear() { this.store.clear(); }
}

// Memoization — cache function results
function memoize(fn) {
  const cache = new Map();
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

const expensiveFn = memoize((n) => {
  // Heavy computation
  return n * n;
});
```

---

## 3.5 Performance Optimization

```javascript
// 1. Use streaming for large data
// BAD:
const data = fs.readFileSync("bigfile.csv"); // Loads all into memory

// GOOD:
fs.createReadStream("bigfile.csv")
  .pipe(csvParser())
  .on("data", row => processRow(row));

// 2. Avoid blocking the event loop
// BAD — blocks all requests for 5 seconds:
app.get("/compute", (req, res) => {
  let sum = 0;
  for (let i = 0; i < 10_000_000_000; i++) sum += i; // BLOCKS!
  res.json({ sum });
});

// GOOD — offload to Worker Thread:
app.get("/compute", async (req, res) => {
  const sum = await runInWorker(heavyComputation);
  res.json({ sum });
});

// 3. Connection pooling for databases
const pool = mysql.createPool({
  connectionLimit: 10, // Reuse connections instead of creating new ones
  host: "localhost",
  database: "mydb"
});

// 4. Compress HTTP responses
const compression = require("compression");
app.use(compression()); // Gzip all responses

// 5. Use Buffer for binary data (avoid string conversion)
const buf = Buffer.from("Hello");  // More efficient than string
const hex = buf.toString("hex");

// 6. Profile with built-in tools
// node --prof app.js (generates V8 profile)
// node --prof-process isolate-*.log > processed.txt
```

---

## 3.6 Memory Management

```javascript
// Monitor memory
setInterval(() => {
  const mem = process.memoryUsage();
  console.log({
    heapUsed: `${Math.round(mem.heapUsed / 1024 / 1024)}MB`,
    heapTotal: `${Math.round(mem.heapTotal / 1024 / 1024)}MB`,
    external: `${Math.round(mem.external / 1024 / 1024)}MB`,
    rss: `${Math.round(mem.rss / 1024 / 1024)}MB`,
  });
}, 5000);

// Common memory leaks to avoid:

// 1. Growing arrays/maps without cleanup
const cache = new Map();
// BAD: cache grows forever
setInterval(() => cache.set(Date.now(), getLargeObject()), 100);
// FIX: Use LRU cache or TTL

// 2. Event listener leaks
const emitter = new EventEmitter();
// BAD: keeps adding listeners
setInterval(() => emitter.on("data", handler), 100);
// FIX: Remove listeners when done
emitter.removeListener("data", handler);
// OR: emitter.removeAllListeners("data");

// 3. Closures holding large references
function createLeak() {
  const largeData = new Array(1_000_000).fill("data");
  return () => largeData.length; // Closure keeps largeData alive!
}
// FIX: Only capture what you need
function noLeak() {
  const largeData = new Array(1_000_000).fill("data");
  const length = largeData.length; // Capture the value, not the array
  return () => length;
}

// WeakMap/WeakSet for object-keyed caches (GC can collect keys)
const weakCache = new WeakMap();
function getFromCache(obj) {
  if (weakCache.has(obj)) return weakCache.get(obj);
  const result = compute(obj);
  weakCache.set(obj, result);
  return result;
}
```

---

## 3.7 Design Patterns in Node.js

### Singleton Pattern

```javascript
// database.js — ensure only one DB connection
class Database {
  constructor() {
    if (Database.instance) {
      return Database.instance;
    }
    this.connection = null;
    Database.instance = this;
  }

  async connect(url) {
    if (this.connection) return this.connection;
    this.connection = await createConnection(url);
    return this.connection;
  }
}

module.exports = new Database(); // Export instance (CommonJS module caching ensures singleton)
```

### Factory Pattern

```javascript
class UserFactory {
  static create(type, data) {
    switch (type) {
      case "admin":
        return new AdminUser(data);
      case "editor":
        return new EditorUser(data);
      case "viewer":
        return new ViewerUser(data);
      default:
        throw new Error(`Unknown user type: ${type}`);
    }
  }
}

const user = UserFactory.create("admin", { name: "Alice" });
```

### Observer Pattern

```javascript
class EventBus {
  constructor() { this.listeners = {}; }

  subscribe(event, callback) {
    if (!this.listeners[event]) this.listeners[event] = [];
    this.listeners[event].push(callback);
    // Return unsubscribe function
    return () => this.unsubscribe(event, callback);
  }

  unsubscribe(event, callback) {
    this.listeners[event] = this.listeners[event]?.filter(cb => cb !== callback);
  }

  publish(event, data) {
    this.listeners[event]?.forEach(cb => cb(data));
  }
}

const bus = new EventBus();
const unsubscribe = bus.subscribe("userSignup", user => sendWelcomeEmail(user));
bus.publish("userSignup", { name: "Bob" });
unsubscribe(); // Clean up
```

### Middleware Pattern (Chain of Responsibility)

```javascript
class Pipeline {
  constructor() { this.stages = []; }

  use(fn) {
    this.stages.push(fn);
    return this; // Fluent interface
  }

  async run(context) {
    let index = 0;
    const next = async () => {
      if (index < this.stages.length) {
        await this.stages[index++](context, next);
      }
    };
    await next();
    return context;
  }
}

const pipeline = new Pipeline()
  .use(async (ctx, next) => { ctx.step1 = true; await next(); })
  .use(async (ctx, next) => { ctx.step2 = true; await next(); })
  .use(async (ctx, next) => { ctx.step3 = true; await next(); });

const result = await pipeline.run({});
// { step1: true, step2: true, step3: true }
```

---

## 3.8 Security Best Practices

```javascript
// 1. Helmet — set security headers
const helmet = require("helmet");
app.use(helmet());

// 2. Rate limiting
const rateLimit = require("express-rate-limit");
app.use("/api/", rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // Max 100 requests per window
  message: "Too many requests"
}));

// 3. Input validation
const { body, validationResult } = require("express-validator");
app.post("/users", [
  body("email").isEmail().normalizeEmail(),
  body("password").isLength({ min: 8 }),
  body("name").trim().notEmpty().escape()
], (req, res) => {
  const errors = validationResult(req);
  if (!errors.isEmpty()) {
    return res.status(400).json({ errors: errors.array() });
  }
  // Proceed with validated data
});

// 4. JWT Authentication
const jwt = require("jsonwebtoken");

function generateToken(userId) {
  return jwt.sign({ id: userId }, process.env.JWT_SECRET, {
    expiresIn: "24h",
    issuer: "my-app",
    audience: "my-app-users"
  });
}

function authMiddleware(req, res, next) {
  const token = req.headers.authorization?.split(" ")[1]; // "Bearer <token>"
  if (!token) return res.status(401).json({ error: "No token" });
  try {
    req.user = jwt.verify(token, process.env.JWT_SECRET);
    next();
  } catch {
    res.status(401).json({ error: "Invalid token" });
  }
}

// 5. Never log sensitive data
// BAD:
console.log("User logged in:", { email, password }); // NEVER log passwords!
// GOOD:
console.log("User logged in:", { email });

// 6. SQL Injection prevention — ALWAYS use parameterized queries
// BAD:
db.query(`SELECT * FROM users WHERE id = ${userId}`); // Injectable!
// GOOD:
db.query("SELECT * FROM users WHERE id = ?", [userId]);
```

---

## 3.9 Testing

```bash
npm install --save-dev jest supertest
```

```javascript
// math.js
function add(a, b) { return a + b; }
module.exports = { add };

// math.test.js
const { add } = require("./math");

describe("add function", () => {
  test("adds two numbers", () => {
    expect(add(2, 3)).toBe(5);
  });

  test("handles negative numbers", () => {
    expect(add(-1, 1)).toBe(0);
  });

  test("handles zero", () => {
    expect(add(0, 0)).toBe(0);
  });
});

// API testing with supertest
const request = require("supertest");
const app = require("./app");

describe("GET /api/users", () => {
  test("returns 200 with users array", async () => {
    const response = await request(app).get("/api/users");
    expect(response.status).toBe(200);
    expect(response.body).toHaveProperty("users");
    expect(Array.isArray(response.body.users)).toBe(true);
  });
});

// Mocking
jest.mock("./database", () => ({
  findUser: jest.fn().mockResolvedValue({ id: 1, name: "Alice" })
}));
```

---

## 3.10 Advanced Interview Questions

**Q1: How would you prevent memory leaks in a long-running Node.js process?**

> Use `WeakMap`/`WeakSet` for object-keyed caches. Always remove event listeners when done. Use streams instead of buffering large data. Set TTLs on caches. Profile with `--inspect` and Chrome DevTools heap snapshots. Monitor `process.memoryUsage()`.

**Q2: What is the difference between `cluster` and `worker_threads`?**

> `cluster` creates multiple processes (each with own memory, event loop, V8) — ideal for scaling HTTP servers across CPUs. `worker_threads` creates threads within one process (shared memory via `SharedArrayBuffer`) — ideal for CPU-bound tasks that need shared data.

**Q3: How would you handle backpressure in streams?**

> Backpressure occurs when a writable stream can't keep up with a readable. Use `.pipe()` which handles it automatically, or manually check `writable.write()` return value — if `false`, pause the readable and resume on the `drain` event.

**Q4: How would you design a graceful shutdown for a Node.js server?**

> Listen for `SIGTERM` signal. Stop accepting new requests. Wait for in-flight requests to complete. Close DB connections and other resources. Then exit.

```javascript
const server = app.listen(3000);

process.on("SIGTERM", () => {
  console.log("Shutting down gracefully...");
  server.close(() => {
    db.pool.end(() => {
      console.log("All connections closed");
      process.exit(0);
    });
  });
});
```

---

## 3.11 Advanced Project Ideas

1. **Microservices Architecture** — Split a monolith into auth, users, orders services communicating via REST + message queue (Bull/Redis)
2. **Real-time Collaborative Document Editor** — WebSockets + operational transforms + Redis pub/sub for scaling
3. **API Gateway** — Rate limiting, auth, routing, load balancing, circuit breaker — production-grade from scratch

---

# OOP in Node.js

## 4.1 Classes and Objects

```javascript
class Animal {
  // Private field (ES2022)
  #name;
  #sound;

  constructor(name, sound) {
    this.#name = name;
    this.#sound = sound;
    this.alive = true; // Public property
  }

  // Public method
  speak() {
    return `${this.#name} says ${this.#sound}!`;
  }

  // Getter
  get name() { return this.#name; }

  // Setter with validation
  set name(value) {
    if (typeof value !== "string" || value.length < 1) {
      throw new Error("Name must be a non-empty string");
    }
    this.#name = value;
  }

  // Static method — called on class, not instance
  static createDefault() {
    return new Animal("Unknown", "...");
  }

  // Static property
  static count = 0;

  toString() {
    return `Animal(${this.#name})`;
  }
}

const cat = new Animal("Whiskers", "Meow");
console.log(cat.speak());      // "Whiskers says Meow!"
console.log(cat.name);         // "Whiskers" (via getter)
cat.name = "Felix";            // Via setter
// cat.#name = "Felix";        // ERROR — private field

const generic = Animal.createDefault(); // Static method
```

---

## 4.2 Inheritance

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    return `${this.name} makes a sound`;
  }

  breathe() {
    return `${this.name} is breathing`;
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // MUST call super() first
    this.breed = breed;
  }

  // Override parent method
  speak() {
    return `${this.name} barks! Woof!`;
  }

  // New method
  fetch(item) {
    return `${this.name} fetches the ${item}!`;
  }
}

class GoldenRetriever extends Dog {
  constructor(name) {
    super(name, "Golden Retriever");
  }

  speak() {
    const parentSay = super.speak(); // Call parent's speak
    return `${parentSay} (very happily)`;
  }
}

const dog = new Dog("Rex", "Labrador");
console.log(dog.speak());         // "Rex barks! Woof!"
console.log(dog.breathe());       // Inherited from Animal
console.log(dog instanceof Dog);   // true
console.log(dog instanceof Animal); // true

const golden = new GoldenRetriever("Buddy");
console.log(golden.speak()); // "Buddy barks! Woof! (very happily)"
```

---

## 4.3 Encapsulation

```javascript
class BankAccount {
  #balance;
  #transactions = [];

  constructor(owner, initialBalance = 0) {
    this.owner = owner;            // Public
    this.#balance = initialBalance; // Private
  }

  deposit(amount) {
    if (amount <= 0) throw new Error("Deposit must be positive");
    this.#balance += amount;
    this.#logTransaction("deposit", amount);
    return this;
  }

  withdraw(amount) {
    if (amount <= 0) throw new Error("Amount must be positive");
    if (amount > this.#balance) throw new Error("Insufficient funds");
    this.#balance -= amount;
    this.#logTransaction("withdrawal", amount);
    return this;
  }

  get balance() { return this.#balance; } // Read-only access

  get statement() {
    return this.#transactions.map(t =>
      `${t.type}: $${t.amount} (Balance: $${t.balance})`
    ).join("\n");
  }

  // Private method — internal implementation detail
  #logTransaction(type, amount) {
    this.#transactions.push({ type, amount, balance: this.#balance, date: new Date() });
  }
}

const account = new BankAccount("Alice", 1000);
account.deposit(500).withdraw(200); // Method chaining
console.log(account.balance);  // 1300
// account.#balance = 99999;   // SyntaxError — private!
console.log(account.statement);
```

---

## 4.4 Polymorphism

```javascript
class Shape {
  area() {
    throw new Error("area() must be implemented by subclass");
  }
  perimeter() {
    throw new Error("perimeter() must be implemented by subclass");
  }
  describe() {
    return `${this.constructor.name}: area=${this.area().toFixed(2)}, perimeter=${this.perimeter().toFixed(2)}`;
  }
}

class Circle extends Shape {
  constructor(radius) {
    super();
    this.radius = radius;
  }
  area() { return Math.PI * this.radius ** 2; }
  perimeter() { return 2 * Math.PI * this.radius; }
}

class Rectangle extends Shape {
  constructor(width, height) {
    super();
    this.width = width;
    this.height = height;
  }
  area() { return this.width * this.height; }
  perimeter() { return 2 * (this.width + this.height); }
}

class Triangle extends Shape {
  constructor(a, b, c) {
    super();
    this.sides = [a, b, c];
  }
  area() {
    const s = this.perimeter() / 2;
    const [a, b, c] = this.sides;
    return Math.sqrt(s * (s-a) * (s-b) * (s-c));
  }
  perimeter() { return this.sides.reduce((a, b) => a + b, 0); }
}

// Polymorphism — same method, different behavior
const shapes = [
  new Circle(5),
  new Rectangle(4, 6),
  new Triangle(3, 4, 5)
];

shapes.forEach(shape => console.log(shape.describe()));
// Each calls its own area() and perimeter() implementation

const totalArea = shapes.reduce((sum, shape) => sum + shape.area(), 0);
console.log(`Total area: ${totalArea.toFixed(2)}`);
```

---

## 4.5 Abstraction

```javascript
// Abstract base class pattern (JS has no native abstract classes)
class PaymentProcessor {
  constructor(currency = "USD") {
    if (new.target === PaymentProcessor) {
      throw new Error("PaymentProcessor is abstract — cannot instantiate directly");
    }
    this.currency = currency;
  }

  // Abstract methods — subclasses MUST implement
  async processPayment(amount, details) {
    throw new Error("processPayment() must be implemented");
  }

  async refund(transactionId) {
    throw new Error("refund() must be implemented");
  }

  // Template method — uses abstract methods internally
  async charge(amount, details) {
    console.log(`Initiating ${this.currency} payment of ${amount}`);
    this.#validateAmount(amount);
    const result = await this.processPayment(amount, details);
    await this.#sendReceipt(result);
    return result;
  }

  #validateAmount(amount) {
    if (amount <= 0) throw new Error("Amount must be positive");
  }

  async #sendReceipt(result) {
    console.log("Receipt sent for transaction:", result.id);
  }
}

class StripeProcessor extends PaymentProcessor {
  async processPayment(amount, details) {
    // Stripe-specific implementation
    console.log(`Processing via Stripe: ${amount}`);
    return { id: "stripe_123", status: "success", amount };
  }

  async refund(transactionId) {
    console.log(`Refunding Stripe transaction: ${transactionId}`);
    return { refunded: true };
  }
}

class PayPalProcessor extends PaymentProcessor {
  async processPayment(amount, details) {
    console.log(`Processing via PayPal: ${amount}`);
    return { id: "paypal_456", status: "success", amount };
  }

  async refund(transactionId) {
    console.log(`Refunding PayPal transaction: ${transactionId}`);
    return { refunded: true };
  }
}

// Usage — caller doesn't care WHICH processor
async function checkout(processor, amount) {
  return await processor.charge(amount, { card: "4111..." });
}

const stripe = new StripeProcessor("USD");
checkout(stripe, 99.99);
```

---

## 4.6 OOP Interview Questions

**Q1: What is the difference between `class` and prototype-based inheritance in JavaScript?**

> ES6 `class` is syntactic sugar over prototype-based inheritance. Under the hood, `extends` sets up the prototype chain. `class` syntax is cleaner and more familiar to OOP developers, but the mechanism is the same — objects delegate property lookups up the prototype chain.

**Q2: What does `super()` do?**

> In a constructor, `super()` calls the parent class constructor and must be called before accessing `this`. In methods, `super.method()` calls the parent's implementation of that method.

**Q3: What is the difference between static and instance methods?**

> Instance methods are available on objects created via `new`. Static methods are on the class itself and can't access `this` (instance). Use static for utility functions, factory methods, or logic that doesn't need instance state.

**Q4: How do you implement interfaces in JavaScript?**

> JS has no `interface` keyword. Use abstract base classes that throw if abstract methods aren't implemented, or use duck typing (check if method exists). TypeScript adds proper interfaces.

**Q5: What are private class fields and how do they differ from convention-based privacy?**

> `#field` syntax (ES2022) enforces true privacy — accessing `#field` from outside the class is a syntax error. The old convention `_field` is just a naming hint — not enforced.

---

# Top 50 Interview Questions

## Theory Questions (1–20)

1. **What is Node.js and how does it differ from browser JavaScript?**
    
    > Node.js is a server-side runtime for JavaScript built on V8. It lacks browser APIs (DOM, window) but provides server APIs (fs, http, process). It's event-driven and non-blocking.
    
2. **What is the event loop?**
    
    > A mechanism that picks callbacks from queues and executes them on the call stack. It enables async programming on a single thread by delegating I/O to the OS and running callbacks when they complete.
    
3. **What is `libuv`?**
    
    > A C library that gives Node.js its event loop, thread pool (for fs/crypto/dns), and cross-platform async I/O. The thread pool (default 4 threads) handles operations that can't be done asynchronously by the OS.
    
4. **What are the phases of the event loop?**
    
    > timers → pending callbacks → idle/prepare → poll → check → close callbacks. Between phases: nextTick and Promise microtasks drain.
    
5. **What is the difference between blocking and non-blocking code?**
    
    > Blocking code stops the event loop until complete (`readFileSync`). Non-blocking code initiates work and continues, receiving result via callback/Promise.
    
6. **What is a Promise?**
    
    > An object representing eventual completion or failure of an async operation. States: pending → fulfilled | rejected. Enables chaining with `.then()/.catch()/.finally()`.
    
7. **What is `async/await`?**
    
    > Syntactic sugar over Promises. `async` functions always return a Promise. `await` pauses execution of the async function until the Promise settles (without blocking the event loop).
    
8. **What is `process.nextTick()`?**
    
    > Schedules a callback to run at the end of the current iteration of the event loop, before any I/O events. Runs before Promises.
    
9. **What is the difference between `require()` and dynamic `import()`?**
    
    > `require()` is sync and loads immediately. `import()` returns a Promise and loads asynchronously. Dynamic `import()` can be used conditionally.
    
10. **What is middleware?**
    
    > A function in the request-response cycle that can read/modify req/res, end the cycle, or pass to the next middleware via `next()`.
    
11. **What is CORS and how do you enable it in Node.js?**
    
    > Cross-Origin Resource Sharing — browser security policy that blocks requests from different origins. Enable with the `cors` npm package: `app.use(cors())`.
    
12. **What is the difference between `PUT` and `PATCH`?**
    
    > `PUT` replaces the entire resource. `PATCH` partially updates the resource.
    
13. **What is REST?**
    
    > Representational State Transfer — architectural style using HTTP verbs (GET/POST/PUT/DELETE) on resources (URLs), stateless communication, and standard status codes.
    
14. **How does Node.js handle file operations?**
    
    > Via the `fs` module. Async operations use the libuv thread pool. The JS thread sends the request and gets a callback when done — non-blocking for the event loop.
    
15. **What is a stream?**
    
    > An interface for reading/writing data in chunks rather than all at once. Types: Readable, Writable, Duplex, Transform. Prevents memory issues with large data.
    
16. **What is backpressure in streams?**
    
    > When a readable stream produces data faster than a writable stream can consume it. `.pipe()` handles this automatically by pausing the readable when the writable buffer is full.
    
17. **What is `cluster` module?**
    
    > Allows creating multiple Node.js processes (workers) that share the same server port, enabling multi-core utilization.
    
18. **What is the difference between `cluster` and `worker_threads`?**
    
    > `cluster` = separate processes with separate memory. `worker_threads` = threads within one process with optional shared memory.
    
19. **What is a memory leak in Node.js?**
    
    > Memory that is allocated but never released — happens with unbounded caches, uncleaned event listeners, and closures holding large references.
    
20. **What is `Buffer` in Node.js?**
    
    > A fixed-size chunk of memory for handling binary data (file I/O, TCP streams, crypto). Stored outside V8 heap for efficiency.
    

---

## Coding Questions (21–40)

21. **Implement a deep clone function**

```javascript
function deepClone(obj) {
  if (obj === null || typeof obj !== "object") return obj;
  if (obj instanceof Date) return new Date(obj.getTime());
  if (Array.isArray(obj)) return obj.map(deepClone);
  return Object.fromEntries(
    Object.entries(obj).map(([k, v]) => [k, deepClone(v)])
  );
}
```

22. **Implement Promise.all from scratch**

```javascript
function myPromiseAll(promises) {
  return new Promise((resolve, reject) => {
    if (promises.length === 0) return resolve([]);
    const results = new Array(promises.length);
    let completed = 0;
    promises.forEach((p, i) => {
      Promise.resolve(p).then(val => {
        results[i] = val;
        if (++completed === promises.length) resolve(results);
      }).catch(reject);
    });
  });
}
```

23. **Implement debounce**

```javascript
function debounce(fn, delay) {
  let timer;
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}
```

24. **Implement throttle**

```javascript
function throttle(fn, interval) {
  let lastCall = 0;
  return function(...args) {
    const now = Date.now();
    if (now - lastCall >= interval) {
      lastCall = now;
      return fn.apply(this, args);
    }
  };
}
```

25. **Flatten a deeply nested array**

```javascript
function flatten(arr) {
  return arr.reduce((flat, item) =>
    flat.concat(Array.isArray(item) ? flatten(item) : item), []);
}
// Or: arr.flat(Infinity)
```

26. **Group array of objects by a key**

```javascript
function groupBy(arr, key) {
  return arr.reduce((groups, item) => {
    const group = item[key];
    groups[group] = groups[group] || [];
    groups[group].push(item);
    return groups;
  }, {});
}
```

27. **Implement curry**

```javascript
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    }
    return function(...more) {
      return curried.apply(this, [...args, ...more]);
    };
  };
}
```

28. **Retry a Promise N times**

```javascript
async function retry(fn, retries = 3, delay = 1000) {
  try {
    return await fn();
  } catch (err) {
    if (retries <= 0) throw err;
    await new Promise(r => setTimeout(r, delay));
    return retry(fn, retries - 1, delay * 2); // Exponential backoff
  }
}
```

29. **Implement an LRU Cache**

```javascript
class LRUCache {
  constructor(capacity) {
    this.capacity = capacity;
    this.cache = new Map();
  }

  get(key) {
    if (!this.cache.has(key)) return -1;
    const val = this.cache.get(key);
    this.cache.delete(key);
    this.cache.set(key, val); // Move to end (most recent)
    return val;
  }

  put(key, value) {
    if (this.cache.has(key)) this.cache.delete(key);
    else if (this.cache.size >= this.capacity) {
      this.cache.delete(this.cache.keys().next().value); // Remove oldest
    }
    this.cache.set(key, value);
  }
}
```

30. **Flatten a nested object**

```javascript
function flattenObject(obj, prefix = "") {
  return Object.entries(obj).reduce((flat, [key, value]) => {
    const newKey = prefix ? `${prefix}.${key}` : key;
    if (typeof value === "object" && value !== null && !Array.isArray(value)) {
      Object.assign(flat, flattenObject(value, newKey));
    } else {
      flat[newKey] = value;
    }
    return flat;
  }, {});
}
// { a: { b: { c: 1 } } } → { "a.b.c": 1 }
```

31. **Implement event emitter**

```javascript
class EventEmitter {
  constructor() { this.events = {}; }
  on(event, fn) { (this.events[event] = this.events[event] || []).push(fn); return this; }
  off(event, fn) { this.events[event] = this.events[event]?.filter(f => f !== fn); return this; }
  emit(event, ...args) { this.events[event]?.forEach(fn => fn(...args)); return this; }
  once(event, fn) {
    const wrapper = (...args) => { fn(...args); this.off(event, wrapper); };
    return this.on(event, wrapper);
  }
}
```

32. **Check if two objects are deeply equal**

```javascript
function deepEqual(a, b) {
  if (a === b) return true;
  if (typeof a !== typeof b) return false;
  if (typeof a !== "object" || a === null || b === null) return false;
  const keysA = Object.keys(a), keysB = Object.keys(b);
  if (keysA.length !== keysB.length) return false;
  return keysA.every(key => deepEqual(a[key], b[key]));
}
```

33. **Rate limiter middleware**

```javascript
function createRateLimiter(maxRequests, windowMs) {
  const clients = new Map();
  return (req, res, next) => {
    const key = req.ip;
    const now = Date.now();
    const clientData = clients.get(key) || { count: 0, start: now };
    if (now - clientData.start > windowMs) {
      clientData.count = 0;
      clientData.start = now;
    }
    clientData.count++;
    clients.set(key, clientData);
    if (clientData.count > maxRequests) {
      return res.status(429).json({ error: "Too many requests" });
    }
    next();
  };
}
```

34. **Parse a query string without URLSearchParams**

```javascript
function parseQueryString(qs) {
  return qs.replace(/^\?/, "").split("&")
    .filter(Boolean)
    .reduce((acc, pair) => {
      const [key, value] = pair.split("=").map(decodeURIComponent);
      acc[key] = value;
      return acc;
    }, {});
}
```

35. **Implement pipe function**

```javascript
const pipe = (...fns) => x => fns.reduce((v, f) => f(v), x);
const compose = (...fns) => x => fns.reduceRight((v, f) => f(v), x);

const process = pipe(
  x => x * 2,
  x => x + 1,
  x => x ** 2
);
console.log(process(3)); // ((3*2)+1)^2 = 49
```

---

## Tricky/Edge Case Questions (36–50)

36. **What is the output?**

```javascript
console.log(typeof null);        // "object" (bug)
console.log(null == undefined);  // true (loose)
console.log(null === undefined); // false (strict)
console.log(NaN === NaN);        // false (NaN is not equal to itself)
console.log(typeof NaN);         // "number"
```

37. **What is `this` in different contexts?**

```javascript
const obj = {
  val: 42,
  regular() { return this.val; },     // obj.val = 42
  arrow: () => this?.val,             // undefined (outer this)
};
const fn = obj.regular;
fn(); // undefined (this = global/undefined in strict mode)
```

38. **Explain the output:**

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
// 3, 3, 3 (var is function-scoped, i = 3 when callbacks run)

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
// 0, 1, 2 (let creates new binding per iteration)
```

39. **What does `++` do in these cases?**

```javascript
let a = 5;
console.log(a++); // 5 (post-increment: use then increment)
console.log(a);   // 6
console.log(++a); // 7 (pre-increment: increment then use)
```

40. **What is the Temporal Dead Zone?**

```javascript
console.log(x); // undefined (var is hoisted & initialized)
console.log(y); // ReferenceError (let/const are hoisted but NOT initialized — TDZ)
var x = 5;
let y = 10;
```

41. **What's wrong with this code?**

```javascript
async function main() {
  const results = [];
  const ids = [1, 2, 3];
  ids.forEach(async id => {           // BUG: forEach doesn't await!
    const data = await fetchData(id);
    results.push(data);
  });
  console.log(results); // Always []!
}

// Fix:
async function main() {
  const ids = [1, 2, 3];
  const results = await Promise.all(ids.map(id => fetchData(id)));
  console.log(results); // [data1, data2, data3]
}
```

42. **What is prototype pollution?**

> Modifying `Object.prototype` — affects all objects. Happens with unsafe `merge` functions: `obj[key] = value` where key is `__proto__`. Fix: use `Object.create(null)` for dictionaries, or validate keys.

43. **What's the difference between `Object.freeze()` and `const`?**

> `const` prevents reassignment of the variable binding. `Object.freeze()` prevents modification of the object's properties. Neither is deep — nested objects can still be modified.

44. **What is a Symbol and when would you use it?**

> A unique, immutable primitive. Use for object property keys that shouldn't collide with string keys — useful in mixins, metaprogramming, and defining protocol methods like `Symbol.iterator`.

45. **How do you handle circular references in JSON.stringify?**

```javascript
function safeStringify(obj) {
  const seen = new WeakSet();
  return JSON.stringify(obj, (key, val) => {
    if (typeof val === "object" && val !== null) {
      if (seen.has(val)) return "[Circular]";
      seen.add(val);
    }
    return val;
  });
}
```

46. **What happens when you `require()` the same module twice?**

> Node.js caches the module after first load. The second `require()` returns the cached exports. The module code runs only once.

47. **How would you implement request tracing in a distributed system?**

> Generate a unique `traceId` per request. Pass it via HTTP headers (`X-Trace-ID`). Include it in all log messages. Propagate it to downstream services. Use AsyncLocalStorage for implicit propagation.

48. **What is the `AsyncLocalStorage` and why is it useful?**

```javascript
const { AsyncLocalStorage } = require("async_hooks");
const storage = new AsyncLocalStorage();

app.use((req, res, next) => {
  const traceId = req.headers["x-trace-id"] || generateId();
  storage.run({ traceId }, next); // All async code in this chain has access
});

function log(message) {
  const ctx = storage.getStore();
  console.log(`[${ctx?.traceId}] ${message}`);
}
```

49. **What is `node:` prefix in imports?**

```javascript
const fs = require("node:fs");       // Explicit built-in (Node 16+)
const path = require("node:path");   // Avoids shadowing by npm packages named 'fs'
```

50. **How would you detect and prevent SQL injection in a Node.js app?**

> Always use parameterized queries or prepared statements. Never concatenate user input into queries. Use an ORM. Validate and sanitize all inputs. Use least-privilege DB accounts.

---

# Quick Revision Cheatsheet

## Core Syntax

```javascript
// Variables
const name = "Alice";   // Immutable binding
let age = 25;           // Mutable binding
// var name = "";       // Avoid — use const/let

// Destructuring
const { a, b } = obj;
const [first, ...rest] = arr;

// Spread
const newArr = [...arr, 4, 5];
const newObj = { ...obj, extra: true };

// Arrow function
const fn = (x, y) => x + y;

// Template literal
const msg = `Hello, ${name}!`;

// Optional chaining
const city = user?.address?.city;

// Nullish coalescing
const val = data ?? "default";
```

## Async Patterns

```javascript
// Promise chain
fetch(url).then(r => r.json()).catch(err => console.error(err));

// Async/await
async function get() {
  try {
    const res = await fetch(url);
    return await res.json();
  } catch (err) { /* handle */ }
}

// Parallel
const [a, b] = await Promise.all([fetchA(), fetchB()]);

// Sequential
for (const item of items) {
  await processItem(item); // Waits for each
}
```

## Event Loop Priority (High → Low)

```
1. Synchronous code
2. process.nextTick()
3. Promise callbacks (.then)
4. setImmediate()
5. setTimeout() / setInterval()
6. I/O callbacks
```

## HTTP Status Codes

```
200 OK             201 Created         204 No Content
400 Bad Request    401 Unauthorized    403 Forbidden
404 Not Found      409 Conflict        422 Unprocessable
429 Too Many Req   500 Server Error    503 Service Unavailable
```

## Common Node.js Modules

```javascript
require("fs")      // File system
require("path")    // Path utilities
require("http")    // HTTP server
require("https")   // HTTPS server
require("os")      // OS info
require("events")  // EventEmitter
require("stream")  // Streams
require("crypto")  // Cryptography
require("url")     // URL parsing
require("util")    // Utilities (promisify, etc.)
require("buffer")  // Binary data
require("worker_threads") // CPU parallelism
require("cluster") // Process parallelism
require("child_process")  // Shell commands
```

## Common Mistakes to Avoid

|❌ Mistake|✅ Fix|
|---|---|
|Using `var`|Use `const`/`let`|
|`==` comparison|Use `===` always|
|`forEach` with async|Use `Promise.all` + `map`|
|Unhandled promise rejections|Always `.catch()` or `try/catch`|
|Blocking the event loop with sync I/O|Use async versions|
|Not validating user input|Validate and sanitize everything|
|Hardcoded secrets in code|Use environment variables|
|Manual string SQL queries|Use parameterized queries|
|Infinite event listener growth|Remove listeners when done|
|Ignoring errors in callbacks|Always check the `err` argument first|

## OOP Quick Reference

```javascript
class Animal {
  #sound;                              // Private field
  constructor(name) { this.name = name; }
  speak() { return this.name; }         // Instance method
  get info() { return `${this.name}`; } // Getter
  static create(n) { return new Animal(n); } // Static method
}

class Dog extends Animal {
  constructor(name) { super(name); }   // Call parent constructor
  speak() {                            // Override
    return super.speak() + " barks!"; // Call parent method
  }
}

const d = new Dog("Rex");
d instanceof Dog;    // true
d instanceof Animal; // true
```

---

# Learning Resources

## Official Documentation

- **Node.js Docs:** https://nodejs.org/en/docs
- **npm Docs:** https://docs.npmjs.com
- **Express.js Docs:** https://expressjs.com
- **MDN JavaScript:** https://developer.mozilla.org/en-US/docs/Web/JavaScript

## Best YouTube Channels

- **Traversy Media** — Practical Node.js tutorials
- **The Net Ninja** — Full Node.js series (beginner to advanced)
- **Fireship** — Quick concept videos (10 minutes)
- **Academind** — Deep dives with Maximilian Schwarzmüller
- **Hussein Nasser** — Backend engineering, Node.js internals
- **Jack Herrington** — Advanced patterns

## GitHub Repositories

- **nodejs/node** — Official Node.js source
- **goldbergyoni/nodebestpractices** — ⭐ Top Node.js best practices list
- **sindresorhus/awesome-nodejs** — Curated packages list
- **expressjs/express** — Express source code
- **nicedoc/awesome-node** — More resources

## Practice Platforms

- **LeetCode** — https://leetcode.com (algorithms + DS)
- **HackerRank** — https://hackerrank.com/domains/nodejs
- **CodeWars** — https://www.codewars.com (kata challenges)
- **Exercism** — https://exercism.org/tracks/javascript
- **NodeSchool** — https://nodeschool.io (Node-specific workshops)
- **Backend Challenges** — https://roadmap.sh/backend/project-ideas

## Courses

- **Node.js — The Complete Guide** (Udemy, Maximilian Schwarzmüller)
- **The Complete Node.js Developer Course** (Udemy, Andrew Mead)
- **Node.js and Express.js – Full Course** (freeCodeCamp, YouTube — free)

## Books

- **Node.js Design Patterns** (Mario Casciaro) — Advanced
- **Learning Node** (Shelley Powers) — Beginner/Intermediate
- **Node.js in Action** (Manning Publications) — Comprehensive