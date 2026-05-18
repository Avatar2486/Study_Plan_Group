# PostgreSQL — Answer Bank

---

**Q: What is MVCC and how does it work in PostgreSQL?**

**Short:** Multi-Version Concurrency Control keeps multiple row versions so readers never block writers. Each transaction sees a snapshot of the DB at its start time.

**Detailed:**
- Every row has `xmin` (transaction that inserted it) and `xmax` (transaction that deleted/updated it).
- UPDATE = insert a new row version + mark old one as expired. No lock needed for reads.
- Old versions accumulate as dead tuples → autovacuum cleans them.
- This is why PostgreSQL rarely has read/write contention — readers work on their snapshot.

---

**Q: What is WAL and why is it important?**

**Short:** Write-Ahead Log — every change is written to the log BEFORE modifying the actual data file. Guarantees crash recovery and enables replication.

**Detailed:**
- On crash: PostgreSQL replays WAL from the last checkpoint to restore consistency.
- Replication: primary ships WAL bytes to standby servers (streaming replication).
- WAL archiving = store WAL files offsite = point-in-time recovery (PITR).
- `pg_wal/` directory contains WAL segments. Size controlled by `max_wal_size`.

---

**Q: What are the different index types in PostgreSQL?**

**Short:** B-Tree (default), Hash, GIN (arrays/JSONB), GiST (geometry/fuzzy), BRIN (large ordered tables), SP-GiST, Partial, Expression.

**Detailed:**
| Index | Best For |
|-------|---------|
| **B-Tree** | Default. Equality + range (`=`, `<`, `>`, `BETWEEN`, `LIKE 'abc%'`) |
| **Hash** | Only equality (`=`). Slightly faster than B-Tree for pure equality lookups |
| **GIN** | Full-text search, JSONB `@>`, arrays `@>` — multiple values per row |
| **GiST** | Geometry, range types, fuzzy search (`pg_trgm`) |
| **BRIN** | Very large append-only tables where data is physically ordered (e.g., logs by timestamp) — tiny index |
| **Partial** | `CREATE INDEX idx ON users(email) WHERE status='active'` — smaller, faster |

---

**Q: How do you read EXPLAIN ANALYZE output?**

**Short:** Look at scan type (Seq vs Index), estimated vs actual rows, and total time. Seq Scan on large tables = problem.

**Detailed:**
```sql
EXPLAIN ANALYZE SELECT * FROM orders WHERE user_id = 5;
```
- `Seq Scan` on large table → needs an index
- `Index Scan` → using index but fetching heap rows
- `Index Only Scan` → best — reads only the index, no heap
- `cost=X..Y` → X = startup cost, Y = total estimated cost
- `actual time=X..Y rows=N` → real numbers; if `rows` estimate vs actual differ a lot → run `ANALYZE`
- `Buffers: hit=N` → N pages read from shared_buffers (cache); `read=N` → disk reads

---

**Q: What are PostgreSQL transaction isolation levels?**

**Short:** Read Committed (default), Repeatable Read, Serializable. Each prevents more anomalies but adds more locking overhead.

**Detailed:**
| Level | Dirty Read | Non-Repeatable Read | Phantom Read |
|-------|-----------|--------------------|----|
| Read Committed (default) | No | Yes | Yes |
| Repeatable Read | No | No | No (in PG) |
| Serializable | No | No | No |

- **Read Committed:** Each statement sees a fresh snapshot. Safe for most apps.
- **Repeatable Read:** Whole transaction sees the same snapshot — good for reports.
- **Serializable:** Full isolation — transactions run as if sequential. Slowest.

---

**Q: How do deadlocks happen and how does PostgreSQL handle them?**

**Short:** Two transactions each wait for the other's lock. PostgreSQL detects the cycle and aborts one automatically with `ERROR: deadlock detected`.

**Detailed:**
```
T1 locks row A, wants row B
T2 locks row B, wants row A → deadlock
```
- PostgreSQL runs a deadlock detection background check.
- Prevention: always acquire locks in the same order across transactions. Keep transactions short.
- `SELECT ... FOR UPDATE SKIP LOCKED` — skip already-locked rows (job queue pattern).
- Monitor with `SELECT * FROM pg_stat_activity WHERE wait_event_type = 'Lock'`.

