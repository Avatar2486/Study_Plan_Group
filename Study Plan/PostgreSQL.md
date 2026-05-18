# PostgreSQL

> Reference: [neon.tech/postgresql/tutorial](https://neon.tech/postgresql/tutorial)

---

## 🔰 **1. Core Concepts & Data Types**

- What is PostgreSQL? How is it different from MySQL / other RDBMS?
- PostgreSQL vs MySQL — key differences (ACID, data types, performance)
- Data types — Numeric (INT, BIGINT, NUMERIC, SERIAL), Character (VARCHAR, TEXT), Boolean
- Date/Time types — DATE, TIME, TIMESTAMP, TIMESTAMPTZ, INTERVAL
- Special types — UUID, ARRAY, JSONB, ENUM, hstore, Geometric
- Schema, Tables, Constraints — PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK, NOT NULL, DEFAULT
- Normalization — 1NF, 2NF, 3NF, BCNF and when to denormalize
- Views — creating, updating, dropping
- Materialized Views — vs regular views, REFRESH MATERIALIZED VIEW, CONCURRENTLY
- Temporary Tables — session scope, transaction scope
- Stored Procedures vs Functions — differences, when to use each
- Triggers — BEFORE / AFTER / INSTEAD OF, row-level vs statement-level
- Sequences — SERIAL vs BIGSERIAL vs GENERATED ALWAYS AS IDENTITY

---

## 🏗️ **2. Architecture & Internals**

- PostgreSQL process model — Postmaster, Backend Process, WAL Writer, Checkpointer, Background Writer, Autovacuum
- Memory architecture — Shared Buffers, Work Mem, Maintenance Work Mem, WAL Buffers
- Storage internals — Heap storage, page/block structure, TOAST (large value storage)
- How a query executes — Parsing → Rewriting → Planning → Execution
- MVCC (Multi-Version Concurrency Control) — how it works, tuple versions, xmin/xmax
- Write-Ahead Logging (WAL) — purpose, how it enables crash recovery and replication
- Checkpoints — what they are, how they flush dirty pages
- Dead tuples — why they accumulate, how autovacuum cleans them
- HOT (Heap-Only Tuple) updates — when PostgreSQL avoids index updates
- TOAST — when it kicks in, compression, external storage

---

## 📑 **3. Indexing**

- B-Tree index — default, use cases (equality + range queries)
- Hash index — equality-only, when faster than B-Tree
- GIN index — full-text search, JSONB, arrays (multiple values per row)
- GiST index — geometric data, fuzzy search, range types
- BRIN index — very large tables with physically ordered data (e.g. timestamps)
- SP-GiST index — non-balanced tree structures, IP addresses, phone numbers
- Partial index — index only a subset of rows (`WHERE status = 'active'`)
- Expression / Functional index — index on a function result (`LOWER(email)`)
- Composite (multi-column) index — column order matters, left-most prefix rule
- Covering index — `INCLUDE` columns for index-only scans
- Index-Only Scan — when it happens, visibility map requirement
- EXPLAIN — reading output: Seq Scan, Index Scan, Index Only Scan, Bitmap Scan
- EXPLAIN ANALYZE — actual time vs estimated, actual rows vs planned rows
- Bloated indexes — how they happen, REINDEX, REINDEX CONCURRENTLY
- When NOT to index — low-cardinality columns, small tables

---

## 🔄 **4. Transactions & Concurrency**

- ACID — Atomicity, Consistency, Isolation, Durability
- Transaction basics — BEGIN, COMMIT, ROLLBACK, SAVEPOINT
- Isolation levels — Read Uncommitted, Read Committed (default), Repeatable Read, Serializable
- Dirty read, Non-repeatable read, Phantom read — which level prevents which
- Row-level locks — FOR UPDATE, FOR SHARE, FOR NO KEY UPDATE, FOR KEY SHARE
- Table-level locks — ACCESS SHARE, ROW EXCLUSIVE, ACCESS EXCLUSIVE
- Advisory locks — application-level locking with `pg_advisory_lock`
- Deadlocks — how they happen, PostgreSQL auto-detection, error message, prevention
- Optimistic locking — version column pattern, no database lock
- Pessimistic locking — SELECT FOR UPDATE, use cases
- SKIP LOCKED — queue/job processing pattern
- `pg_stat_activity` — monitoring active connections and locks

---

## ⚡ **5. Query Optimization & Performance**

- EXPLAIN vs EXPLAIN ANALYZE vs EXPLAIN (BUFFERS)
- Sequential Scan vs Index Scan — when each is chosen
- Join types — Nested Loop, Hash Join, Merge Join — when PostgreSQL picks each
- CTEs (WITH clause) — optimization fence (pre-PG12), inlining (PG12+), RECURSIVE CTEs
- Subqueries vs JOINs vs CTEs — performance tradeoffs
- Window functions — RANK, ROW_NUMBER, DENSE_RANK, LAG, LEAD, SUM OVER, PARTITION BY
- Aggregation — GROUP BY, HAVING, DISTINCT, DISTINCT ON
- Pagination — LIMIT/OFFSET problems at scale, keyset pagination alternative
- Statistics — pg_stats, ANALYZE, how the planner uses statistics
- Vacuum — VACUUM vs VACUUM FULL vs AUTOVACUUM — differences and when to use
- N+1 query problem — how to identify and fix
- Avoiding full table scans — conditions that break index usage (functions on columns, implicit casts)
- Connection pooling — why needed, PgBouncer (session vs transaction mode), `pg.Pool` in Node.js
- `work_mem`, `shared_buffers`, `effective_cache_size` — what they do, how to tune

---

## 🔀 **6. Partitioning & Sharding**

- Table partitioning — why use it, when it helps
- Range partitioning — `PARTITION BY RANGE (created_at)` — good for time-series data
- List partitioning — `PARTITION BY LIST (region)` — good for category/country splits
- Hash partitioning — `PARTITION BY HASH (user_id)` — even distribution
- Partition pruning — how PostgreSQL skips irrelevant partitions at query time
- Partition indexes — local vs global indexes
- Partitioning vs Sharding — differences, use cases
- Sharding strategies — PgBouncer, CitusDB for horizontal scaling
- Foreign Data Wrappers (FDW) — querying external databases from PostgreSQL

---

## 🔁 **7. Replication & High Availability**

- Streaming Replication — WAL-based, physical copy, same major version required
- Logical Replication — row-level changes, selective tables, cross-version support
- Replication slots — prevent WAL deletion before replica consumes
- Read replicas — offloading read queries, connection routing
- Synchronous vs asynchronous replication — tradeoff between safety and performance
- Failover — Patroni, repmgr, Stolon — automatic promotion
- Point-in-Time Recovery (PITR) — WAL archiving to restore DB to any past moment
- pg_basebackup — taking a base backup for standby setup

---

## 🔍 **8. JSONB & Full-Text Search**

- JSON vs JSONB — storage differences, performance, indexing support
- JSONB operators — `->`, `->>`, `#>`, `@>` (containment), `?` (key exists)
- JSONB indexing — GIN index, `jsonb_path_ops` for containment queries
- Querying nested JSONB — `jsonb_array_elements`, `jsonb_each`
- Full-Text Search — `tsvector`, `tsquery`, `to_tsvector`, `to_tsquery`
- Full-text ranking — `ts_rank`, `ts_rank_cd`
- Full-text GIN index — fast text search on large tables
- `pg_trgm` — trigram-based fuzzy search (`LIKE '%keyword%'` with index)

---

## 🧰 **9. Practical SQL to Know**

- SELECT, INSERT, UPDATE, DELETE, UPSERT (`ON CONFLICT DO UPDATE`)
- JOINs — INNER, LEFT, RIGHT, FULL OUTER, CROSS, SELF JOIN
- Second highest value — `ORDER BY DESC LIMIT 1 OFFSET 1` or subquery
- Find duplicates — `GROUP BY ... HAVING COUNT(*) > 1`
- DELETE vs TRUNCATE vs DROP — differences (rollback, triggers, speed)
- Recursive CTEs — tree traversal (org charts, categories)
- Lateral joins — `JOIN LATERAL` — correlated subquery as a join
- COPY command — bulk import/export CSV to/from table
- `pg_dump` / `pg_restore` — backup and restore
- `pg_stat_user_tables` — dead tuples, sequential scans, index usage stats

---

## 🎓 **10. Capstone Practice**

- Optimize a slow query — identify with EXPLAIN ANALYZE, add correct index
- Build a partitioned table for 100M+ rows time-series data
- Implement full-text search on a products table using tsvector + GIN
- Set up streaming replication and a read replica locally
- Simulate a deadlock and observe PostgreSQL's auto-resolution
- Build a JSONB-backed flexible product attributes system
- Implement keyset pagination on a large table

---

## Links
- [[Study Plan/MySQL]] — MySQL questions
- [[Study Plan/MongoDB]] — MongoDB questions
- [[Study Plan.md]] — back to main plan
