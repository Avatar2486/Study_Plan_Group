# MongoDB

> Reference: [mongodb.com/docs](https://www.mongodb.com/docs/) | [mongoosejs.com](https://mongoosejs.com/)

---

## 🔰 **1. Core Concepts & Data Model**

- What is MongoDB? Document database vs relational database
- BSON — Binary JSON, supported data types beyond JSON (ObjectId, Date, Binary, Decimal128)
- Documents — key-value pairs, nested documents, arrays
- Collections — schema-less by default, logical grouping of documents
- Databases — multiple DBs in one MongoDB instance
- ObjectId — structure (timestamp + random + counter), auto-generated `_id`
- MongoDB Atlas vs self-hosted — managed vs on-premises
- MongoDB vs PostgreSQL vs MySQL — when to choose MongoDB
- Namespace — `database.collection` format
- MongoDB shell — `mongosh` commands
- Schema design philosophy — embed vs reference (join)

---

## 🏗️ **2. Architecture & Internals**

- WiredTiger storage engine — default since 3.2, compression, MVCC
- Document-level concurrency — WiredTiger uses optimistic document-level locking
- Memory-mapped storage (MMAP) — old engine, replaced by WiredTiger
- Journal — write-ahead log equivalent, ensures durability on crash
- Oplog (Operations Log) — capped collection used for replication
- Replica Set internals — primary election (Raft-based), oplog replication
- Write concern — `w:1`, `w:majority`, `w:0` — durability vs performance tradeoff
- Read concern — `local`, `majority`, `linearizable` — freshness of reads
- Read preference — `primary`, `primaryPreferred`, `secondary`, `nearest`
- Working set — data + indexes that fit in RAM — key to MongoDB performance
- Collection scan vs index scan — `collectionScan: true` in explain is the warning

---

## 📑 **3. Indexing**

- Single field index — ascending (1) or descending (-1)
- Compound index — multiple fields, order matters for sort + filter
- Multikey index — automatically created when indexing an array field
- Text index — full-text search, `$text` operator, one text index per collection
- Geospatial index — `2dsphere` (GPS coords), `2d` (flat plane)
- Hashed index — for hash-based sharding, equality only
- Wildcard index — index all fields or a subset using `$**`
- TTL (Time-To-Live) index — auto-delete documents after expiry (e.g. sessions, logs)
- Partial index — index only documents matching a filter expression
- Sparse index — only index documents that have the indexed field
- Unique index — enforce uniqueness, `_id` is always unique
- `explain("executionStats")` — reading IXSCAN vs COLLSCAN, nReturned, totalDocsExamined
- Index intersection — MongoDB can merge two indexes for one query
- `hint()` — force a specific index
- `db.collection.getIndexes()` — list all indexes
- Covered query — query + projection fully satisfied from index, no document fetch

---

## 🔄 **4. CRUD Operations**

- `insertOne`, `insertMany` — insert documents
- `findOne`, `find` — read with query filter, projection
- `updateOne`, `updateMany`, `replaceOne` — update operators
- Update operators — `$set`, `$unset`, `$inc`, `$push`, `$pull`, `$addToSet`, `$pop`, `$rename`
- `deleteOne`, `deleteMany` — remove documents
- `findOneAndUpdate`, `findOneAndDelete` — atomic read-modify operations
- `upsert: true` — insert if not found, update if found
- Bulk operations — `bulkWrite` — ordered vs unordered, performance benefits
- `countDocuments` vs `estimatedDocumentCount` — accuracy vs speed
- `distinct` — unique values for a field
- Projections — include (`1`) or exclude (`0`) fields, `_id: 0` to remove id
- Query operators — `$eq`, `$ne`, `$gt`, `$lt`, `$gte`, `$lte`, `$in`, `$nin`, `$exists`, `$type`
- Logical operators — `$and`, `$or`, `$nor`, `$not`
- Array query operators — `$all`, `$elemMatch`, `$size`
- `$regex` — pattern matching (watch for index usage)
- Cursor methods — `.sort()`, `.limit()`, `.skip()`, `.toArray()`, `.forEach()`

---

## 🔀 **5. Aggregation Framework**

- What is the aggregation pipeline? — sequence of stages that transform documents
- `$match` — filter documents (like WHERE), put early to reduce data
- `$project` — reshape documents, include/exclude fields, computed fields
- `$group` — group by field, use accumulators: `$sum`, `$avg`, `$min`, `$max`, `$count`, `$push`, `$addToSet`
- `$sort` — sort documents (can use index if early in pipeline)
- `$limit` / `$skip` — pagination
- `$lookup` — left outer join between collections (like SQL JOIN)
- `$unwind` — deconstruct array field into separate documents
- `$addFields` — add new fields to documents
- `$replaceRoot` — promote embedded document to top level
- `$facet` — run multiple sub-pipelines in parallel
- `$bucket` / `$bucketAuto` — range-based grouping
- `$count` — count documents in pipeline
- `$out` — write pipeline result to a collection
- `$merge` — merge pipeline result into existing collection
- Pipeline optimization — stage order matters, `$match` + `$sort` before `$lookup`
- Aggregation explain — `db.collection.aggregate([...]).explain("executionStats")`
- `$expr` — use aggregation expressions inside `$match`
- `$graphLookup` — recursive graph traversal

---

## 🏛️ **6. Schema Design**

### Embed vs Reference
- Embed — related data inside the same document (denormalized)
  - Good for: data always read together, one-to-few relationships
  - Bad for: large/unbounded arrays, data shared across many documents
- Reference — store ObjectId and use `$lookup` or app-level join
  - Good for: many-to-many, large related data, frequently updated sub-data
  - Bad for: many joins = multiple round trips

### Common Patterns
- Polymorphic pattern — different document shapes in one collection
- Bucket pattern — group time-series data (e.g., 1 doc = 1 hour of sensor readings)
- Outlier pattern — handle documents that grow beyond normal bounds
- Computed pattern — pre-compute and store derived values (avoid re-computation on read)
- Subset pattern — store most-used fields in main doc, rest in separate collection
- Extended reference pattern — embed frequently read fields from referenced doc
- Approximation pattern — approximate counters instead of exact (e.g., view counts)
- Schema validation — `$jsonSchema` validator, enforce required fields + types

---

## 🔁 **7. Transactions & Consistency**

- Single-document atomicity — MongoDB guarantees atomic read-modify-write on one document
- Multi-document transactions — supported since MongoDB 4.0 on replica sets
- Multi-document transactions (sharded) — since MongoDB 4.2
- Transaction syntax — `session.startTransaction()`, `session.commitTransaction()`, `session.abortTransaction()`
- Write concern in transactions — ensure majority acknowledgment
- Read concern in transactions — `snapshot` for consistent reads across documents
- Transaction performance cost — slower than single-document ops, avoid overuse
- Idempotent write patterns — design ops safe to retry on failure
- Optimistic concurrency control — version field + conditional update pattern

---

## 🔀 **8. Replication & Sharding**

### Replica Sets
- Replica set — primary + secondaries + optional arbiters
- Primary — handles all writes
- Secondaries — replicate via oplog, can serve reads
- Arbiter — tie-breaker in elections, holds no data
- Automatic failover — election triggered when primary unreachable
- `rs.status()` — check replica set health
- Oplog — capped collection, size matters for replication lag
- Hidden / Delayed replica — analytics or backup use cases

### Sharding
- Horizontal scaling — distribute data across multiple shards
- Shard key — choosing the right one is critical (cardinality, write distribution, query isolation)
- Hashed sharding — even distribution, no range queries
- Ranged sharding — range queries efficient, risk of hotspots
- Chunks — data is split into chunks, balanced across shards by balancer
- Mongos — query router, client connects to mongos not shard directly
- Config servers — store cluster metadata
- Jumbo chunks — chunks that can't be split, performance problem
- `sh.status()` — check sharding status

---

## 🔒 **9. Security & Administration**

- Authentication — SCRAM (default), X.509 certificates, LDAP
- Authorization — Role-Based Access Control (RBAC)
- Built-in roles — `read`, `readWrite`, `dbAdmin`, `clusterAdmin`, `root`
- Custom roles — fine-grained privileges
- Encryption at rest — WiredTiger encryption, MongoDB Enterprise
- TLS/SSL in transit — `--tlsMode`, certificate setup
- Network access — `bindIp`, firewall rules, Atlas network peering
- Audit logging — track who did what (Enterprise)
- `mongodump` / `mongorestore` — logical backup/restore
- `mongoimport` / `mongoexport` — JSON/CSV import/export
- Atlas Backup — continuous cloud backup, PITR

---

## 🧰 **10. Mongoose (Node.js ODM)**

- Schema — define structure, types, validators, defaults
- Model — compiles schema, maps to collection
- Validators — `required`, `min`, `max`, `enum`, `match`, custom validator functions
- Virtuals — computed properties, not stored in DB
- Middleware (hooks) — `pre` / `post` hooks on `save`, `remove`, `find`, `update`
- Population — `populate()` for reference resolution (like JOIN)
- Lean queries — `.lean()` returns plain JS objects, faster, no Mongoose overhead
- Indexes in schema — `{ index: true }`, `{ unique: true }`, compound indexes
- Schema options — `timestamps: true` (auto `createdAt`, `updatedAt`), `versionKey`
- Transactions with Mongoose — pass session to query options
- `findByIdAndUpdate` — `new: true` to return updated doc, `runValidators: true`
- Aggregation with Mongoose — `Model.aggregate([...])`
- Discriminators — polymorphic models in single collection

---

## 🎓 **11. Capstone Practice**

- Design a schema for an e-commerce product catalog (embed vs reference decision)
- Build an aggregation pipeline for monthly sales report by category
- Implement TTL index for session/token expiry
- Set up a local replica set and observe failover
- Optimize a slow query using explain and the right index
- Implement multi-document transactions for a bank transfer
- Build a full-text search with text index and `$text` operator

---

## Links
- [[Study Plan/PostgreSQL]] — PostgreSQL questions
- [[Study Plan/MySQL]] — MySQL questions
- [[Study Plan.md]] — back to main plan
