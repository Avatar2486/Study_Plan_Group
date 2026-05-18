# Node.js — Answer Bank

---

**Q: What are the phases of the Node.js Event Loop?**

**Short:** timers → pending I/O → idle/prepare → poll → check → close callbacks.

**Detailed:**
- **Timers:** executes `setTimeout` / `setInterval` callbacks whose delay has expired
- **Pending I/O:** I/O callbacks deferred from the previous loop (e.g., TCP errors)
- **Poll:** retrieves new I/O events; blocks here if queue is empty (up to timer threshold)
- **Check:** `setImmediate()` callbacks run here — always after poll
- **Close:** `socket.on('close', ...)` type callbacks
- `process.nextTick()` runs BEFORE any phase transition — highest priority
- Promise microtasks run after `nextTick`, before the next loop phase

---

**Q: What is the difference between `process.nextTick()` and `setImmediate()`?**

**Short:** `nextTick` fires before any I/O in the current iteration. `setImmediate` fires in the check phase — after I/O.

**Detailed:**
```javascript
setImmediate(() => console.log("setImmediate"));
process.nextTick(() => console.log("nextTick"));
Promise.resolve().then(() => console.log("promise"));
console.log("sync");

// Output: sync → nextTick → promise → setImmediate
```
`nextTick` can starve the event loop if called recursively — prefer `setImmediate` for recursive async work.

---

**Q: What is the difference between CommonJS and ES Modules?**

**Short:** CJS uses `require()` / `module.exports` — synchronous, dynamic. ESM uses `import`/`export` — static, async, tree-shakable.

**Detailed:**
```javascript
// CommonJS
const fs = require('fs');        // synchronous, cached on first load
module.exports = { fn };

// ES Modules
import fs from 'node:fs';        // static — analyzable at parse time
export const fn = () => {};
```
- ESM: enables tree shaking, top-level `await`, native browser support
- Set `"type": "module"` in package.json for ESM, or use `.mjs` extension
- CJS: `__dirname`, `__filename` available. ESM: use `import.meta.url` instead

---

**Q: What are Node.js Streams? What is backpressure?**

**Short:** Streams process data in chunks rather than loading it all into memory. Backpressure is the signal to pause when the consumer is slower than the producer.

**Detailed:**
```javascript
const readable = fs.createReadStream('large.csv');
const writable = fs.createWriteStream('output.csv');

// .pipe() handles backpressure automatically
readable.pipe(writable);

// Manual — check writable.write() return value
readable.on('data', (chunk) => {
  const ok = writable.write(chunk);
  if (!ok) readable.pause();  // consumer is full
});
writable.on('drain', () => readable.resume()); // consumer ready again
```
Use `stream.pipeline()` from `stream/promises` for error-safe piping.

---

**Q: What is the difference between Worker Threads and Cluster module?**

**Short:** Worker Threads share memory in one process (for CPU-bound tasks). Cluster forks multiple processes each with their own memory (for load balancing HTTP servers).

**Detailed:**
- **Worker Threads:** `worker_threads` module. Share `SharedArrayBuffer`. True parallelism for CPU-heavy computation (image processing, crypto, ML inference).
- **Cluster:** `cluster.fork()` spawns N worker processes. Each listens on the same port — OS distributes connections. Used for multi-core HTTP server scaling.
- For I/O-bound: neither needed — async/await handles it.
- PM2 does cluster mode automatically in production.

---

**Q: What are common Node.js memory leaks and how do you detect them?**

**Short:** Event listener accumulation, closures holding references, global variables, unclosed DB connections.

**Detailed:**
```javascript
// Memory leak: accumulating listeners
emitter.on('data', handler);   // call .off() or .once() to clean up

// Detecting leaks:
// 1. process.memoryUsage() — watch heapUsed over time
// 2. --inspect flag + Chrome DevTools heap snapshot
// 3. clinic.js / 0x flamegraphs
// 4. heapdump npm package
```
In Express: always call `next()` or `res.end()` — pending requests hold memory. In timers: always `clearInterval`/`clearTimeout` when no longer needed.

---

