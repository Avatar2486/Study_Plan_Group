# Node.js

---

## 🔰 **1. Node.js Foundations (Absolute Core)**

### 🧱 Building Blocks

- What is Node.js? V8 engine, libuv, event-driven architecture
- Node.js vs Browser JavaScript (window, DOM, process, fs)
- REPL, running scripts (`node app.js`), shebang lines
- `process` object (`argv`, `env`, `cwd`, `exit`, `pid`, `version`)
- `console` methods (`log`, `error`, `warn`, `time`, `table`, `dir`)
- Global objects (`__dirname`, `__filename`, `global`, `Buffer`, `setTimeout`)
- Variables: `var`, `let`, `const` — scoping, hoisting, TDZ
- Data Types: primitives vs reference types, type coercion
- Numbers, Strings, Booleans, `null`, `undefined`, `Symbol`, `BigInt`
- Template literals, tagged templates
- Comments & JSDoc

### 🔁 Control Flow

- `if`, `else if`, `else`, ternary (`? :`)
- `switch` statements
- `for`, `while`, `do...while`
- `for...of` (values), `for...in` (keys)
- `break`, `continue`, labeled statements
- Short-circuit evaluation (`&&`, `||`, `??`)
- Optional chaining (`?.`)

### 📦 Core Data Structures

- **Arrays** — methods: `map`, `filter`, `reduce`, `find`, `some`, `every`, `flat`, `flatMap`
- **Objects** — creation, access, `Object.keys/values/entries/assign/freeze/create`
- **Maps** — ordered key-value, any key type, size property
- **Sets** — unique values, set operations, `WeakSet`
- **WeakMap / WeakRef** — GC-friendly references, use cases
- Spread (`...`) and Rest patterns
- Destructuring (array + object, nested, defaults, renaming)

### 🔄 Iteration System

- **Iterables vs Iterators** — `Symbol.iterator` protocol
- `__iter__` equivalent: `[Symbol.iterator]()` + `{ value, done }`
- **Custom iterators** — manual `next()` implementation
- **Generator functions** (`function*`, `yield`, `yield*`)
- Generator lifecycle: suspended, running, completed
- `for...of` with custom iterables
- Built-in iterables: Arrays, Maps, Sets, Strings, NodeLists
- Iterator helpers: `Array.from`, spread on iterables

### ⚙️ Functions

- Function declarations vs expressions vs arrow functions
- Parameters, defaults, rest (`...args`)
- Return values, implicit returns in arrow functions
- `this` keyword — context rules in regular vs arrow functions
- `call`, `apply`, `bind`
- Scope: lexical scope, scope chain
- **Closures** — data privacy, factory functions, memoization
- Lambda / arrow function nuances (no `this`, `arguments`)
- First-class functions, higher-order functions
- **Function decorators** (manual HOF pattern + TC39 Decorator proposal)
- Recursion, tail call optimization awareness
- IIFEs (Immediately Invoked Function Expressions)
- `arguments` object vs rest params

### 🌀 **Generators & Iterators (Key Skill)**

- `function*` syntax, `yield`, `yield*` delegation
- Generator object lifecycle (suspended → running → completed)
- Passing values into generators via `next(value)`
- Generator expressions (none in JS — use generator functions)
- Lazy evaluation benefits
- Use cases: infinite sequences, async iteration, pipelines
- **Async generators** (`async function*`, `for await...of`)
- `Symbol.asyncIterator` protocol
- Streaming large data with async generators

---

## 🧰 **2. Object-Oriented Programming (OOP)**

