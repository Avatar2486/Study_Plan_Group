# Python

---

## 🔰 **1. Python Foundations (Absolute Core)**

### 🧱 Building Blocks

- Hello Python, REPL, scripts
- Variables & Types
- Numbers (int, float, decimal, fractions)
- Strings
- Input / Print / f-strings
- Comments & Docstrings
- Booleans & Comparisons
- Operators (Arithmetic, Logical, Bitwise)

### 🔁 Control Flow

- `if`, `elif`, `else`
- `for` & `while` loops
- `break`, `continue`, `pass`
- Ternary expressions

### 📦 Core Data Structures

- **Lists**
- **Tuples (immutability, packing/unpacking)**
- **Sets** (dedupe, membership, set ops)
- **Dictionaries** (key/value store, iteration)

### 🔄 Iteration System

- **Iterables vs Iterators**
- `__iter__`, `__next__`
- **Custom iterators**
- Built-in iterator helpers (`enumerate`, `zip`, `map`, `filter`, `sorted`, `all`, `any`)

### ⚙️ Functions

- Defining functions
- Parameters, arguments, defaults
- Return values
- Mutable vs Immutable argument pitfalls
- Variable arguments (`args`, `*kwargs`)
- Scope & `global`, `nonlocal`
- Lambda functions
- Recursion basics
- First-class + Higher-order functions
- Function decorators (syntax + execution order)

### 🌀 **Generators (Key Skill)**

- `yield` + generator function lifecycle
- Generator expressions `(x for x in ...)`
- Lazy evaluation benefits
- Use cases: streaming, pipelines, large data processing
- `yield from` delegation

---

## 🧰 **2. Object-Oriented Programming (OOP)**

- Classes & Objects
- Methods & attributes
- Encapsulation
- Constructors (`__init__`)
- Class vs Instance variables
- Classmethods & Staticmethods
- Inheritance & Multiple inheritance
- Method resolution order (MRO)
- Polymorphism
- Operator overloading (`__add__`, `__str__`, etc.)
- Abstract base classes
- Interfaces via Protocols
- Dataclasses (auto-init, slots)
- Properties & descriptors
- Composition vs inheritance
- Metaclasses (awareness)

---

## 📦 **3. Python Modules & Best Practices**

- Modules & `import`
- Packages & `__init__.py`
- Virtual environments (`venv`, `pipenv`, `poetry`)
- Managing dependencies
- Project structures
- Logging
- Configuration management (`dotenv`, configparser)

---

## 🧪 **4. Testing & Quality**

- `unittest`
- `pytest`
- Fixtures
- Mocking & patching
- Parametrized tests
- Code coverage
- TDD workflow
- Linting: flake8, black, mypy
- Pre-commit hooks
- Secure coding practices

---

## ⚙️ **5. Concurrency & Parallelism (Correct & Complete)**

### 🌪 Threads

- GIL explained
- Thread safety
- Thread pools (`ThreadPoolExecutor`)

### 🧩 Multiprocessing

- Bypassing GIL
- Shared memory vs message passing
- `ProcessPoolExecutor`

### 🌀 **AsyncIO & Coroutines (Deep)**

- What is a coroutine? (`async def`)
- `await`, suspension points
- Event loop mechanics
- Scheduling coroutines
- Tasks (`create_task`, `gather`)
- Async iterators `async for`
- Async generators `async yield`
- Queues & semaphores
- Task cancellations
- Avoiding blocking IO in async
- Coroutines vs threads vs processes
- Combining async + threads safely
- Debugging coroutines & leaks

---

## 🌐 **6. File IO, Databases & Networking**

- Open/read/write files
- With-context (`context manager`, `__enter__`, `__exit__`)
- CSV, JSON, YAML, XML
- SQLite
- ORM (SQLAlchemy, Tortoise)
- HTTP requests (`requests`, `aiohttp`)
- Sockets (sync & async)
- Cloud storage APIs
- Caching (redis)

---

## 🚀 **7. Web Frameworks (Sync + Async)**

- Flask
- Django
- **FastAPI (async-first)**
- Middlewares
- Background tasks
- Auth/JWT
- Rate limiting
- Async streaming responses
- API versioning
- API contracts + OpenAPI schemas

---

## 📡 **8. Distributed Systems & Messaging**

- REST vs RPC
- gRPC (sync + async stubs)
- Kafka/RabbitMQ/Redis streams
- Async event consumers
- Idempotent message handling
- Retries & exponential backoff
- Connection pooling
- Circuit breakers
- Task queues (Celery/RQ/Arq)

---

## 🤖 **9. Performance, Memory & Internals**

- Profilers (cProfile, py-spy)
- Time complexity (Big-O for Python DS)
- Memory optimizations (`sys.getsizeof`, slots)
- Iterators for memory savings
- GIL impact + bypass strategies
- CPython bytecode
- Bytecode inspection (`dis`)
- Garbage collection
- `__slots__` vs dict instance
- C extensions (Cython, PyPy, Rust FFI)

---

## 🧠 **10. Functional & Advanced Paradigms**

- Pure functions
- Immutability
- Currying, partials
- Map/Filter/Reduce
- Comprehensions
- Itertools
- Functools
- Lazy evaluation
- Monads (light exposure)

---

## 🎁 **11. Packaging, CLI & Deployment**

- CLI tools (`argparse`, Typer)
- Publish package to PyPI
- Versioning (semver)
- Build wheels
- Dockerizing Python apps
- CI/CD
- Unit vs integration vs E2E tests
- Virtualenv management in prod
- gunicorn

---

## 🎓 **13. Capstones (Project Ideas)**

- Async web scraper with backpressure
- Kafka microservice with FastAPI
- Build a task scheduler (mini-Airflow)
- Create your own iterator library
- Custom ORM using descriptors + metaclasses
- Distributed rate limiter
- Build a coroutine-based crawler

---