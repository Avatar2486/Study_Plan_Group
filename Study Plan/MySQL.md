# MySQL

> Reference: [dev.mysql.com/doc](https://dev.mysql.com/doc/) | [mysqltutorial.org](https://www.mysqltutorial.org/)

---

## 🔰 **1. Core Concepts & Data Types**

- What is MySQL? Where is it used vs PostgreSQL?
- MySQL editions — Community, Enterprise; MySQL vs MariaDB differences
- Data types — INT, BIGINT, TINYINT, DECIMAL, FLOAT, DOUBLE
- String types — VARCHAR, CHAR, TEXT, TINYTEXT, MEDIUMTEXT, LONGTEXT, BLOB
- Date/Time types — DATE, TIME, DATETIME, TIMESTAMP, YEAR
- ENUM and SET types — definition, use cases, limitations
- NULL handling — NULL vs empty string, IFNULL, COALESCE, NULLIF
- Schema design — CREATE TABLE, ALTER TABLE, DROP TABLE
- Constraints — PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK (MySQL 8+), NOT NULL, DEFAULT
- AUTO_INCREMENT — behavior, gap on rollback, resetting the counter
- Normalization — 1NF, 2NF, 3NF and when to denormalize for read performance
- Character sets and collations — utf8 vs utf8mb4, case sensitivity in comparisons

---

## 🏗️ **2. Architecture & Internals**

- MySQL architecture — Connection layer, Query cache (removed in 8.0), SQL layer, Storage Engine layer
- Storage engines — InnoDB (default), MyISAM, MEMORY, CSV — differences and use cases
- InnoDB internals — clustered index, buffer pool, doublewrite buffer, redo log
- Clustered index — primary key IS the table in InnoDB, physical row ordering
- Secondary indexes in InnoDB — store primary key value, not the row pointer
- Buffer Pool — how InnoDB caches data and indexes in memory, LRU eviction
- Redo Log (InnoDB) — ensures durability, crash recovery
- Binary Log (binlog) — replication, point-in-time recovery, statement vs row vs mixed format
- `ibdata1` / `.ibd` files — tablespace storage
- Query execution flow — Parser → Preprocessor → Optimizer → Execution Engine → Storage Engine
- MySQL 8.0 changes — removal of query cache, window functions, CTEs, roles

---

## 📑 **3. Indexing**

- B-Tree index — default for most columns, equality + range
- Full-text index — `MATCH ... AGAINST`, MyISAM and InnoDB support
- Spatial index — for geometry/geographic data (GIS)
- Hash index — only in MEMORY engine, exact match only
- Composite index — left-most prefix rule, column order matters
- Covering index — all needed columns in the index, avoids table lookup
- Prefix index — index first N chars of a long string column
- Index cardinality — high cardinality = good index candidate
- EXPLAIN output — `type` column (const, eq_ref, ref, range, index, ALL)
- `type: ALL` — full table scan — the warning sign
- Using index condition pushdown (ICP) — filtering in storage engine layer
- Index Merge — MySQL using multiple indexes for one query
- Invisible indexes (MySQL 8.0+) — test index removal without actually dropping
- ANALYZE TABLE — update index statistics for the optimizer
- `SHOW INDEX FROM table` — inspect index cardinality and structure

---

## 🔄 **4. Transactions & Concurrency (InnoDB)**

- ACID compliance in InnoDB
- BEGIN / START TRANSACTION, COMMIT, ROLLBACK, SAVEPOINT
- Isolation levels — READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ (default), SERIALIZABLE
- Repeatable Read in MySQL — gap locks + next-key locks (prevents phantoms unlike standard SQL)
- Row-level locks — record lock, gap lock, next-key lock
- Table-level locks — LOCK TABLES, MyISAM uses these exclusively
- Intention locks — IX, IS — signal intent before row-level lock
- Deadlocks — InnoDB auto-detection, `SHOW ENGINE INNODB STATUS`
- `innodb_lock_wait_timeout` — how long before lock timeout error
- Optimistic locking — version column pattern
- `SELECT ... FOR UPDATE` — pessimistic exclusive lock
- `SELECT ... FOR SHARE` (MySQL 8+) / `LOCK IN SHARE MODE` — shared lock
- `SKIP LOCKED` and `NOWAIT` (MySQL 8+) — job queue patterns

---

## ⚡ **5. Query Optimization & Performance**

- EXPLAIN — reading output: id, select_type, table, type, possible_keys, key, rows, Extra
- EXPLAIN ANALYZE (MySQL 8.0.18+) — actual execution stats
- `type` column values — const > eq_ref > ref > range > index > ALL (worst)
- `Extra` column warnings — `Using filesort`, `Using temporary` — performance red flags
- Query cache — removed in MySQL 8.0, what replaced it
- Slow query log — `long_query_time`, `log_slow_queries`, `mysqldumpslow`
- JOIN optimization — join order, join buffer, Batched Key Access (BKA)
- Subquery vs JOIN — correlated subquery performance trap
- CTEs (WITH clause) — MySQL 8.0+, recursive CTEs
- Window functions — MySQL 8.0+: RANK, ROW_NUMBER, DENSE_RANK, LAG, LEAD
- GROUP BY optimization — loose index scan, tight index scan
- ORDER BY optimization — using index for sort, filesort fallback
- LIMIT optimization — early row retrieval, OFFSET performance problem at scale
- `SQL_NO_CACHE`, query hints — force/ignore specific indexes
- `innodb_buffer_pool_size` — most important InnoDB config, set to 70–80% of RAM
- Connection pooling — `mysql2` in Node.js with pool settings
- Prepared statements — caching execution plan, preventing SQL injection

---

## 🔀 **6. Replication & High Availability**

- Binary log replication — source/replica architecture, async by default
- Statement-based vs row-based vs mixed replication
- GTID replication (MySQL 5.6+) — global transaction IDs, easier failover
- Replica lag — how it happens, monitoring with `Seconds_Behind_Master`
- Semi-synchronous replication — at least one replica acknowledges before commit
- Group Replication — multi-primary or single-primary, built-in HA
- MySQL Router — connection routing, read/write splitting
- MySQL InnoDB Cluster — Group Replication + MySQL Router + MySQL Shell
- Read replicas — offload SELECT queries, connection routing strategy
- ProxySQL — advanced connection pooler with query routing rules
- `SHOW SLAVE STATUS` / `SHOW REPLICA STATUS` (MySQL 8.0+)

---

## 🗄️ **7. MySQL-Specific Features**

- `ON DUPLICATE KEY UPDATE` — upsert in MySQL
- `INSERT IGNORE` — skip rows that cause duplicate key errors
- `REPLACE INTO` — delete + insert if key conflict
- `LOAD DATA INFILE` — bulk import from CSV file (faster than INSERT loops)
- `mysqldump` — logical backup, restore with `mysql < dump.sql`
- `mysqlpump` — parallel logical backup (MySQL 5.7+)
- XtraBackup (Percona) — hot physical backup for InnoDB without locking
- `SHOW PROCESSLIST` — see active connections and running queries
- `SHOW ENGINE INNODB STATUS` — lock info, deadlocks, buffer pool stats
- `information_schema` — metadata about tables, indexes, columns
- `performance_schema` — query stats, wait events, memory usage
- `sys` schema — human-readable views over performance_schema
- Generated columns (MySQL 5.7+) — VIRTUAL or STORED computed columns
- JSON type (MySQL 5.7+) — JSON functions, `JSON_EXTRACT`, `->` operator, indexing via virtual column
- Common Table Expressions (CTE) — MySQL 8.0+
- Window functions — MySQL 8.0+
- Invisible columns — MySQL 8.0.23+

---

## 🧰 **8. Practical SQL to Know**

- SELECT, INSERT, UPDATE, DELETE
- UPSERT — `INSERT ... ON DUPLICATE KEY UPDATE`
- JOINs — INNER, LEFT, RIGHT, CROSS, SELF
- Find duplicates — `GROUP BY ... HAVING COUNT(*) > 1`
- Delete duplicates — keep one row, delete rest using subquery or self-join
- Second highest salary — `ORDER BY salary DESC LIMIT 1 OFFSET 1` or subquery
- Running total — window function `SUM(amount) OVER (ORDER BY date)`
- Pivot table — using `CASE WHEN` + `GROUP BY` or `PIVOT` equivalent
- String functions — `CONCAT`, `SUBSTRING`, `REPLACE`, `TRIM`, `LENGTH`, `LOCATE`
- Date functions — `NOW()`, `CURDATE()`, `DATEDIFF`, `DATE_FORMAT`, `DATE_ADD`
- NULL functions — `IFNULL`, `COALESCE`, `NULLIF`, `IS NULL`, `IS NOT NULL`

---

## 🎓 **9. Capstone Practice**

- Identify and fix a slow query using EXPLAIN and indexes
- Implement a job queue using `SELECT ... FOR UPDATE SKIP LOCKED`
- Set up a source-replica replication locally
- Build a full-text search on a blog posts table
- Optimize a reporting query using covering indexes and partitioning
- Implement optimistic locking with a `version` column in Node.js

---

## Links
- [[Study Plan/PostgreSQL]] — PostgreSQL questions
- [[Study Plan/MongoDB]] — MongoDB questions
- [[Study Plan.md]] — back to main plan
