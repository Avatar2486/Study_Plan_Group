# Python — Answer Bank

---

**Q: What is the difference between `is` and `==`?**

**Short:** `==` checks value equality. `is` checks identity — same object in memory.

**Detailed:**
```python
a = [1, 2, 3]
b = [1, 2, 3]
a == b   # True  — same values
a is b   # False — different objects in memory
a is a   # True  — same object
```
Use `is` only for `None`, `True`, `False`. Never use `is` to compare strings or numbers (CPython interns small ones, but it's implementation-specific).

---

**Q: What are falsy values in Python?**

**Short:** `0`, `0.0`, `""`, `[]`, `{}`, `()`, `set()`, `None`, `False`.

**Detailed:**
Any object that evaluates to `False` in a boolean context. `bool(x)` returns `False` for all of these. Custom objects can define `__bool__` or `__len__` to control truthiness. `if not x:` is idiomatic Python for checking falsy.

---

**Q: What is the LEGB rule?**

**Short:** Variable lookup order: Local → Enclosing → Global → Built-in.

**Detailed:**
```python
x = "global"
def outer():
    x = "enclosing"
    def inner():
        x = "local"
        print(x)  # "local"
    inner()
```
`global x` inside a function lets you assign to global scope. `nonlocal x` lets inner function assign to enclosing scope.

---

**Q: What happens when you use a mutable default argument?**

**Short:** The default object is created once and shared across all calls — mutations persist between calls.

**Detailed:**
```python
def append(val, lst=[]):   # BAD — lst is created once
    lst.append(val)
    return lst

append(1)  # [1]
append(2)  # [1, 2]  ← not a fresh list!

# FIX: use None sentinel
def append(val, lst=None):
    if lst is None:
        lst = []
    lst.append(val)
    return lst
```

---

**Q: What does `yield from` do?**

**Short:** Delegates iteration to a sub-generator, passing values through in both directions.

**Detailed:**
```python
def gen_a():
    yield 1
    yield 2

def gen_b():
    yield from gen_a()  # delegates — same as: for x in gen_a(): yield x
    yield 3

list(gen_b())  # [1, 2, 3]
```
Also passes `send()` values and exceptions into the sub-generator, which plain `for` + `yield` doesn't do.

---

**Q: What is the difference between an iterable and an iterator?**

**Short:** An iterable has `__iter__`. An iterator has both `__iter__` and `__next__`.

**Detailed:**
- **Iterable:** can be looped over. `list`, `tuple`, `str`, `dict` — calling `iter(x)` returns an iterator.
- **Iterator:** stateful cursor. Calling `next()` advances it. Raises `StopIteration` when exhausted.
- An iterator IS an iterable (its `__iter__` returns itself). An iterable is NOT always an iterator.
- Generators are iterators.

---

**Q: What is the GIL and how does it affect Python?**

**Short:** The Global Interpreter Lock allows only one thread to execute Python bytecode at a time — CPU-bound threads don't run in parallel.

**Detailed:**
- CPython uses reference counting for memory management. The GIL prevents race conditions on reference counts.
- **Impact:** `ThreadPoolExecutor` doesn't speed up CPU-bound work. It DOES help I/O-bound work (GIL released during I/O).
- **Bypass:** Use `multiprocessing` (separate processes, no shared GIL) or C extensions (can release GIL).
- Python 3.13+ has experimental free-threaded mode (GIL optional).

---

**Q: What is the difference between `asyncio.gather` and `asyncio.wait`?**

**Short:** `gather` runs all coroutines concurrently and returns results in order. `wait` gives more control — first completed, first exception, etc.

**Detailed:**
```python
# gather — all results at once
results = await asyncio.gather(task1(), task2(), return_exceptions=True)

# wait — get completed sets
done, pending = await asyncio.wait(tasks, return_when=asyncio.FIRST_COMPLETED)
```
- `gather` cancels all if one fails (unless `return_exceptions=True`)
- `wait` never cancels — you manage pending tasks yourself
- Use `gather` for "run all, get all results". Use `wait` for "stop as soon as one succeeds/fails".

---

**Q: What is the difference between `__str__` and `__repr__`?**

**Short:** `__repr__` is for developers (unambiguous, ideally eval-able). `__str__` is for end users (readable).

**Detailed:**
```python
class Point:
    def __repr__(self): return f"Point(x={self.x}, y={self.y})"
    def __str__(self):  return f"({self.x}, {self.y})"
```
- `repr(obj)` → `__repr__`. `str(obj)` → `__str__`. If `__str__` not defined, Python falls back to `__repr__`.
- In f-strings: `f"{p!r}"` calls `__repr__`, `f"{p}"` calls `__str__`.
- Always define `__repr__`. `__str__` is optional.

---

**Q: What is MRO and how does Python resolve it?**

**Short:** Method Resolution Order — the order Python searches classes for a method. Computed using C3 linearization.

**Detailed:**
```python
class A: pass
class B(A): pass
class C(A): pass
class D(B, C): pass

D.__mro__  # D → B → C → A → object
```
Rule: left-to-right depth-first, but no class appears before all its subclasses. `super()` follows MRO. `ClassName.__mro__` shows the full order.

---

**Q: When would you use a Protocol instead of ABC?**

**Short:** Protocol enables structural subtyping ("duck typing with types") — no inheritance needed. ABC requires explicit inheritance.

**Detailed:**
```python
from typing import Protocol

class Drawable(Protocol):
    def draw(self) -> None: ...

class Circle:          # No inheritance from Drawable
    def draw(self): print("circle")

def render(shape: Drawable): shape.draw()
render(Circle())  # Works — Circle satisfies the protocol structurally
```
Use Protocol when you can't or don't want to force inheritance (third-party classes, simple interfaces).

---

**Q: What do `__slots__` do?**

**Short:** Replace the per-instance `__dict__` with a fixed-size array — less memory, slightly faster attribute access.

**Detailed:**
```python
class Point:
    __slots__ = ('x', 'y')

p = Point()
p.x = 1
p.z = 3  # AttributeError — can't add new attributes
```
- Saves ~40–50% memory for classes with many instances.
- Can't add arbitrary attributes. No `__dict__` unless explicitly added to `__slots__`.
- Good for data-heavy classes (e.g., parsing millions of records).

---

**Q: What is the difference between `@classmethod` and `@staticmethod`?**

**Short:** `classmethod` receives `cls` (the class). `staticmethod` receives nothing — it's just a regular function in the class namespace.

**Detailed:**
```python
class User:
    count = 0

    @classmethod
    def get_count(cls):      # cls = User or subclass
        return cls.count

    @staticmethod
    def validate_email(email):  # no cls, no self
        return "@" in email
```
Use `classmethod` for factory methods or accessing class state. Use `staticmethod` for utility functions that logically belong to the class but need no class/instance access.

---

**Q: How do decorators work?**

**Short:** A decorator is a function that takes a function and returns a new function — wrapping the original behavior.

**Detailed:**
```python
def log(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print("Done")
        return result
    return wrapper

@log
def greet(name): return f"Hello {name}"
# Same as: greet = log(greet)
```
Always use `@functools.wraps(func)` inside wrapper to preserve `__name__`, `__doc__`.

---

**Q: How do you run blocking code inside an async function?**

**Short:** Use `asyncio.to_thread()` (Python 3.9+) or `loop.run_in_executor()` to run blocking code in a thread pool.

**Detailed:**
```python
import asyncio

def blocking_io():
    import time; time.sleep(2)  # blocking
    return "done"

async def main():
    result = await asyncio.to_thread(blocking_io)
    # Or: loop = asyncio.get_event_loop()
    # result = await loop.run_in_executor(None, blocking_io)
```
Never call blocking I/O directly in async — it blocks the entire event loop.

---

## Links
- [[Study Plan/Python]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