- Classes & Objects — ES6 class syntax, `new` keyword
- Constructors (`constructor()`)
- Instance vs Class (static) properties and methods
- **Private fields** (`#field`) and private methods — true encapsulation
- **Getters & Setters** (`get`/`set` keywords)
- **Inheritance** — `extends`, `super()`, `super.method()`
- Prototype chain — `__proto__`, `Object.getPrototypeOf`, `prototype`
- Class vs Prototype-based understanding (under the hood)
- **Method Resolution Order** — prototype chain traversal
- **Polymorphism** — method overriding, duck typing
- **Encapsulation** — private fields, closures for privacy
- **Abstraction** — abstract base class pattern, `new.target`
- **Operator overloading** — `Symbol.toPrimitive`, `valueOf`, `toString`
- `instanceof`, `typeof`, `Object.prototype.toString.call`
- **Mixins** — composing behaviors without inheritance
- **Composition vs Inheritance** — prefer composition
- `Object.create()` — prototypal inheritance directly
- Symbols as unique property keys
- Proxy & Reflect — meta-programming, traps
- **Dataclass equivalent** — plain classes + validation, or libs like `class-validator`

---

## 📦 **3. Modules & Package Ecosystem**

- **CommonJS** — `require()`, `module.exports`, `exports`, caching behavior
- **ES Modules (ESM)** — `import`/`export`, static analysis, tree shaking
- Named vs default exports, re-exports (`export { x } from`)
- `import()` — dynamic imports (lazy loading)
- `node:` prefix for built-in modules (Node 16+)
- CJS vs ESM interop — `.mjs`, `"type": "module"` in package.json
- **`__dirname` / `__filename`** in CJS vs `import.meta.url` in ESM
- `package.json` — fields: `main`, `exports`, `type`, `scripts`, `engines`
- **Semantic Versioning** — `^`, `~`, exact, ranges
- **npm** — install, update, audit, workspaces
- **npx** — run without installing globally
- **pnpm / yarn** — alternatives, monorepo support
- **Virtual environments equivalent** — `node_modules`, `.npmrc`, `nvm`, `volta`
- Lock files — `package-lock.json`, `yarn.lock` — reproducible installs
- Publishing packages to npm registry
- **Monorepos** — npm workspaces, Turborepo
- Environment variable management — `dotenv`, `dotenv-expand`
- Configuration management — `config`, `convict`, `zod`-based config validation

---

## 🧪 **4. Testing & Code Quality**

- **Jest** — unit tests, describe/it/expect, matchers
- **Vitest** — faster Jest alternative (ESM-native)
- **Mocha + Chai** — classic combination
- **Supertest** — HTTP integration testing for Express/Fastify
- **Fixtures & factories** — test data setup
- **Mocking** — `jest.fn()`, `jest.mock()`, `jest.spyOn()`
- **Module mocking** — manual mocks in `__mocks__`
- **Snapshot testing** — UI output, JSON structures
- **Parametrized tests** — `test.each`
- **Code coverage** — `--coverage`, Istanbul/c8
- **TDD workflow** — Red → Green → Refactor
- **E2E testing** — Playwright, Cypress (for full-stack)
- **Linting** — ESLint, rules, plugins, flat config
- **Formatting** — Prettier, EditorConfig
- **Type checking** — TypeScript, JSDoc type annotations
- **Husky + lint-staged** — pre-commit hooks
- **Secure coding** — `npm audit`, Snyk, input sanitization
- **Dependency injection** for testability

---

## ⚙️ **5. Async Programming & Concurrency (Correct & Complete)**

### 🌀 Event Loop Mechanics

- Call stack, heap, callback queue, microtask queue
- **Event loop phases** — timers → pending I/O → idle → poll → check → close
- `process.nextTick()` — before any I/O, before Promises
- Microtask queue — Promises, `queueMicrotask`
- Macrotask queue — `setTimeout`, `setInterval`, `setImmediate`, I/O
- `setImmediate` vs `setTimeout(fn, 0)` — phase difference
- Starving the event loop — how to avoid

### 🔁 Callbacks & Promises

- Callback pattern — error-first convention `(err, data) =>`
- Callback hell — pyramid of doom
- **Promises** — states (pending/fulfilled/rejected), chaining
- `.then()`, `.catch()`, `.finally()`
- **Promise combinators**:
    - `Promise.all` — all or fail
    - `Promise.allSettled` — all statuses
    - `Promise.race` — first settles (either)
    - `Promise.any` — first success