---

**Q: What is the difference between JSON and JSONB in PostgreSQL?**

**Short:** JSON stores plain text (preserves whitespace/key order). JSONB stores binary — faster reads, supports indexing, no duplicates.

**Detailed:**
```sql
-- JSONB: indexable with GIN
CREATE INDEX idx ON products USING GIN (attributes);
SELECT * FROM products WHERE attributes @> '{"color": "red"}';

-- Operators
data->>'name'          -- text value of key
data->'address'        -- JSON value of key
data @> '{"key":"val"}'  -- containment check (needs GIN index)
data ? 'key'           -- key exists
```
Always use JSONB unless you need to preserve exact text format. JSON is mainly for write-once data.

---

**Q: What is the difference between Streaming Replication and Logical Replication?**

**Short:** Streaming copies raw WAL bytes (full DB, physical). Logical decodes row-level changes (selective tables, cross-version).

**Detailed:**
| | Streaming | Logical |
|--|--|--|
| What's copied | Raw WAL (binary) | Decoded INSERT/UPDATE/DELETE |
| Granularity | Whole cluster | Per-table selection |
| Cross-version | Same major version | Works across versions |
| Use case | Read replicas, HA | CDC, migration, selective sync |

---

**Q: When should you use table partitioning?**

**Short:** When a table has 10M+ rows and queries always filter on the same column (date, region) — partitioning lets PostgreSQL skip irrelevant partitions.

**Detailed:**
```sql
-- Range partitioning by month
CREATE TABLE events (id INT, created_at TIMESTAMPTZ) PARTITION BY RANGE (created_at);
CREATE TABLE events_2024_01 PARTITION OF events FOR VALUES FROM ('2024-01-01') TO ('2024-02-01');

-- Query only scans the relevant partition
SELECT * FROM events WHERE created_at > '2024-01-01'; -- partition pruning kicks in
```
Types: Range (dates, numeric ranges), List (categories, regions), Hash (even distribution).

---

**Q: What is the difference between DELETE, TRUNCATE, and DROP?**

**Short:** DELETE removes rows (filterable, triggers fire). TRUNCATE removes all rows fast (no triggers). DROP removes the table entirely.

**Detailed:**
| | DELETE | TRUNCATE | DROP |
|--|--|--|--|
| WHERE filter | Yes | No | No |
| Triggers fire | Yes | No (by default) | No |
| Rollback | Yes | Yes (in transaction) | Yes (in transaction) |
| Resets sequences | No | Yes (with RESTART IDENTITY) | N/A |
| Speed | Slow (row-by-row) | Fast | Instant |

---

**Q: What are Window Functions and give an example?**

**Short:** Compute aggregates across related rows without collapsing them into one row — unlike GROUP BY.

**Detailed:**
```sql
-- Rank employees by salary within each department
SELECT
  name,
  department,
  salary,
  RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank,
  SUM(salary) OVER (PARTITION BY department) AS dept_total,
  LAG(salary) OVER (ORDER BY salary) AS prev_salary
FROM employees;
```
Common functions: `RANK()`, `ROW_NUMBER()`, `DENSE_RANK()`, `LAG()`, `LEAD()`, `SUM() OVER()`, `AVG() OVER()`, `FIRST_VALUE()`.

---

**Q: How do you optimize a slow PostgreSQL query?**

**Short:** Run `EXPLAIN ANALYZE` → find Seq Scans → add index → check statistics → rewrite query.

**Detailed:**
1. `EXPLAIN ANALYZE <query>` — identify bottleneck (Seq Scan on large table, large rows estimate)
2. Check if index exists: if not, create the right type (B-Tree for range, GIN for JSONB)
3. Run `ANALYZE tablename` if estimates are wrong (stale statistics)
4. Avoid functions on indexed columns in WHERE: `WHERE LOWER(email) = 'x'` → create functional index
5. Fix N+1: replace loop queries with JOINs or CTEs
6. For repeated expensive queries: Materialized View or Redis cache

---

## Links
- [[Study Plan/PostgreSQL]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
