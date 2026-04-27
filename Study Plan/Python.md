# 🐍 Python — Complete Extended

# 🚧 Main Topics Only Acess [[Python Main Topics]]

## 🔰 1. Python Foundations (Absolute Core)

### 🧱 1.1 Building Blocks

- [ ] Hello Python — running scripts vs REPL (`python3 script.py` vs `python3`)
- [ ] Variables & naming rules (snake_case, reserved words)
- [ ] Types overview — dynamic typing, `type()`, `isinstance()`
- [ ] **Numbers**
    - `int`, `float`, `complex`
    - `decimal.Decimal` for precision
    - `fractions.Fraction`
    - Integer division `//`, modulo `%`, power `**`
- [ ] **Strings**
    - Single, double, triple quotes
    - Indexing & slicing `s[1:5:2]`
    - Common methods: `.strip()`, `.split()`, `.join()`, `.replace()`, `.find()`, `.startswith()`
    - String immutability
    - `str.encode()` / `bytes.decode()` — encoding basics
- [ ] **f-strings** — `f"{name!r}"`, expressions, formatting specs `f"{value:.2f}"`
- [ ] `input()` / `print()` — `sep`, `end`, `file` params
- [ ] Comments `#` and **Docstrings** (`"""..."""`, Google/NumPy style)
- [ ] **Booleans** — `True`, `False`, truthiness & falsy values (`0`, `""`, `[]`, `None`)
- [ ] **Operators**
    - Arithmetic: `+`, `-`, `*`, `/`, `//`, `%`, `**`
    - Comparison: `==`, `!=`, `<`, `>`, `<=`, `>=`
    - Logical: `and`, `or`, `not`
    - Bitwise: `&`, `|`, `^`, `~`, `<<`, `>>`
    - Assignment: `=`, `+=`, `-=`, `*=`, etc.
    - Identity: `is`, `is not`
    - Membership: `in`, `not in`
- [ ] Operator precedence & associativity

---

### 🔁 1.2 Control Flow

- [ ] `if`, `elif`, `else` — nesting, chaining
- [ ] `for` loops — iterating lists, strings, ranges
- [ ] `while` loops — condition-based iteration
- [ ] `range(start, stop, step)`
- [ ] `break` — exit loop early
- [ ] `continue` — skip to next iteration
- [ ] `pass` — placeholder / no-op
- [ ] `else` on loops — runs if loop completes without `break`
- [ ] **Ternary expressions** — `x if condition else y`
- [ ] Pattern matching (`match`/`case`) — Python 3.10+
    - Literal patterns
    - Capture patterns
    - Sequence & mapping patterns
    - Guard clauses (`if` in case)

---

### 📦 1.3 Core Data Structures

#### Lists

- [ ] Creation, indexing, slicing
- [ ] Mutability — in-place modification
- [ ] Methods: `.append()`, `.extend()`, `.insert()`, `.remove()`, `.pop()`, `.sort()`, `.reverse()`, `.copy()`
- [ ] Shallow vs deep copy (`copy.copy()` vs `copy.deepcopy()`)
- [ ] List as stack & queue
- [ ] Nested lists (2D grids)

#### Tuples

- [ ] Immutability — why & when
- [ ] Packing & unpacking — `a, b, c = (1, 2, 3)`
- [ ] Star unpacking — `first, *rest = items`
- [ ] Single-element tuple — `(x,)`
- [ ] Named tuples (`collections.namedtuple`, `typing.NamedTuple`)
- [ ] Use as dict keys (hashability)

#### Sets

- [ ] Creation: `{1, 2, 3}` vs `set()`
- [ ] Deduplication
- [ ] Membership testing — O(1)
- [ ] Set operations: `|` union, `&` intersection, `-` difference, `^` symmetric difference
- [ ] `frozenset` — immutable set
- [ ] When to use sets vs lists

#### Dictionaries

- [ ] Creation, access, `.get()` with default
- [ ] `.keys()`, `.values()`, `.items()`
- [ ] `.update()`, `.pop()`, `.setdefault()`
- [ ] Dict unpacking `{**d1, **d2}`
- [ ] Insertion-order guarantee (Python 3.7+)
- [ ] `defaultdict`, `OrderedDict`, `Counter` (`collections` module)
- [ ] Dictionary comprehensions
- [ ] Nested dicts