- `util.promisify` — convert callback APIs to Promises

### 🌪 Async/Await (Deep)

- `async` function — always returns Promise
- `await` — suspension without blocking event loop
- `try/catch/finally` for async error handling
- Sequential vs parallel execution patterns
- `for await...of` — async iteration
- **Top-level `await`** (ESM only)
- `AsyncLocalStorage` — request-scoped context, tracing
- Avoiding common mistakes: `forEach` + async, unhandled rejections

### 🧵 Worker Threads (CPU-bound tasks)

- `worker_threads` module — true parallelism in Node.js
- `isMainThread`, `parentPort`, `workerData`
- `SharedArrayBuffer` + `Atomics` — shared memory
- Worker pools — reusing workers efficiently
- Use cases: image processing, crypto, heavy computation

### 🏗 Cluster Module (Multi-process scaling)

- `cluster.fork()` — one process per CPU core
- Primary/worker architecture
- Shared port listening
- Worker lifecycle — exit, restart, IPC
- PM2 as production cluster manager

### 🔗 Child Processes

- `spawn` — streaming, large output
- `exec` — buffered output, shell commands
- `execFile` — direct binary execution
- `fork` — Node.js child with IPC channel
- Communication via IPC (`send`, `message`)

---

## 🌐 **6. File I/O, Databases & Networking**

### File System

- `fs` module — sync vs async vs promise APIs
- Read, write, append, delete, rename, copy
- Directory operations — `mkdir`, `readdir`, `rmdir`
- File stats — `stat`, `lstat`, `access`, `exists` alternative
- **Watchers** — `fs.watch`, `fs.watchFile`, chokidar
- Path module — `join`, `resolve`, `basename`, `extname`, `dirname`, `relative`
- **Context manager equivalent** — `try/finally` or `using` (TC39 Resource Management)

### Streams (Deep)

- **Readable, Writable, Duplex, Transform** streams
- **Backpressure** — when to pause/resume, `highWaterMark`
- `.pipe()` — automatic backpressure handling
- `pipeline()` from `stream/promises` — error-safe piping
- Stream events: `data`, `end`, `error`, `drain`, `finish`
- **Object mode** streams
- Creating custom Transform streams
- `readline` — line-by-line file processing
- Streaming with HTTP (response piping, file download)

### Data Formats

- JSON — `parse`, `stringify`, replacers, revivers, circular reference handling
- CSV — `csv-parse`, `fast-csv`
- YAML — `js-yaml`
- XML — `xml2js`, `fast-xml-parser`
- Binary — `Buffer`, `TypedArray`, `DataView`

### Databases

- **SQLite** — `better-sqlite3`, `sqlite3`
- **PostgreSQL** — `pg`, connection pooling
- **MySQL** — `mysql2`
- **MongoDB** — `mongoose`, schemas, virtuals, middleware
- **Redis** — `ioredis`, caching, pub/sub, sessions, rate limiting
- **ORMs** — Prisma (type-safe), Sequelize, TypeORM, Drizzle
- Query builders — Knex.js
- Database migrations and seeding
- Connection pooling — `pg-pool`, Prisma connection limit
- Transactions — ACID, rollback patterns

### Networking & HTTP

- `http` / `https` modules — low-level server
- Making HTTP requests — `fetch` (native Node 18+), `axios`, `got`, `node-fetch`
- **WebSockets** — `ws` library, `socket.io`
- **Server-Sent Events (SSE)** — one-way real-time streaming
- DNS module — `dns.resolve`, `dns.lookup`
- **gRPC** — `@grpc/grpc-js`, protobuf, streaming RPCs
- Sockets — `net` module, TCP/UDP
- TLS/SSL — `tls` module, certificate handling

---

## 🚀 **7. Web Frameworks (Sync + Async)**

### Express.js (Most widely used)

