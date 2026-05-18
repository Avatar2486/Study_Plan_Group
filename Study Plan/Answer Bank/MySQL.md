# MySQL — Answer Bank

---

**Q: What is the difference between InnoDB and MyISAM?**

**Short:** InnoDB = ACID, row-level locking, foreign keys, crash recovery. MyISAM = no transactions, table-level locking, faster for read-heavy with no writes.

**Detailed:**
| | InnoDB | MyISAM |
|--|--|--|
| Transactions | Yes (ACID) | No |
| Locking | Row-level | Table-level |
| Foreign Keys | Yes | No |
| Crash Recovery | Yes (redo log) | No (can corrupt) |
| Full-Text Search | Yes (MySQL 5.6+) | Yes |
| Use Case | Almost all production workloads | Legacy read-only tables |

InnoDB is the default since MySQL 5.5. MyISAM is rarely used in new projects.

---

**Q: What is a clustered index in InnoDB?**

**Short:** The table itself IS organized by the primary key — rows are physically stored in primary key order. Every InnoDB table has exactly one clustered index.

**Detailed:**
- If you define a PRIMARY KEY, that becomes the clustered index.
- If no PK, InnoDB uses the first UNIQUE NOT NULL column. If none, it creates a hidden 6-byte row ID.
- Secondary indexes store the PRIMARY KEY value (not a physical pointer) — so a secondary index lookup = two lookups (index + PK lookup).
- Wide primary keys = bloated secondary indexes. Keep PK small (INT over UUID when possible).

---

**Q: How do you read the EXPLAIN `type` column?**

**Short:** The `type` column shows how MySQL accesses rows. Best to worst: `const > eq_ref > ref > range > index > ALL`.

**Detailed:**
| Type | Meaning |
|------|---------|
| `const` | At most 1 row — PK or UNIQUE equality lookup |
| `eq_ref` | One row per row from previous table — PK join |
| `ref` | Multiple rows — non-unique index lookup |
| `range` | Index range scan (`BETWEEN`, `>`, `<`, `IN`) |
| `index` | Full index scan (better than ALL but still slow) |
| `ALL` | Full table scan — almost always a problem on large tables |

If you see `ALL` on a large table, add an index. Look at `Extra` column too: `Using filesort` and `Using temporary` are red flags.

---

**Q: What is the difference between gap lock, record lock, and next-key lock?**

**Short:** Record lock = locks a row. Gap lock = locks the space between rows. Next-key lock = record + gap before it (default in InnoDB Repeatable Read).

**Detailed:**
- InnoDB uses next-key locks by default (Repeatable Read) to prevent phantom reads.
- `SELECT * FROM orders WHERE id = 5 FOR UPDATE` → record lock on id=5
- `SELECT * FROM orders WHERE id BETWEEN 5 AND 10 FOR UPDATE` → next-key locks on 5–10 range
- Gap locks prevent INSERT into the locked range — stops phantoms.
- `READ COMMITTED` uses only record locks, no gap locks → fewer deadlocks but allows phantoms.

---

**Q: What is the difference between the three binlog formats?**

**Short:** Statement-based logs the SQL. Row-based logs before/after row images. Mixed uses statement when safe, row otherwise.

**Detailed:**
| Format | What's Logged | Pros | Cons |
|--------|--------------|------|------|
| STATEMENT | SQL query text | Small log size | Non-deterministic functions (NOW(), UUID()) can cause replica divergence |
| ROW | Actual row changes (before/after) | Accurate, safe | Larger logs |
| MIXED | Statement when safe, row otherwise | Balance | Complex to predict |

Modern best practice: ROW format for accuracy. Required for GTID replication and CDC tools like Debezium.

---

**Q: How does GTID replication work?**

**Short:** Global Transaction ID = unique ID per committed transaction across the cluster. Replicas track which GTIDs they've applied — makes failover and re-pointing replicas simple.

**Detailed:**
- Format: `server_uuid:transaction_id` (e.g., `3E11FA47-71CA-11E1-9E33-C80AA9429562:1-23`)
- Every committed transaction gets a GTID written to binlog.
- Replica tracks `gtid_executed` — can connect to any source and say "I have up to X, give me the rest".
- Failover: promote any replica — no need to figure out binlog position. Just point to new primary.
- Enable with `gtid_mode=ON` and `enforce_gtid_consistency=ON`.

---

**Q: What is `ON DUPLICATE KEY UPDATE` and when to use it?**

**Short:** MySQL's upsert — if INSERT violates a unique/PK constraint, UPDATE the existing row instead of failing.

**Detailed:**
```sql
INSERT INTO page_views (page_id, count)
VALUES (1, 1)
ON DUPLICATE KEY UPDATE count = count + 1;

-- Multi-row upsert
INSERT INTO products (id, name, price) VALUES (1, 'Widget', 9.99), (2, 'Gadget', 19.99)
ON DUPLICATE KEY UPDATE price = VALUES(price);  -- VALUES() refers to the inserted value
```
Equivalent to PostgreSQL's `INSERT ... ON CONFLICT DO UPDATE`.

---

**Q: How does MySQL's slow query log work?**

**Short:** Logs queries that take longer than `long_query_time` seconds. Analyze with `mysqldumpslow` or `pt-query-digest`.

**Detailed:**
```sql
-- Enable
SET GLOBAL slow_query_log = 'ON';
SET GLOBAL long_query_time = 1;  -- log queries > 1 second
SET GLOBAL log_queries_not_using_indexes = 'ON';  -- also log full scans

-- Analyze
mysqldumpslow -s t -t 10 /var/log/mysql/slow.log  -- top 10 slowest
```
`pt-query-digest` (Percona Toolkit) gives better analysis — groups similar queries, shows execution counts and average time.

---

**Q: What is a covering index?**

**Short:** An index that contains all columns needed by a query — so MySQL reads only the index, never the table rows (no heap lookup).

**Detailed:**
```sql
-- Query needs: user_id (filter), email (select)
SELECT email FROM users WHERE user_id = 5;

-- Covering index includes both columns
CREATE INDEX idx_covering ON users(user_id, email);
-- EXPLAIN shows: Extra = "Using index" → covered, no table access
```
Check for `Using index` in EXPLAIN `Extra` column. Much faster than `Using index condition` (which still hits the table).

---

**Q: What is `EXPLAIN ANALYZE` in MySQL 8.0.18+?**

**Short:** Shows the actual execution plan with real row counts and timings — not just estimates. Far more useful than plain `EXPLAIN`.

**Detailed:**
```sql
EXPLAIN ANALYZE SELECT * FROM orders WHERE user_id = 5;
-- Output includes:
-- -> Index lookup on orders using idx_user (user_id=5)  (cost=X rows=N) (actual time=X..Y rows=N loops=1)
```
Key things to look for:
- `actual rows` vs `estimated rows` — big mismatch = stale statistics, run `ANALYZE TABLE`
- `actual time` — total time in milliseconds
- `Using filesort` / `Using temporary` in extra info = performance issues

---

**Q: How do you prevent a query from using `Using filesort`?**

**Short:** Add an index that matches both the WHERE filter and the ORDER BY columns in the right order.

**Detailed:**
```sql
-- Slow: filesort
SELECT * FROM orders WHERE user_id = 5 ORDER BY created_at DESC;

-- Fix: composite index on filter + sort columns
CREATE INDEX idx_user_date ON orders(user_id, created_at DESC);
-- Now MySQL uses the index for both filtering AND sorting
```
If you can't avoid filesort, increase `sort_buffer_size`. But the right fix is always the right index.

---

## Links
- [[Study Plan/MySQL]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