---

### 🔄 1.4 Iteration System

- [ ] **Iterables vs Iterators** — what's the difference?
- [ ] `iter()` and `next()` — manual iteration
- [ ] `StopIteration` exception
- [ ] `__iter__` and `__next__` dunder methods
- [ ] **Custom iterators** — class-based implementation
- [ ] **Built-in helpers**
    - `enumerate(iterable, start=0)` — index + value
    - `zip(*iterables)` — parallel iteration; `zip_longest`
    - `map(func, iterable)` — lazy transform
    - `filter(func, iterable)` — lazy filter
    - `sorted(iterable, key=..., reverse=...)` — returns new list
    - `reversed()` — reverse iterator
    - `all(iterable)` / `any(iterable)` — short-circuit booleans
    - `min()`, `max()` with `key=` argument
    - `sum()`, `len()`

---

### ⚙️ 1.5 Functions

- [ ] Defining with `def`, return values, implicit `None`
- [ ] Positional, keyword, default arguments
- [ ] **Argument types**
    - `*args` — variable positional
    - `**kwargs` — variable keyword
    - Keyword-only args (after `*`)
    - Positional-only args (before `/`) — Python 3.8+
    - Argument order: `pos / pos_or_kw * kw_only **kwargs`
- [ ] **Mutable default argument pitfall** — use `None` sentinel
- [ ] Variable scope — LEGB rule (Local → Enclosing → Global → Built-in)
- [ ] `global` and `nonlocal` keywords
- [ ] **Lambda functions** — `lambda x: x * 2`, limitations
- [ ] **Recursion**
    - Base case & recursive case
    - Call stack & stack overflow
    - Tail recursion (Python doesn't optimize it)
    - `sys.setrecursionlimit()`
- [ ] **First-class functions** — assign, pass, return functions
- [ ] **Higher-order functions** — accept/return functions
- [ ] **Closures** — inner function capturing outer scope; `__closure__`
- [ ] **Decorators**
    - Syntax `@decorator`
    - Execution order
    - Decorator with arguments (decorator factory)
    - Stacking decorators
    - `functools.wraps` — preserving metadata
    - Class-based decorators
- [ ] **Type hints** — `def greet(name: str) -> str:`
    - `Optional`, `Union`, `List`, `Dict`, `Tuple`
    - `Any`, `Callable`, `TypeVar`
    - Python 3.10+ union syntax `int | str`

---

### 🌀 1.6 Generators (Key Skill)

- [ ] `yield` keyword — pausing execution
- [ ] Generator function lifecycle — suspended frame
- [ ] `next()` calls & `StopIteration`
- [ ] **Generator expressions** — `(x**2 for x in range(10))`
- [ ] Lazy evaluation — why it matters for memory
- [ ] **`send()`** — sending values into a generator
- [ ] **`throw()`** — injecting exceptions
- [ ] **`close()`** — terminating a generator
- [ ] **`yield from`** — delegation to sub-generators
- [ ] Use cases: streaming data, infinite sequences, pipelines, large file processing
- [ ] Generator pipelines — chaining generators
- [ ] Generators vs list comprehensions — tradeoff

---

### 🔁 Recap — Foundations Self-Test

> Can you answer these without looking?

- What is the difference between `is` and `==`?
- What are falsy values in Python?
- What is the LEGB rule?
- What happens when you use a mutable default argument?
- What does `yield from` do?
- What's the difference between an iterable and an iterator?

---

## 🧰 2. Object-Oriented Programming (OOP)

### 2.1 Core Concepts

- [ ] Classes & Objects — blueprints and instances
- [ ] `__init__` constructor
- [ ] Instance attributes vs Class attributes
- [ ] `self` — the instance reference
- [ ] Methods: instance, class (`@classmethod`), static (`@staticmethod`)
- [ ] `cls` in classmethods — factory patterns
- [ ] **Encapsulation**
    - Public, `_protected`, `__private` (name mangling)
- [ ] **Properties & Descriptors**
    - `@property`, `@setter`, `@deleter`
    - Descriptors: `__get__`, `__set__`, `__delete__`
    - Non-data vs data descriptors

---

### 2.2 Inheritance & Polymorphism

- [ ] Single inheritance — `class Dog(Animal):`
- [ ] `super()` — calling parent methods
- [ ] **Multiple inheritance**
- [ ] **MRO (Method Resolution Order)** — C3 linearization, `__mro__`, `mro()`
- [ ] **Polymorphism** — same interface, different behavior
- [ ] Duck typing — "if it walks like a duck…"
- [ ] **Abstract Base Classes (ABC)**
    - `from abc import ABC, abstractmethod`
    - Enforcing interface contracts
- [ ] **Interfaces via Protocols** (`typing.Protocol`) — structural subtyping
- [ ] **Mixins** — reusable behavior without full inheritance

---

### 2.3 Dunder (Magic) Methods

- [ ] `__str__` vs `__repr__`
- [ ] `__len__`, `__getitem__`, `__setitem__`, `__delitem__` — sequence protocol
- [ ] `__contains__` — `in` operator
- [ ] `__iter__`, `__next__` — iterable protocol
- [ ] `__call__` — callable objects
- [ ] `__enter__`, `__exit__` — context manager protocol
- [ ] **Operator overloading**: `__add__`, `__sub__`, `__mul__`, `__eq__`, `__lt__`, `__le__`, etc.
- [ ] `__hash__` — hashability; relationship with `__eq__`
- [ ] `__bool__` — truthiness
- [ ] `__slots__` — memory optimization, disabling `__dict__`
- [ ] `__new__` vs `__init__` — instance creation

---

### 2.4 Advanced OOP

- [ ] **Dataclasses** (`@dataclass`)
    - Auto-generated `__init__`, `__repr__`, `__eq__`
    - `field()`, `default_factory`
    - Frozen dataclasses (immutable)
    - `__post_init__`
    - `@dataclass(slots=True)` — Python 3.10+
- [ ] **Composition vs Inheritance** — prefer composition
- [ ] **Metaclasses**
    - `type` is the metaclass of all classes
    - `__new__` in metaclass
    - `__init_subclass__` — lighter alternative
    - `__class_getitem__` — generics support
    - Awareness-level: when to use, when to avoid
- [ ] `__init_subclass__` hook
- [ ] Class decorators

---

### 🔁 Recap — OOP Self-Test

- What is the MRO and how does Python resolve it?
- What's the difference between `__str__` and `__repr__`?
- When would you use a Protocol instead of ABC?
- What does `@property` do and why use it over direct attribute access?
- What problem do `__slots__` solve?

---

## 📦 3. Modules, Packages & Best Practices

### 3.1 Modules & Imports

- [ ] `import module`, `from module import name`, `import module as alias`
- [ ] `__name__ == "__main__"` guard
- [ ] Module search path (`sys.path`)
- [ ] Relative imports — `.`, `..`
- [ ] Circular imports — detection and resolution
- [ ] Lazy imports — deferring heavy imports
- [ ] `importlib` — dynamic imports

### 3.2 Packages

- [ ] `__init__.py` — making a package
- [ ] `__all__` — controlling `from package import *`
- [ ] Namespace packages (no `__init__.py`) — Python 3.3+
- [ ] Package layout conventions

### 3.3 Environment & Dependency Management

- [ ] `venv` — creating and activating virtual environments
- [ ] `pip` — install, freeze, requirements.txt
- [ ] `pipenv` — Pipfile + lock file
- [ ] `poetry` — modern dependency + publishing
- [ ] `pyproject.toml` — unified config (PEP 517/518)
- [ ] Pinning vs range-based dependencies

### 3.4 Project Structure

```
my_project/
├── src/
│   └── my_package/
│       ├── __init__.py
│       └── core.py
├── tests/
├── pyproject.toml
├── README.md
└── .env
```

### 3.5 Configuration & Logging

- [ ] **Logging** — `logging` module
    - Levels: DEBUG, INFO, WARNING, ERROR, CRITICAL
    - Handlers, formatters, filters
    - `logging.config.dictConfig()`
    - Structured logging (`structlog`)
- [ ] **Configuration management**
    - `python-dotenv` — `.env` files
    - `configparser` — INI files
    - `pydantic-settings` — type-safe config

---

## 🧪 4. Testing & Quality

### 4.1 Testing Frameworks

- [ ] **`unittest`** — built-in
    - `TestCase`, `setUp`, `tearDown`
    - Assertions: `assertEqual`, `assertRaises`, `assertIn`
- [ ] **`pytest`** — preferred
    - Test discovery conventions
    - `assert` rewriting
    - `-v`, `-k`, `-x`, `--tb` flags
- [ ] **Fixtures** — `@pytest.fixture`, `scope` (function/class/module/session)
- [ ] **Parametrize** — `@pytest.mark.parametrize`
- [ ] **Mocking** — `unittest.mock`
    - `Mock`, `MagicMock`, `patch`, `patch.object`
    - `side_effect`, `return_value`
    - Spy pattern
- [ ] **Code coverage** — `pytest-cov`, coverage reports, `.coveragerc`

### 4.2 Testing Strategies

- [ ] Unit tests — testing in isolation
- [ ] Integration tests — testing interactions
- [ ] E2E tests — full system tests
- [ ] **TDD workflow** — Red → Green → Refactor
- [ ] Property-based testing — `hypothesis`
- [ ] Testing async code — `pytest-asyncio`
- [ ] Test doubles — stubs, fakes, mocks, spies

### 4.3 Code Quality

- [ ] **Linting**
    - `flake8` — PEP8 compliance
    - `pylint` — deeper analysis
    - `ruff` — fast modern linter (replaces flake8 + isort)
- [ ] **Formatting** — `black` (opinionated), `isort` (import sorting)
- [ ] **Type checking** — `mypy`, `pyright`
- [ ] **Pre-commit hooks** — `.pre-commit-config.yaml`
- [ ] Secure coding
    - Avoid `eval()`, `exec()`
    - SQL injection prevention
    - Input validation
    - `bandit` — security linter

---

## ⚙️ 5. Concurrency & Parallelism

### 5.1 Threading

- [ ] `threading.Thread` — creation, `.start()`, `.join()`
- [ ] **GIL (Global Interpreter Lock)** — what it is, why it exists
- [ ] Thread safety — race conditions
- [ ] **Synchronization primitives**: `Lock`, `RLock`, `Semaphore`, `Event`, `Condition`, `Barrier`
- [ ] `threading.local()` — thread-local storage
- [ ] **`ThreadPoolExecutor`** — `concurrent.futures`
    - `submit()`, `map()`, futures
    - `as_completed()`
- [ ] Daemon threads
- [ ] When threading helps (I/O-bound) vs when it doesn't (CPU-bound)

### 5.2 Multiprocessing

- [ ] `multiprocessing.Process` — creation, IPC
- [ ] **Bypassing GIL** — true parallelism
- [ ] Shared memory — `Value`, `Array`, `Manager`
- [ ] Message passing — `Queue`, `Pipe`
- [ ] **`ProcessPoolExecutor`** — `concurrent.futures`
- [ ] `Pool.map()`, `starmap()`
- [ ] Pickling — what can/can't be pickled
- [ ] `multiprocessing.pool` — worker processes
- [ ] When to use: CPU-bound tasks

### 5.3 AsyncIO & Coroutines (Deep)

- [ ] **What is a coroutine?** — `async def`, returning a coroutine object
- [ ] `await` — suspension point, yielding control
- [ ] **Event loop mechanics** — `asyncio.get_event_loop()`, `asyncio.run()`
- [ ] Scheduling coroutines — `asyncio.create_task()`, `asyncio.ensure_future()`
- [ ] **`asyncio.gather()`** — run coroutines concurrently
- [ ] **`asyncio.wait()`** — with `FIRST_COMPLETED`, `FIRST_EXCEPTION`
- [ ] **`asyncio.wait_for()`** — timeout on coroutines
- [ ] **`asyncio.shield()`** — protect from cancellation
- [ ] **Async iterators** — `async for`, `__aiter__`, `__anext__`
- [ ] **Async generators** — `async def` + `yield`
- [ ] **Async context managers** — `async with`, `__aenter__`, `__aexit__`
- [ ] **Queues** — `asyncio.Queue`, producer-consumer pattern
- [ ] **Semaphores** — `asyncio.Semaphore` for rate limiting
- [ ] **Task cancellation** — `task.cancel()`, `CancelledError`, cleanup
- [ ] **Avoiding blocking I/O** — `asyncio.to_thread()`, `loop.run_in_executor()`
- [ ] Coroutines vs threads vs processes — decision matrix
- [ ] Combining async + threads safely
- [ ] Debugging — `asyncio.get_event_loop().set_debug(True)`, `asyncio.all_tasks()`
- [ ] Task & coroutine leaks — detection and prevention
- [ ] **`anyio`** — async compatibility layer (awareness)
- [ ] **`trio`** — structured concurrency alternative (awareness)

---

### 🔁 Recap — Concurrency Self-Test

- Why doesn't threading help with CPU-bound tasks?
- What is the event loop and how does it schedule work?
- When would you use `gather` vs `wait`?
- What happens when you `cancel()` a task?
- How do you run blocking code inside an async function?

---

## 🌐 6. File I/O, Databases & Networking

### 6.1 File I/O

- [ ] `open()` — modes `r`, `w`, `a`, `b`, `x`, `+`
- [ ] `with` statement — auto-close guarantee
- [ ] `.read()`, `.readline()`, `.readlines()`, `.write()`, `.writelines()`
- [ ] Large files — line-by-line iteration
- [ ] **Context managers** — `__enter__`, `__exit__`, `contextlib.contextmanager`
- [ ] `contextlib.suppress()`, `contextlib.ExitStack`
- [ ] `pathlib.Path` — modern file path handling
    - `.read_text()`, `.write_text()`, `.glob()`, `.rglob()`
    - `.stat()`, `.exists()`, `.mkdir()`
- [ ] `os` and `shutil` — file operations
- [ ] `tempfile` — temporary files and directories
- [ ] `io.StringIO`, `io.BytesIO` — in-memory file objects

### 6.2 Serialization Formats

- [ ] **CSV** — `csv.reader`, `csv.writer`, `csv.DictReader`, `csv.DictWriter`
- [ ] **JSON** — `json.loads`, `json.dumps`, `json.load`, `json.dump`; custom encoders/decoders
- [ ] **YAML** — `PyYAML` (`safe_load`/`safe_dump`), `ruamel.yaml`
- [ ] **XML** — `xml.etree.ElementTree`, `lxml`
- [ ] **TOML** — `tomllib` (built-in Python 3.11+), `tomli`
- [ ] **Pickle** — `pickle.dumps`/`loads`; security warnings
- [ ] **MessagePack / Protocol Buffers** — binary formats (awareness)

### 6.3 Databases

- [ ] **SQLite** — `sqlite3` module, connection, cursor, parameterized queries
- [ ] SQL basics: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `JOIN`, transactions
- [ ] **SQLAlchemy**
    - Core (expression language)
    - ORM — `declarative_base`, models, sessions
    - Relationships: one-to-one, one-to-many, many-to-many
    - Migrations with `alembic`
- [ ] **Async ORM** — `Tortoise-ORM`, `SQLAlchemy async`
- [ ] **PostgreSQL** — `psycopg2`, `asyncpg`
- [ ] **MongoDB** — `pymongo`, `motor` (async)
- [ ] **Redis** — `redis-py`, `aioredis` — caching, pub/sub, rate limiting

### 6.4 Networking

- [ ] **HTTP requests** — `requests` (sync), `httpx` (sync + async)
    - GET, POST, PUT, DELETE, PATCH
    - Headers, params, auth, timeout, retries
    - Session reuse
- [ ] **`aiohttp`** — async HTTP client/server
- [ ] **Sockets** — `socket` module
    - TCP vs UDP
    - Server: bind, listen, accept
    - Client: connect, send, recv
    - Async sockets with asyncio
- [ ] **WebSockets** — `websockets`, `aiohttp` WS support
- [ ] Cloud storage APIs — `boto3` (AWS S3), `google-cloud-storage`

---

## 🚀 7. Web Frameworks

### 7.1 Flask (Sync, Micro)

- [ ] Routes & view functions
- [ ] Request & Response objects
- [ ] Templates (Jinja2)
- [ ] Blueprints — modular apps
- [ ] Flask extensions: Flask-SQLAlchemy, Flask-Login
- [ ] App factory pattern

### 7.2 Django (Batteries Included)

- [ ] MTV architecture — Model, Template, View
- [ ] ORM — models, migrations, querysets
- [ ] Admin panel
- [ ] URL routing
- [ ] Forms & validation
- [ ] Auth system
- [ ] Django REST Framework (DRF) — serializers, viewsets, routers
- [ ] Django Channels — async/WebSocket support

### 7.3 FastAPI (Async-First)

- [ ] Path operations — `@app.get()`, `@app.post()`, etc.
- [ ] **Pydantic models** — request/response validation
- [ ] Dependency injection — `Depends()`
- [ ] Path params, query params, request body
- [ ] Response models & status codes
- [ ] **Background tasks** — `BackgroundTasks`
- [ ] **Async streaming responses** — `StreamingResponse`
- [ ] **Middlewares** — custom, CORS, GZip
- [ ] **Auth/JWT** — OAuth2, `python-jose`, `passlib`
- [ ] Rate limiting — `slowapi`
- [ ] **API versioning** — prefix routing, header-based
- [ ] **OpenAPI schemas** — auto-generated docs (`/docs`, `/redoc`)
- [ ] WebSocket endpoints
- [ ] Lifespan events — startup/shutdown handlers

### 7.4 Common Web Concepts

- [ ] WSGI vs ASGI
- [ ] `gunicorn` — WSGI server
- [ ] `uvicorn` — ASGI server
- [ ] `hypercorn` — ASGI server (HTTP/2, HTTP/3)
- [ ] Reverse proxy — nginx, Caddy
- [ ] Cookie & session management
- [ ] CORS — Cross-Origin Resource Sharing
- [ ] CSRF protection

---

## 📡 8. Distributed Systems & Messaging

### 8.1 Communication Protocols

- [ ] **REST** — stateless, HTTP verbs, status codes, HATEOAS
- [ ] **RPC** — Remote Procedure Call concepts
- [ ] **gRPC**
    - Protocol Buffers (`.proto` files)
    - Sync + async stubs
    - Unary, server-streaming, client-streaming, bidirectional streaming
    - `grpcio`, `grpcio-tools`
- [ ] **GraphQL** — `strawberry`, `ariadne` (awareness)
- [ ] **WebSocket** — persistent bidirectional connection

### 8.2 Message Queues & Streaming

- [ ] **Kafka** — topics, partitions, consumer groups, offsets
    - `confluent-kafka`, `aiokafka`
- [ ] **RabbitMQ** — exchanges, queues, routing keys, `aio-pika`
- [ ] **Redis Streams** — `XADD`, `XREAD`, consumer groups
- [ ] Async event consumers
- [ ] **Idempotent message handling** — exactly-once semantics

### 8.3 Resilience Patterns

- [ ] **Retries & exponential backoff** — `tenacity`, `backoff`
- [ ] **Circuit breakers** — `pybreaker`
- [ ] **Connection pooling** — database + HTTP
- [ ] **Timeouts** — always set them
- [ ] **Dead letter queues**
- [ ] **Saga pattern** — distributed transactions

### 8.4 Task Queues

- [ ] **Celery** — tasks, workers, beat scheduler, results backend
- [ ] **RQ (Redis Queue)** — simpler alternative
- [ ] **Arq** — async task queue
- [ ] Task routing, priorities, chaining
- [ ] Monitoring — Flower (Celery), `rq-dashboard`

---

## 🤖 9. Performance, Memory & Internals

### 9.1 Profiling & Benchmarking

- [ ] `timeit` — micro-benchmarks
- [ ] `cProfile` — function-level profiling
- [ ] `pstats` — analyzing cProfile output
- [ ] `py-spy` — sampling profiler (no code changes)
- [ ] `line_profiler` — line-by-line
- [ ] `memory_profiler` — memory usage per line
- [ ] `tracemalloc` — built-in memory tracing

### 9.2 Time & Space Complexity

- [ ] Big-O notation — O(1), O(log n), O(n), O(n log n), O(n²)
- [ ] Python data structure complexity:
    - List: append O(1) amortized, insert O(n), lookup O(n)
    - Dict/Set: lookup O(1) average
    - `deque`: append/pop O(1) both ends
    - `heapq`: push/pop O(log n)
- [ ] Algorithm complexity of builtins (`sorted` = Timsort = O(n log n))

### 9.3 Memory Optimization

- [ ] `sys.getsizeof()` — object size
- [ ] `__slots__` vs `__dict__` — when slots win
- [ ] Generator expressions vs list comprehensions
- [ ] Object interning — small integers, short strings
- [ ] **Garbage collection**
    - Reference counting
    - Cyclic GC — `gc` module
    - `gc.collect()`, `gc.disable()`
    - Weak references — `weakref`

### 9.4 CPython Internals

- [ ] CPython architecture overview
- [ ] Bytecode — `.pyc` files
- [ ] `dis` module — disassembling bytecode
- [ ] GIL impact — `sys.getswitchinterval()`
- [ ] GIL bypass: multiprocessing, C extensions
- [ ] **C Extensions** — Cython, CFFI
- [ ] **PyPy** — JIT-compiled Python
- [ ] **Rust FFI** — `PyO3`, `maturin`
- [ ] `ctypes` — calling C libraries

---

## 🧠 10. Functional & Advanced Paradigms

### 10.1 Functional Programming

- [ ] **Pure functions** — no side effects, deterministic
- [ ] **Immutability** — prefer immutable data
- [ ] `map()`, `filter()`, `reduce()` (`functools.reduce`)
- [ ] **Comprehensions**
    - List: `[x for x in ...]`
    - Dict: `{k: v for k, v in ...}`
    - Set: `{x for x in ...}`
    - Generator: `(x for x in ...)`
    - Nested comprehensions
- [ ] **`functools`**
    - `partial` — partial application / currying
    - `lru_cache` / `cache` — memoization
    - `wraps` — decorator metadata
    - `reduce`, `total_ordering`, `singledispatch`
- [ ] **`itertools`**
    - `chain`, `islice`, `cycle`, `repeat`
    - `product`, `permutations`, `combinations`
    - `groupby`, `takewhile`, `dropwhile`
    - `accumulate`, `starmap`
    - `pairwise` (Python 3.10+)
- [ ] **Currying** — `functools.partial`, manual currying
- [ ] **Lazy evaluation** — generators, `itertools`

### 10.2 Advanced Patterns

- [ ] **Monads (light)** — `Maybe`, `Result` patterns; `returns` library
- [ ] **Structural pattern matching** (`match`/`case`) — revisit with complex patterns
- [ ] **Pipelines** — data pipelines with generators
- [ ] **Memoization** — `lru_cache`, manual caching
- [ ] `singledispatch` — function overloading by type
- [ ] `@overload` — type-hint overloads (typing)

---

## 🎁 11. Packaging, CLI & Deployment

### 11.1 CLI Tools

- [ ] `argparse` — built-in argument parsing
    - Positional & optional args, subparsers
- [ ] `Typer` — type-hint based CLI (built on Click)
- [ ] `Click` — decorator-based CLI
- [ ] Rich — beautiful terminal output (`rich`)
- [ ] `Textual` — TUI (Terminal User Interface) framework

### 11.2 Packaging

- [ ] `pyproject.toml` — unified project config
- [ ] Build backends: `setuptools`, `flit`, `hatchling`, `poetry`
- [ ] Building: `python -m build` → sdist + wheel
- [ ] Publishing to **PyPI** — `twine`, API tokens
- [ ] Versioning — Semantic Versioning (`semver`) — `MAJOR.MINOR.PATCH`
- [ ] `bumpversion` / `bump2version`
- [ ] `__version__` convention

### 11.3 Containerization & Deployment

- [ ] **Dockerizing Python apps**
    - Multi-stage builds
    - `.dockerignore`
    - Non-root user
    - Layer caching optimization
- [ ] **Docker Compose** — multi-service apps
- [ ] **gunicorn** — WSGI production server; `--workers`, `--worker-class`
- [ ] **uvicorn** + gunicorn with `uvicorn.workers.UvicornWorker`
- [ ] **Environment variables** in prod — secrets management
- [ ] **CI/CD**
    - GitHub Actions — test, lint, build, deploy
    - Automated PyPI publishing
    - Matrix testing across Python versions
- [ ] Health checks, graceful shutdown

---

## 🔍 12. Standard Library Essentials _(Gap Fill)_

> Often overlooked — powerful tools already built in.

- [ ] **`collections`** — `deque`, `Counter`, `defaultdict`, `namedtuple`, `ChainMap`
- [ ] **`heapq`** — min-heap, `nlargest`, `nsmallest`
- [ ] **`bisect`** — binary search on sorted lists
- [ ] **`dataclasses`** — (covered in OOP)
- [ ] **`enum`** — `Enum`, `IntEnum`, `Flag`, `auto()`
- [ ] **`datetime`** — dates, times, timedeltas, timezones (`zoneinfo`)
- [ ] **`re`** — regular expressions; groups, lookahead, flags
- [ ] **`pathlib`** — (covered in File I/O)
- [ ] **`contextlib`** — (covered in File I/O)
- [ ] **`functools`**, **`itertools`** — (covered in Functional)
- [ ] **`typing`** — type hints deep dive
    - `Generic`, `Protocol`, `TypedDict`, `Literal`
    - `get_type_hints()`, `TYPE_CHECKING`
- [ ] **`abc`** — Abstract Base Classes
- [ ] **`inspect`** — introspection: `signature`, `getsource`, `isfunction`
- [ ] **`ast`** — parse Python source into AST
- [ ] **`operator`** — `itemgetter`, `attrgetter`, `methodcaller`
- [ ] **`struct`** — pack/unpack binary data
- [ ] **`uuid`** — UUID generation
- [ ] **`hashlib`** — cryptographic hashing (SHA256, MD5)
- [ ] **`secrets`** — cryptographically secure randomness
- [ ] **`random`** — pseudo-random (not for security)
- [ ] **`math`**, **`statistics`** — math helpers
- [ ] **`pprint`** — pretty-print complex structures
- [ ] **`copy`** — shallow vs deep copy
- [ ] **`textwrap`**, **`string`** — text utilities
- [ ] **`subprocess`** — running system commands safely
- [ ] **`signal`** — Unix signal handling
- [ ] **`atexit`** — shutdown hooks

---

## 🎓 13. Capstone Projects

> Build these end-to-end to solidify everything.

|#|Project|Key Skills|
|---|---|---|
|1|**Async web scraper with backpressure**|asyncio, aiohttp, semaphore, generators|
|2|**Kafka microservice with FastAPI**|Kafka, async consumers, REST, Docker|
|3|**Mini task scheduler (Airflow-like)**|DAGs, async scheduling, Celery|
|4|**Custom iterator library**|`__iter__`, `__next__`, `yield from`, protocols|
|5|**Custom ORM with descriptors + metaclasses**|descriptors, metaclasses, SQL|
|6|**Distributed rate limiter**|Redis, sliding window algorithm, async|
|7|**Coroutine-based crawler**|asyncio, queues, circuit breakers|
|8|**Type-safe CLI tool published to PyPI**|Typer, packaging, PyPI, semver|
|9|**In-memory caching layer (mini-Redis)**|sockets, async, data structures|
|10|**gRPC service with async client**|Protobuf, gRPC, streaming|

---

## 📚 Quick Reference — Decision Matrix

|Task type|Tool|
|---|---|
|I/O-bound concurrency|`asyncio` or `ThreadPoolExecutor`|
|CPU-bound parallelism|`ProcessPoolExecutor` or `multiprocessing`|
|Simple background jobs|`threading.Thread`|
|Heavy data processing|generators + `itertools`|
|Shared mutable state|`threading.Lock` / `asyncio.Lock`|
|Large datasets|generators, `itertools.islice`|
|Fast lookups|`dict` or `set`|
|Sorted + fast insert|`heapq` or `bisect`|
|Type safety|`mypy` + type hints|
|Config management|`pydantic-settings`|
|Production API|FastAPI + uvicorn + gunicorn|