- Setup, routing, middleware pipeline
- Route params, query strings, request body parsing
- `express.Router()` — modular routing
- Error handling middleware (4-param signature)
- Static file serving
- Template engines — EJS, Handlebars, Pug
- **Middleware ecosystem** — helmet, cors, morgan, compression

### Fastify (High-performance)

- Schema-based validation (JSON Schema / Zod)
- Plugin system — `fastify-plugin`, encapsulation
- Hooks — `onRequest`, `preHandler`, `onSend`, `onError`
- Decorators — extending request/reply
- Built-in Swagger/OpenAPI generation
- Async-first route handlers

### NestJS (Enterprise / Angular-inspired)

- Modules, Controllers, Providers (DI container)
- Guards, Interceptors, Pipes, Filters — AOP patterns
- TypeScript-first
- Microservices support built-in

### Common Patterns Across Frameworks

- **Middleware** — logging, auth, rate limiting, parsing
- **Background tasks** — `bull`, `bullmq`, `node-cron`
- **Auth / JWT** — `jsonwebtoken`, `passport`, refresh tokens
- **Rate limiting** — `express-rate-limit`, Redis-backed
- **Streaming responses** — SSE, chunked transfer
- **API versioning** — URL prefix, header-based
- **OpenAPI / Swagger** — `swagger-ui-express`, `@nestjs/swagger`
- **Validation** — `joi`, `zod`, `class-validator`
- **Request ID & correlation** — `AsyncLocalStorage` + UUID
- **CORS handling** — `cors` package, preflight
- **Content negotiation** — JSON, MessagePack, custom

---

## 📡 **8. Distributed Systems & Messaging**

- REST vs RPC design philosophy
- **gRPC** — protocol buffers, streaming (unary/server/client/bidirectional)
- **REST best practices** — idempotency, HATEOAS, pagination
- **GraphQL** — `apollo-server`, `mercurius`, DataLoader for N+1
- **Message Queues** — RabbitMQ (`amqplib`), Bull/BullMQ (Redis-backed)
- **Kafka** — `kafkajs` — producers, consumers, consumer groups, partitions
- **Redis Streams** — lightweight alternative to Kafka
- **Pub/Sub** — Redis `publish/subscribe`, EventEmitter pattern
- **Async event consumers** — idempotent message handling
- **Retries & exponential backoff** — `p-retry`, custom retry logic
- **Dead letter queues (DLQ)** — handling failed messages
- **Circuit breakers** — `opossum` library
- **Service discovery** — Consul, environment-based
- **Health checks** — `/health`, `/ready`, `/live` endpoints
- **Distributed tracing** — OpenTelemetry, Jaeger, Zipkin
- **Connection pooling** — DB pools, HTTP agent keep-alive
- **Idempotency keys** — safe retries on POST requests

---

## 🤖 **9. Performance, Memory & Internals**

### Profiling & Measurement

- `console.time` / `console.timeEnd`
- `performance.now()` — high-resolution timing
- `--prof` flag — V8 profiler output
- `clinic.js` — flamegraphs, bubbleprof, heapprofiler
- `0x` — flamegraph profiler
- `node --inspect` + Chrome DevTools — CPU profiling
- `autocannon`, `k6`, `wrk` — HTTP load testing

### Memory Management

- V8 heap — new space (young gen), old space (old gen)
- Garbage collection — mark-and-sweep, generational GC
- `process.memoryUsage()` — `heapUsed`, `heapTotal`, `rss`, `external`
- **Memory leaks** — event listener accumulation, closures, global references
- Heap snapshots — Chrome DevTools, `heapdump`
- **`--max-old-space-size`** — increase heap for large workloads
- **`__slots__` equivalent** — lean objects, avoid dynamic properties
- `Buffer.allocUnsafe` vs `Buffer.alloc` — performance tradeoffs
- `WeakMap`/`WeakRef`/`FinalizationRegistry` — GC-safe references

### V8 Internals Awareness

