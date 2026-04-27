# Java

---

# 🔥 FAANG-Level Java Mastery Roadmap

---

## ✨ **1. Java Fundamentals & Internals**

### 🔹 Core Java Concepts

- Data Types, Variables, Operators
- Control Statements (if-else, loops, switch)
- Methods, Overloading, Recursion
- Arrays and Multidimensional Arrays
- String, StringBuffer, StringBuilder
- Java Packages & Imports
- Exception Handling (Checked vs Unchecked)
- Inner classes, Anonymous classes
- Static blocks, instance blocks
- Java Naming Conventions & Code Style
- hashCode, equals

**Scenarios:**

- What happens when you access an array out of bounds?
- How does method overloading resolution behave with `null` arguments?
- Differences in behavior when exceptions are rethrown vs wrapped

### 🔹 OOPs & Design Principles

- Class, Object, Inheritance, Encapsulation, Abstraction, Polymorphism
- Constructors, Constructor Overloading
- SOLID Principles
- Design Patterns (Singleton, Factory, Builder, Strategy, Observer, etc.)
- Access Modifiers & Encapsulation
- The `this` keyword, static/final modifiers

**Scenarios:**

- What happens when a subclass hides a static method?
- Mutable vs Immutable objects in design pattern implementation
- Constructor chaining and inheritance pitfalls

### 🔹 JVM Internals

- JVM Architecture: ClassLoader, Method Area, Heap, Stack, Native Stack, PC Register
- Class Loading (Bootstrap, Extension, Application ClassLoaders)
- Bytecode, Class File Structure
- Just-In-Time (JIT) Compiler: C1 vs C2, Tiered Compilation
- Reflection API, Annotations
- Finalization, Object Resurrection, `finalize()` deprecation

**Scenarios:**

- How does the JVM behave when two classloaders load the same class?
- Performance impact of frequent reflection usage
- Difference in behavior between eagerly and lazily loaded classes

### 🔹 Memory Management

- Heap, Stack, Method Area, Native Stack
- Escape Analysis, Stack Allocation
- Reference Types: Strong, Soft, Weak, Phantom
- Java Serialization & Deserialization

**Scenarios:**

- Effect of SoftReference under memory pressure
- Object graph behavior during serialization
- TLAB behavior under frequent object creation

### 📌 Practice

- Use tools like `jconsole`, `jvisualvm`, `YourKit`, `JFR`
- Analyze heap dumps, GC logs, and thread dumps
- JVM tuning via flags: `Xms`, `Xmx`, `XX:+UseG1GC`, etc.

---

## 📂 **2. Collections Framework (Internals & Advanced Concepts)**

### 🔹 Core Collections

Note: **Study Data structure & Algorithm used by each collection interface/class internally and their time complexity**

- List: ArrayList, LinkedList
- Set: HashSet, LinkedHashSet, TreeSet
- Map: HashMap, LinkedHashMap, TreeMap, Hashtable
- Queue: PriorityQueue, Deque
- EnumMap, IdentityHashMap, WeakHashMap
- Comparator, Comparable

**Scenarios:**

- HashMap behavior with high load factor and hash collisions
- TreeSet sorting behavior with custom Comparator
- ArrayList resizing impact under bulk insertions

### 🔹 Advanced & Concurrent Collections

- ConcurrentHashMap, CopyOnWriteArrayList, CopyOnWriteArraySet
- BlockingQueue, ConcurrentLinkedQueue, DelayQueue
- ConcurrentSkipListMap, ConcurrentSkipListSet
- Fail-Fast vs Fail-Safe Iterators

**Scenarios:**

- Behavior of ConcurrentHashMap during key iteration and mutation
- CopyOnWriteArrayList performance tradeoff under high write load
- BlockingQueue behavior with full capacity

### 🔹 Hands-On

- Implement HashMap/LinkedList from scratch
- Performance tuning (load factor, initial capacity)
- Test concurrent access to custom data structures

---

## 🚀 **3. Multithreading & Concurrency**

### 🔹 Thread Basics

- Creating Threads (Thread, Runnable, Callable)
- Thread Lifecycle & State Transitions
- Thread Priorities, Daemon Threads
- .sleep(), .join(), .yield()

**Scenarios:**