**Q: How does Promise.all vs allSettled vs race vs any work?**

**Short:** `all` = fail-fast. `allSettled` = wait all. `race` = first settles. `any` = first succeeds.

**Detailed:**
```javascript
Promise.all([p1, p2])         // rejects if ANY rejects (fast fail)
Promise.allSettled([p1, p2])  // always fulfills — [{status:'fulfilled',value}, {status:'rejected',reason}]
Promise.race([p1, p2])        // first to settle (resolve OR reject) wins
Promise.any([p1, p2])         // first to RESOLVE wins; rejects only if ALL reject → AggregateError
```

---

**Q: What are JWT best practices in Node.js?**

**Short:** Short expiry (15min access token), RS256 over HS256, refresh tokens in httpOnly cookies, validate on every request.

**Detailed:**
- **HS256:** symmetric — secret shared between issuer and verifier (single server ok)
- **RS256:** asymmetric — private key signs, public key verifies (multi-service, better)
- Store refresh tokens in httpOnly, Secure, SameSite=Strict cookie — not localStorage (XSS safe)
- Validate `exp`, `iss`, `aud` claims on every request
- Keep access token short-lived (15min). Refresh token: 7–30 days, rotate on use, revoke on logout via DB blacklist

---

**Q: What are V8 hidden classes and why do they matter for performance?**

**Short:** V8 assigns a hidden class to each object based on its shape. Objects with the same shape share the same class — enabling JIT optimization. Changing shape (adding properties dynamically) breaks this.

**Detailed:**
```javascript
// GOOD — consistent shape, V8 can optimize
function Point(x, y) { this.x = x; this.y = y; }
const p1 = new Point(1, 2);
const p2 = new Point(3, 4);

// BAD — different shapes, deoptimizes
const a = { x: 1 };
const b = { x: 1, y: 2 }; // different hidden class from a
a.y = 2; // shape changed — V8 must deoptimize
```
Always initialize all properties in the constructor in the same order.

---

**Q: What is the difference between `spawn`, `exec`, `execFile`, and `fork` in child_process?**

**Short:** `spawn` = streaming, large output. `exec` = buffered, shell. `execFile` = direct binary. `fork` = Node.js child with IPC.

**Detailed:**
```javascript
// spawn — streams stdout/stderr, no shell, good for large output
spawn('ls', ['-la']);

// exec — runs in shell, buffers output, for short commands
exec('ls -la | grep .js', callback);

// execFile — like exec but no shell (safer, no injection risk)
execFile('node', ['script.js'], callback);

// fork — special case for Node.js files, opens IPC channel
fork('child.js');  // child can do process.send() / process.on('message')
```
Never use `exec` with user-provided input — shell injection risk.

---

**Q: How does Node.js handle errors in async code?**

**Short:** Unhandled Promise rejections crash the process (Node 15+). Always use try/catch in async functions or `.catch()` on Promises.

**Detailed:**
```javascript
// Async function — use try/catch
async function loadData() {
  try {
    const data = await fetchFromDB();
    return data;
  } catch (err) {
    logger.error(err);
    throw err; // re-throw or handle
  }
}

// Global handler (last resort)
process.on('unhandledRejection', (reason, promise) => {
  logger.error('Unhandled Rejection:', reason);
  process.exit(1);
});

// EventEmitter errors — always add error listener
emitter.on('error', (err) => console.error(err)); // else throws
```

---

**Q: What is Express middleware and how does the pipeline work?**

**Short:** Middleware functions with signature `(req, res, next)` — chained in order. `next()` passes to the next middleware. Order matters.

**Detailed:**
```javascript
app.use(express.json());           // 1. parse body
app.use(authMiddleware);           // 2. verify JWT
app.get('/data', async (req, res) => { // 3. route handler
  res.json({ ok: true });
});
// 4-param middleware = error handler (must be last)
app.use((err, req, res, next) => {
  res.status(500).json({ error: err.message });
});
```
If `next()` is never called, the request hangs. If `next(err)` is called, jumps to error handler.

---

## Links
- [[Study Plan/Node JS]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