- **Hidden classes** — keeping object shapes consistent for JIT optimization
- **Inline caching** — V8 optimizes repeated same-shape calls
- **Deoptimization** — avoid mixing types in hot functions
- `v8.getHeapStatistics()` — programmatic heap info
- `--trace-gc`, `--trace-opt`, `--trace-deopt` flags
- **Bytecode inspection** — `node --print-bytecode`

### Optimization Patterns

- Avoid synchronous I/O in server hot paths
- Stream large payloads instead of buffering
- Object pooling — reuse expensive objects
- Batch DB/API calls — avoid N+1 patterns
- Response compression — `zlib`, `compression` middleware
- HTTP/2 — multiplexing, server push
- `keep-alive` connections — reduce TCP overhead
- CPU-bound → Worker Threads; I/O-bound → async/await

---

## 🧠 **10. Functional & Advanced Paradigms**

- **Pure functions** — no side effects, deterministic
- **Immutability** — `Object.freeze`, spread patterns, `immer`
- **Currying** — manual + `lodash/fp.curry`
- **Partial application** — `Function.prototype.bind`, custom `partial`
- **Function composition** — `pipe`, `compose` (right-to-left)
- **Map / Filter / Reduce** — declarative data transformations
- **Comprehension equivalent** — chained array methods, generator expressions
- **`itertools` equivalent** — `iter-tools` library, manual generators
- **`functools` equivalent** — `lodash`, `ramda`, `remeda`
- **Lazy evaluation** — generators, `Proxy`-based lazy props
- **Transducers** — composable reducing functions
- **Monads awareness** — Option/Maybe with `folktale`, `fp-ts`
- **Point-free style** — compose without naming arguments
- **Algebraic Data Types (ADT)** — discriminated unions in TypeScript

---

## 🔒 **11. Security**

- **OWASP Top 10** awareness for Node.js
- **Input validation** — `zod`, `joi`, `express-validator`; never trust user input
- **SQL injection** — always parameterized queries; never string concatenation
- **NoSQL injection** — MongoDB operator injection (`$where`, `$regex`)
- **XSS** — sanitize HTML output, `DOMPurify`, Content-Security-Policy header
- **CSRF** — `csurf`, SameSite cookies, double-submit tokens
- **Helmet.js** — security headers (CSP, HSTS, X-Frame-Options)
- **Authentication** — JWT (`jsonwebtoken`), session-based, OAuth2/OIDC
- **JWT best practices** — short expiry, refresh tokens, `RS256` over `HS256`
- **Password hashing** — `bcrypt`, `argon2`; never store plain or MD5
- **Rate limiting** — `express-rate-limit`, Redis-backed distributed limiting
- **HTTPS / TLS** — certificate management, `Let's Encrypt`, HTTP → HTTPS redirect
- **`npm audit`** — dependency vulnerability scanning
- **Secrets management** — never hardcode; use `dotenv`, AWS Secrets Manager, Vault
- **Prototype pollution** — sanitize merge/assign with user data, `Object.create(null)`
- **Path traversal** — validate and sanitize file paths (`path.resolve` + prefix check)
- **`child_process`** safety — avoid `exec` with user input; prefer `execFile`/`spawn`
- **Dependency supply chain** — pin versions, use Snyk, audit regularly

---

## 🎁 **12. CLI, Packaging & Deployment**

### CLI Tools

- `process.argv` — raw argument parsing
- `commander` / `yargs` — full CLI framework
- `inquirer` / `@clack/prompts` — interactive prompts
- `chalk` / `picocolors` — terminal colors
- `ora` — spinners and progress
- Shebang lines (`#!/usr/bin/env node`), `bin` field in package.json

### Packaging & Publishing

- `package.json` — `exports` map, dual CJS+ESM packages
- Build tools — `tsup`, `esbuild`, `rollup`, `ncc` (single-file bundle)
- **TypeScript** — `tsc`, `tsconfig.json`, declaration files (`.d.ts`)
- Publishing to npm — `npm publish`, scoped packages, tags (`latest`, `beta`)
- Semantic versioning — `standard-version`, `release-it`, `changesets`

### Deployment & Infrastructure