- Thread starvation due to priority misconfiguration
- Unexpected behavior from forgetting to call `start()`

### 🔹 Synchronization

- synchronized methods/blocks
- `wait()`, `notify()`, `notifyAll()`
- ReentrantLock, ReadWriteLock, Locks

**Scenarios:**

- Missed signal problem with wait/notify
- Deadlock detection and resolution

### 🔹 java.util.concurrent Package

- Executors, ExecutorService, ThreadPoolExecutor
- Callable, Future, FutureTask
- BlockingQueue, LinkedBlockingQueue, PriorityBlockingQueue, ConcurrentHashMap
- Semaphore, CountDownLatch, CyclicBarrier, Phaser
- Atomic Variables (AtomicInteger, AtomicBoolean, etc.)

**Scenarios:**

- ThreadPool rejection policies when queue is full
- Behavior of CountDownLatch when await called after count reaches zero

### 🔹 Advanced Topics

- ThreadLocal, InheritableThreadLocal
- Volatile keyword, Happens-Before relationship
- Java Memory Model (JMM)
- Thread safety, race conditions, deadlocks, starvation

**Scenarios:**

- Memory visibility issues due to missing volatile
- Data race due to unsynchronized access

---

## 🚡 **4. Java 8 and Beyond**

### 🔹 Functional Programming

- Lambda Expressions
- Method References, Constructor References
- Functional Interfaces (Predicate, Consumer, Supplier, Function, BiFunction)

**Scenarios:**

- Difference in behavior with lambdas capturing vs not capturing variables
- Side-effects in lambdas breaking stream behavior

### 🔹 Streams API

- Intermediate and Terminal operations
- Stream pipeline, short-circuiting
- map, filter, reduce, flatMap, collect
- Parallel Streams and performance

**Scenarios:**

- Order sensitivity in parallel streams
- Incorrect use of mutable state in streams

### 🔹 Optional

- Avoiding null, orElse, map, flatMap, ifPresent

**Scenarios:**

- Optional chaining vs null checks
- Cost of wrapping primitives in Optional

### 🔹 Date and Time API

- java.time (LocalDate, LocalDateTime, ZonedDateTime, Duration, Period)

**Scenarios:**

- Daylight saving time handling in ZonedDateTime
- Parsing legacy `Date` into `LocalDate`

### 🔹 Interface Enhancements

- Default and Static methods in interfaces

**Scenarios:**

- Diamond problem with default methods
- Overriding static methods in interface

---

## 🚜 **5. Garbage Collection & Performance Tuning**

### 🔹 GC Algorithms

- Serial, Parallel, CMS, G1, ZGC, Shenandoah
- Minor GC vs Major GC vs Full GC
- TLAB, GC Roots, Reachability Analysis
- How to tune garbage collector for different types of application (data-intensive, I/O intensive, CPU intensive)

**Scenarios:**

- GC thrashing under memory pressure
- Long GC pause due to full heap

### 🔹 Tools

- jstat, jmap, jconsole, jvisualvm, JFR
- Eclipse MAT, YourKit, JProfiler

### 🔹 Tuning

- GC logs analysis, latency vs throughput tuning
- JVM flags for tuning

---

## 🔧 **6. Debugging, Profiling, and Best Practices**

### 🔹 Debugging

- IDE Debugging Tools (breakpoints, watches)
- Analyzing Thread Dumps & Heap Dumps

**Scenarios:**

- Analyzing deadlocks with `jstack`
- Diagnosing memory leaks via heap dump inspection

### 🔹 Profiling & Monitoring

- Java Mission Control, Flight Recorder
- VisualVM, jstack, jmap, jcmd

### 🔹 Logging

- SLF4J, Logback, Log4j2
- Logging best practices & MDC context

---

---

## 🔎 7**. Study & Practice Strategy**

- Read Effective Java (Joshua Bloch), Java Concurrency in Practice
- IMPORTANT NOTE: Study internals of everything
- Solve coding problems: Custom HashMap, Producer-Consumer, Thread-safe LRU cache
- Use openjdk source code for internals
- Simulate GC behavior and analyze memory consumption
- Convert imperative code to functional style using Streams
- Observe thread behavior in debugger and with profiling tools

---