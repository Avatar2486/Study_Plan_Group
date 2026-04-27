# Go

---

# 🟩 **1. Go Language Fundamentals**

### **Core Topics**

✅ What is Go? Why created (simplicity, concurrency, cloud)

✅ Installing Go & `GOROOT`, `GOPATH`

✅ Variables, constants, `:=`

✅ Data types: string, int, float, bool

✅ Arrays vs Slices

✅ Maps

✅ Control Flow (`if`, `for`, `switch`)

✅ Functions & multiple return values

✅ Importing packages

✅ Error handling basics (no exceptions)

✅ **defer** — delayed execution at function exit

✅ **panic & recover** — controlled failure handling

✅ Time handling: `time.Now`, parsing, formatting

### **Practice Questions**

1️⃣ Why does Go return errors instead of throwing exceptions?

2️⃣ What does `:=` do differently than `var`?

3️⃣ Why does Go require unused variables removed?

4️⃣ When should you use `panic` vs return error?

5️⃣ How does `defer` unwind execution?

### **Hands-On**

✔ Build a calculator CLI

✔ Store users in slice + modify

✔ Use defer + panic/recover safely

---

# 🟨 **2. Data Structures, Functions & Composition**

### **Core Topics**

✅ Structs & methods

✅ Struct embedding (composition > inheritance)

✅ Interfaces & duck typing

✅ Generics (Go 1.18+)

✅ Passing values vs pointers

✅ Packages, modules, `go mod init`

✅ Config handling (env vars, config structs)

✅ Expanded `defer` examples in methods

### **Practice Questions**

1️⃣ Why composition > inheritance?

2️⃣ What is duck typing in Go?

3️⃣ When to use pointer receivers vs value receivers?

4️⃣ What problem do generics solve?

5️⃣ Best way to load config cleanly?

### **Hands-On**

✔ Create a struct + methods

✔ Implement interface without `implements`

✔ Write generic sum function

✔ Organize project into `/cmd`, `/pkg`, `/internal`

✔ Load config from env

---

# 🟥 **3. Concurrency (Go’s Superpower)**

### **Core Topics**

✅ Goroutines — lightweight execution units

✅ **Goroutine lifecycle** (start, run, exit)

✅ **Goroutine leaks** — causes & prevention

- Blocked read/write
- Forgotten receivers
- Missing cancellation
- Detect leaks via tooling

✅ Channels (buffered/unbuffered)

✅ **Channel closing semantics**

- Only sender closes
- Detect closed channels (`v, ok`)
- `for range` on closed channels
- Avoid sending on closed channel

✅ Synchronization: WaitGroup, Mutex, Atomic

✅ **Bounded concurrency**

- worker pool
- semaphore pattern (buffered channel)
- pipeline fan-in/fan-out

✅ **Backpressure**

- buffer sizing
- pushback via blocking
- dropping tasks vs queuing
- propagate backpressure with context

✅ Select statement

✅ Context cancellation + deadlines

- context.WithTimeout
- context.WithCancel
- context propagation

✅ Error groups pattern

- `errgroup.Group`
- cancel all children on first error
- avoid leaks

### **Practice Questions**

1️⃣ Concurrency vs parallelism?

2️⃣ When to choose channels vs mutex?

3️⃣ How do goroutine leaks happen?

4️⃣ Why must only the sender close channels?

5️⃣ Race condition detection (`-race`)?

6️⃣ Why bounded concurrency matters?

7️⃣ How does Go’s G-M-P scheduler work?

### **Hands-On**

✔ Build worker pool with bounded concurrency

✔ Scrape 100 URLs concurrently + backpressure

✔ Timeout slow ops with context

✔ Detect races using `go run -race`

---

# 📦 **4. File I/O, JSON, Testing & Tooling**

### **Core Topics**

✅ Read/write files

✅ JSON encode/decode

✅ `os`, `io`, `bufio`, `encoding/json`

✅ Unit tests & table-driven tests

✅ Mocks & interfaces

✅ Benchmark tests

✅ `go vet`, `golangci-lint`, static analysis

✅ Logging basics (`log`, `fmt`)

✅ Module versioning

✅ Time parsing + formatting

### **Practice Questions**

1️⃣ How parse JSON into struct?

2️⃣ What is table-driven testing?

3️⃣ What do `go vet` and `golangci-lint` catch?

4️⃣ How to structure testable code?

5️⃣ When use `strings.Builder` vs `+`?

### **Hands-On**

✔ Write unit tests for calculator

✔ Benchmark concatenation

✔ Build config loader from JSON

---

# ⚙️ **5. Building Web Apps With `net/http`**

### **Core Topics**

✅ `net/http` basics

✅ Handlers & routing

✅ Middleware concept

✅ Query params & headers

✅ HTTP status codes

✅ Graceful shutdown

- `http.Server` with timeouts
- listen for `SIGTERM`
- cancel ongoing work

✅ Request lifecycle

- Context expiry
- Client disconnect handling

### Practice Qs

1️⃣ How does Go handle HTTP without frameworks?

2️⃣ What is handler chaining?

3️⃣ How to use context for shutdown?

### Hands-On

✔ Build REST API

✔ Implement custom logger middleware

✔ Add graceful shutdown

---

# 🚀 **6. Gin Framework (High Velocity Backend)**

### **Core Topics**

✅ Routing, groups, params

✅ JSON binding & validation

✅ Cookie + token auth

✅ CORS

✅ Static files

✅ Env configs

✅ **Gin context lifecycle**

✔ Valid only during request

✔ Copy context for async goroutines

✔ Don’t store Gin context globally

✅ **Error handling patterns**

✔ `c.Error`, error aggregator

✔ Central error middleware

✔ Unified API responses

✅ **Middleware execution flow**

✔ Pre-handler

✔ `c.Next()`

✔ Post-handler

✔ Abort chain

✅ **Background work**

✔ Use `go func()` safely

✔ Use `ctx.Copy()`

✔ Cancel goroutines when client disconnects

✔ Avoid leaks

### Practice Qs

1️⃣ How do Gin middlewares work?

2️⃣ How does JSON binding validate automatically?

3️⃣ Path vs query params?

4️⃣ Why copy context for background work?

### Hands-On

✔ Build Users CRUD

✔ Add request logging middleware

✔ Validate payloads

✔ Run background tasks with cancellation

---

# 🗄 **7. Database Layer & Production APIs**

### **Core Topics**

Postgres/MySQL

sql.DB

Pooling

ORM vs raw SQL

Migrations

Repo/service layer

JWT auth

Password hashing

Pagination/filtering

### Practice Qs

DB pooling?

ORM pros/cons?

JWT security?

N+1 problems?

---

# 🔥 **8. Cloud, Scaling & Observability**

### **Core Topics**

Dependency injection

zerolog/zap

Prometheus + Grafana

Tracing with OpenTelemetry

Redis cache

Rate limiting

Backpressure at API edge

Vault/secrets

Graceful degradation

---

# 🌍 **9. Microservices & Messaging**

### **Core Topics**

REST vs gRPC

Protobuf

Kafka/NATS/RabbitMQ

Idempotency

Circuit breakers

Saga patterns

Context propagation across services

Testing distributed systems

---

# 👑 **10. Expert + Go Internals**

### **Core Topics**

GC phases

Escape analysis

G-M-P scheduling internals

Memory fragmentation & stack growth

Unsafe & reflect

Build tags

Cross-compilation

Reusable librariess

---