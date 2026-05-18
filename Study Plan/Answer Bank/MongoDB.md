# MongoDB — Answer Bank

---

**Q: When should you embed vs reference documents?**

**Short:** Embed when data is always read together and the relationship is one-to-few. Reference when data is large, shared, or frequently updated independently.

**Detailed:**
| Embed | Reference |
|-------|---------|
| Data read together 95% of the time | Data queried independently |
| One-to-few (user → addresses) | One-to-many, many-to-many |
| Sub-document doesn't grow unboundedly | Sub-array can grow very large |
| No sharing needed | Same sub-document referenced by many |
| Example: blog post + comments (max 100) | Example: products + categories |

Rule of thumb: unbounded arrays in a document = bad. Max document size is 16MB.

---

**Q: Explain the MongoDB aggregation pipeline.**

**Short:** A sequence of stages that transform documents one step at a time — like a Unix pipe for data.

**Detailed:**
```javascript
db.orders.aggregate([
  { $match: { status: "completed" } },          // filter first (uses index)
  { $group: { _id: "$userId", total: { $sum: "$amount" } } },
  { $sort: { total: -1 } },
  { $limit: 10 },
  { $lookup: {
      from: "users",
      localField: "_id",
      foreignField: "_id",
      as: "user"
  }},
  { $unwind: "$user" },
  { $project: { "user.name": 1, total: 1 } }
]);
```
Always put `$match` and `$sort` early to reduce data before expensive stages. `$lookup` is MongoDB's LEFT OUTER JOIN.

---

**Q: What are the different index types in MongoDB?**

**Short:** Single field, Compound, Multikey (arrays), Text, Geospatial (2dsphere), TTL, Hashed, Wildcard, Partial, Sparse.

**Detailed:**
| Index | Use Case |
|-------|---------|
| Single field | Basic equality/range queries |
| Compound | Multi-field filter/sort |
| Multikey | Indexing array fields |
| Text | Full-text search (`$text`) |
| TTL | Auto-delete documents after expiry (sessions, logs) |
| 2dsphere | GPS coordinates, geospatial queries |
| Hashed | Shard key, equality only |
| Wildcard | Dynamic fields, unknown schema keys |
| Partial | Index subset of documents meeting a filter |

`db.collection.getIndexes()` — list all indexes. Check with `explain("executionStats")`.

---

**Q: What is COLLSCAN vs IXSCAN in explain output?**

**Short:** COLLSCAN = full collection scan (every document read). IXSCAN = index scan. COLLSCAN on a large collection = performance problem.

**Detailed:**
```javascript
db.users.find({ email: "x@y.com" }).explain("executionStats")
// "winningPlan": { "stage": "COLLSCAN" }  ← bad, no index
// "winningPlan": { "stage": "IXSCAN" }    ← good, using index

// Key metrics:
// totalDocsExamined >> nReturned = inefficient
// totalDocsExamined == nReturned = perfect selectivity
```

---

**Q: What is write concern and read concern in MongoDB?**

**Short:** Write concern = how many nodes must acknowledge a write before it's considered successful. Read concern = how fresh/consistent the data must be when read.

**Detailed:**
- **Write concern `w:1`** (default) — primary acknowledges. Fast but data could be lost if primary fails before replicating.
- **Write concern `w:majority`** — majority of nodes acknowledge. Slower but durable.
- **Write concern `w:0`** — fire and forget. Fastest, no acknowledgment.
- **Read concern `local`** (default) — latest data on the node (may not be committed to majority yet).
- **Read concern `majority`** — data acknowledged by majority — consistent.
- **Read concern `linearizable`** — strongest, ensures reading the latest committed write. Slowest.

---

**Q: How does MongoDB replica set election work?**

**Short:** When primary becomes unreachable, remaining members hold an election. Member with highest priority and most up-to-date oplog wins.

**Detailed:**
- Requires a majority vote to elect a new primary (3 nodes = 2 needed to elect).
- Arbiter: votes but holds no data — used to break ties in even-member sets.
- Election timeout: ~10 seconds after primary unreachable.
- `rs.status()` — check current primary and member states.
- Prevent elections: `priority: 0` on a member → never becomes primary (analytics replica).

---

**Q: How do you choose a good shard key?**

**Short:** High cardinality + even write distribution + supports common query patterns. Bad keys cause hotspots.

**Detailed:**
- **Cardinality:** enough distinct values to distribute across shards (e.g., `userId` is good, `status` with 3 values is bad)
- **Write distribution:** monotonically increasing keys (timestamps, ObjectId) cause hotspot on the last shard — use hashed sharding instead.
- **Query isolation:** if most queries filter by `userId`, shard on `userId` — queries go to one shard.
- **Hashed vs Ranged:** Hashed = even distribution, no range queries. Ranged = range queries efficient, hotspot risk.

---

**Q: What is Mongoose's `.lean()` and when should you use it?**

**Short:** `.lean()` returns plain JavaScript objects instead of full Mongoose documents — faster, less memory, no Mongoose overhead.

**Detailed:**
```javascript
// Without lean — returns full Mongoose Document with virtuals, methods, tracking
const user = await User.findById(id);

// With lean — returns plain POJO, ~2x faster
const user = await User.findById(id).lean();

// When to use lean:
// ✓ Read-only operations (API responses, data processing)
// ✓ When you don't need save(), virtuals, or middleware
// ✗ Don't use when you need to call .save() or use Mongoose methods
```

---

**Q: How do multi-document transactions work in MongoDB?**

**Short:** MongoDB 4.0+ supports multi-document ACID transactions on replica sets. MongoDB 4.2+ supports on sharded clusters. Session-based, similar to SQL transactions.

**Detailed:**
```javascript
const session = await mongoose.startSession();
session.startTransaction();

try {
  await Account.updateOne({ _id: fromId }, { $inc: { balance: -100 } }, { session });
  await Account.updateOne({ _id: toId }, { $inc: { balance: 100 } }, { session });
  await session.commitTransaction();
} catch (err) {
  await session.abortTransaction();
  throw err;
} finally {
  session.endSession();
}
```
Transactions are slower than single-document ops — design schema to avoid them when possible. Single-document atomicity is "free" in MongoDB.

---

**Q: How does the `$lookup` stage work in aggregation?**

**Short:** Performs a LEFT OUTER JOIN from one collection to another — fetches matching documents from the foreign collection.

**Detailed:**
```javascript
db.orders.aggregate([
  {
    $lookup: {
      from: "products",        // foreign collection
      localField: "productId", // field in orders
      foreignField: "_id",     // field in products
      as: "productDetails"     // output array field
    }
  },
  { $unwind: "$productDetails" }  // flatten the array
]);
```
`$lookup` is expensive — use sparingly, put `$match` before it to reduce input documents. For complex joins, use the pipeline form of `$lookup` (MongoDB 3.6+).

---

**Q: What is a TTL index and when is it useful?**

**Short:** Time-To-Live index automatically deletes documents after a specified time — perfect for sessions, tokens, logs, cache entries.

**Detailed:**
```javascript
// Expire documents 1 hour after createdAt
db.sessions.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 });

// Expire at a specific future date stored in the document
db.tokens.createIndex({ expiresAt: 1 }, { expireAfterSeconds: 0 });
// expiresAt field should be a Date — document expires AT that date
```
TTL background thread runs every 60 seconds — deletion is not instantaneous. Only works on `Date` fields.

---

## Links
- [[Study Plan/MongoDB]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