- **Docker** — `Dockerfile` for Node.js, multi-stage builds, `.dockerignore`
- **Docker Compose** — local multi-service setup
- **PM2** — process manager, clustering, log management, `ecosystem.config.js`
- **Graceful shutdown** — `SIGTERM` handler, drain in-flight requests, close DB
- **Health checks** — `/healthz`, `/readyz`, `/livez` endpoints
- **Environment parity** — dev/staging/prod config via env vars
- **CI/CD** — GitHub Actions, GitLab CI — lint → test → build → deploy pipeline
- **Kubernetes basics** — Deployment, Service, ConfigMap, liveness/readiness probes
- **Serverless** — AWS Lambda (Node runtime), Vercel, Netlify Functions
- **Reverse proxy** — Nginx config for Node.js apps
- **Logging** — `pino` (structured JSON), `winston`, log levels, log aggregation (ELK, Datadog)
- **Monitoring & APM** — Prometheus + Grafana, Datadog, New Relic, OpenTelemetry

---

## 🧩 **13. Design Patterns (Node.js Specific)**

- **Singleton** — module-level export, class-based
- **Factory** — `createX()` functions, class factories
- **Builder** — fluent interface, method chaining
- **Observer / EventEmitter** — `events` module, custom pub/sub
- **Middleware / Chain of Responsibility** — Express/Koa pipeline
- **Strategy** — swap algorithm implementations
- **Proxy** — ES6 `Proxy` for validation, logging, lazy loading
- **Repository pattern** — abstract data access layer
- **Service Layer** — separate business logic from controllers
- **Dependency Injection** — manual, InversifyJS, NestJS DI
- **Module pattern** — encapsulation via closures (pre-class)
- **Plugin pattern** — Fastify/Hapi plugin registration
- **CQRS** — separate read/write models
- **Event Sourcing** — store events, derive state

---

## 🧪 **14. TypeScript with Node.js (Essential)**

- Why TypeScript — safety, IDE support, refactoring confidence
- `tsconfig.json` — `target`, `module`, `strict`, `paths`, `outDir`
- **Types vs Interfaces** — when to use each
- **Generics** — reusable typed functions and classes
- **Utility types** — `Partial`, `Required`, `Pick`, `Omit`, `Readonly`, `Record`, `ReturnType`
- **Discriminated unions** — type-safe state machines
- **Type guards** — `typeof`, `instanceof`, custom predicates (`is`)
- **Declaration merging** — extending third-party types
- **Decorators** — experimental, NestJS usage
- **`zod`** — runtime validation + TypeScript type inference
- **`ts-node`**, `tsx`, `ts-node-esm` — running TS directly
- Path aliases — `@/` imports with `tsconfig` + `tsconfig-paths`
- **Strict null checks** — eliminating `undefined` bugs

---

## 🎓 **15. Capstone Projects (Production-Level Ideas)**

- **Async REST API with full stack** — Express/Fastify + Prisma + PostgreSQL + Redis caching + JWT auth + rate limiting + Swagger docs + Docker
- **Real-time Collaboration Tool** — WebSocket + Redis pub/sub + operational transforms + cluster scaling
- **Kafka Microservices** — Producer/Consumer services + dead letter queue + distributed tracing with OpenTelemetry
- **Build a Task Scheduler (mini-Airflow)** — BullMQ + cron expressions + job dependencies + web dashboard
- **Custom ORM** — using Proxy + descriptors + query builder pattern
- **Distributed Rate Limiter** — Redis sliding window + Lua scripts + multi-node sync
- **Build a coroutine-style async crawler** — async generators + backpressure + politeness delay + robots.txt
- **CLI DevTool** — commander + inquirer + fs operations + npm publish pipeline
- **GraphQL API** — Apollo Server + DataLoader (N+1 fix) + subscriptions + persisted queries
- **Serverless Microservice** — AWS Lambda + API Gateway + DynamoDB + CDK IaC

---


Access The AI genrated Topics Here : [[Node JS AI]]