# PostgreSQL

### [https://neon.tech/postgresql/tutorial](https://neon.tech/postgresql/tutorial): Study Queries & Practical

---

## **🔥 1. Core PostgreSQL Concepts**

### **Core Topics**

✅ **What is PostgreSQL? Why is it different from other RDBMS?**

✅ **PostgreSQL Data Types (Numeric, Character, Boolean, Date/Time, JSON, Arrays, hstore, ENUM, UUID, Geometric)**

✅ **PostgreSQL Schema, Tables, and Constraints (Primary Key, Foreign Key, Unique, Check, NOT NULL, DEFAULT)**

✅ **Normalization (1NF, 2NF, 3NF, BCNF, 4NF, 5NF) and Denormalization**

✅ **Views, Materialized Views, and Temporary Tables**

✅ **Stored Procedures, Functions, and Triggers**

### **Practice Questions**

1️⃣ What are **the key differences between PostgreSQL and MySQL?**

2️⃣ How does **PostgreSQL handle composite types and arrays?**

3️⃣ What is **the difference between a View and a Materialized View?**

### **Hands-On Practice**

✔ Create a **PostgreSQL schema with multiple tables using primary and foreign keys**.

✔ Implement **Materialized Views and compare their performance with normal views**.

---

## **🔥 2. PostgreSQL Architecture & Internals**

### **Core Topics**

✅ **PostgreSQL Process Model (Backend Process, Autovacuum, WAL Writer, Checkpointer, Background Writer)**

✅  PostgreSQL Memory Architecture 

✅ **PostgreSQL Storage (Heap Storage, TOAST, Tablespaces, Block Storage)**

✅ **How PostgreSQL Executes Queries (Parsing → Planning → Optimization → Execution)**

✅ How writes and reads happens internally in postgres

✅ **Multi-Version Concurrency Control (MVCC) & Tuple Visibility**

✅ **Write-Ahead Logging (WAL) & Crash Recovery**

### **Practice Questions**

1️⃣ What is **MVCC, and how does PostgreSQL handle concurrent transactions?**

2️⃣ How does **PostgreSQL recover from a system crash using WAL?**

3️⃣ What are **TOAST tables, and when are they used?**

### **Hands-On Practice**

✔ Monitor **PostgreSQL background processes using system tools**.

✔ Observe **how PostgreSQL manages dead tuples using autovacuum**.

---

## **🔥 3. PostgreSQL Indexing & Performance Optimization**

### **Core Topics**

✅ **Types of Indexes (B-Tree, Hash, BRIN, GIN, GiST, SP-GiST)**

✅ **Covering Indexes, Partial Indexes, Expression Indexes, Composite Indexes**

✅ **PostgreSQL EXPLAIN & EXPLAIN ANALYZE for Query Optimization**

✅ **Autovacuum, Analyze, and Reindex (How to Prevent Bloat)**

✅ HOT Tuples

### **Practice Questions**

1️⃣ What is **the difference between B-Tree, GIN, and BRIN indexes?**

2️⃣ How does **PostgreSQL decide the best execution plan for a query?**

3️⃣ What are **Index-Only Scans, and when are they used?**

### **Hands-On Practice**

✔ Optimize **a slow query using different indexing strategies**.

✔ Use **EXPLAIN ANALYZE to understand query execution plans**.

---

## **🔥 4. PostgreSQL Transactions & Concurrency Control**

### **Core Topics**

✅ **ACID Compliance & Transaction Isolation Levels**

✅ **Deadlocks in PostgreSQL (Detection, Prevention, and Resolution)**

✅ **Row-Level Locks, Table Locks, Advisory Locks**

✅ **PostgreSQL Locking Strategies (Optimistic vs Pessimistic Locking)**

✅ **Savepoints & Nested Transactions**

### **Practice Questions**

1️⃣ What is **the difference between Read Committed and Serializable isolation levels?**

2️⃣ How does **PostgreSQL handle deadlocks, and how can you avoid them?**

3️⃣ What is **an Advisory Lock, and when should you use it?**

### **Hands-On Practice**

✔ Simulate **deadlocks and analyze their resolution using pg_stat_activity**.

✔ Implement **Optimistic and Pessimistic Locking in a multi-threaded environment**.

---

## **🔥 5. Query Optimization & Execution Planning**

### **Core Topics**

✅ **Join Algorithms (Nested Loop, Hash Join, Merge Join, Parallel Hash Join)**

✅ **CTEs (Common Table Expressions) vs Subqueries vs Temporary Tables**

✅ **Parallel Query Execution & Parallel Index Scans**

### **Practice Questions**

1️⃣ What is **the difference between Hash Join, Merge Join, and Nested Loop Join?**

2️⃣ How does **PostgreSQL decide the best execution plan for a query?**

### **Hands-On Practice**

✔ Analyze **execution plans of different join types on large datasets**.

---

## **🔥 6. Partitioning & Sharding in PostgreSQL**

### **Core Topics**

✅ **Table Partitioning (Range Partitioning, List Partitioning, Hash Partitioning)**

✅ **Sharding Strategies (PgBouncer, CitusDB, PL/Proxy)**

✅ **PostgreSQL Replication & High Availability (Streaming Replication, Logical Replication)**

### **Practice Questions**

1️⃣ How does **partitioning improve query performance?**

2️⃣ What is **the difference between Partitioning and Sharding?**

### **Hands-On Practice**

✔ Implement **Partitioning on a large dataset and compare performance with non-partitioned tables**.

---

## **🔥 7. PostgreSQL Caching & Performance Tuning**

### **Core Topics**

✅ **PostgreSQL Shared Buffers & Kernel Page Cache**

✅ **PostgreSQL Configuration for High Performance (work_mem, effective_cache_size, maintenance_work_mem)**

✅ **Connection Pooling (PgBouncer vs HikariCP for Connection Management)**

### **Practice Questions**

1️⃣ What is **the role of Shared Buffers in PostgreSQL, and how does it impact performance?**

### **Hands-On Practice**

✔ Optimize **PostgreSQL configuration for high throughput**.

---

## **🔥 8. PostgreSQL JSON & Full-Text Search**

### **Core Topics**

✅ **PostgreSQL JSONB (Storage, Indexing, Querying, Performance Considerations)**

✅ **Full-Text Search using PostgreSQL (tsvector, tsquery, GIN Indexes)**

### **Practice Questions**

1️⃣ What is **the difference between JSON and JSONB in PostgreSQL?**

### **Hands-On Practice**

✔ Implement **Full-Text Search on a large dataset using tsvector and GIN indexes**.

---

## **🔥 9. PostgreSQL High Availability & Scalability**

### **Core Topics**

✅ **Streaming Replication vs Logical Replication**

✅ **Failover & Load Balancing (Patroni, Stolon, Repmgr)**

✅ **Read-Replicas & Write-Write for Scaling Reads in PostgreSQL**

### **Practice Questions**

1️⃣ What is **the difference between Streaming and Logical Replication?**

### **Hands-On Practice**

✔ Set up **a read-replica and test query performance improvements**.

---

## **🔥 Final Steps: FAANG-Level PostgreSQL Mastery**

🚀 **To Crack FAANG Interviews**, focus on:

✅ **Query Optimization & Execution Plans**

✅ **Indexing Strategies & Performance Tuning**

✅ **Concurrency Control & Transactions**

✅ **Partitioning, Sharding, and High Availability**

✅ **Debugging Slow Queries & Performance Bottlenecks**

🔥 **This roadmap covers everything needed for FAANG+ PostgreSQL interviews.**