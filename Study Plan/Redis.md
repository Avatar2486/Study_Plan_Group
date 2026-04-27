# Redis

---

## **🔥 1. Core Redis Concepts**

### **Core Topics**

✅ **What is Redis? Why is it different from traditional databases?**

✅ **Key-Value Store Basics, SET, SETEX, EX, GET, MGET, MSET, SETNX, PX**

✅ **How Redis Handles Data in Memory, KeySpaces in redis** 

✅ **Redis vs Memcached vs PostgreSQL Caching**

✅ **Common Use Cases (Caching, Leaderboards, Pub/Sub, Session Management, Rate Limiting, Distributed Locks)**

### **Practice Questions**

1️⃣ What are **the differences between Redis and Memcached?**

2️⃣ How does **Redis achieve high throughput and low latency?**

3️⃣ When should you **not use Redis?**

### **Hands-On Practice**

✔ Install **Redis locally and run basic commands (SET, GET, DEL, EXISTS, EXPIRE, TTL, PERSIST).**

✔ Implement **a caching mechanism for an API using Redis.**

---

## **🔥 2. Redis Data Structures & Real-World Usage**

### **Core Topics**

✅ **Strings (Atomic Counters, Caching, Rate Limiting)**

✅ **Lists (Task Queues, Recent Items, Time-Based Storage)**

✅ **Sets & Sorted Sets (Leaderboards, Unique Elements, Expiring Items)**

✅ **Hashes (User Sessions, Object Storage)**

✅ **Bitmaps & HyperLogLogs (Bitwise Operations, Unique Counting, Approximate Counting)**

✅ **Streams (Event Processing, Message Queues)**

### **Practice Questions**

1️⃣ When should you use **a Sorted Set over a List?**

2️⃣ How does **Redis HyperLogLog work, and why is it useful?**

3️⃣ What is **the difference between a Redis List and a Redis Stream?**

### **Hands-On Practice**

✔ Implement **a leaderboard system using Sorted Sets.**

✔ Use **Redis Bitmaps for tracking user login days in a month.**

---

## **🔥 3. Redis Persistence & Durability**

### **Core Topics**

✅ **Redis RDB (Snapshot Persistence) vs AOF (Append-Only File)**

✅ **Redis Data Persistence Trade-offs (Performance vs Durability)**

✅ **Configuring Redis Persistence for High Availability**

✅ **How to Restore Redis from Snapshots**

### **Practice Questions**

1️⃣ What is **the difference between RDB and AOF?**

2️⃣ How does **Redis ensure durability after a crash?**

3️⃣ What are **the pros and cons of using only AOF mode?**

### **Hands-On Practice**

✔ Configure **Redis to use both RDB and AOF, then simulate a failure and restore data.**

✔ Tune **AOF rewrite settings to improve performance.**

---

## **🔥 4. Redis Transactions & Lua Scripting**

### **Core Topics**

✅ **How Redis Transactions Work (MULTI, EXEC, DISCARD, WATCH)**

✅ **Optimistic Locking with WATCH**

✅ **Atomicity & Isolation in Redis Transactions**

✅ **Redis Lua Scripting (Why It’s Used and How It Works)**

### **Practice Questions**

1️⃣ What is **the difference between Redis Transactions and Database Transactions?**

2️⃣ How does **WATCH help implement optimistic concurrency control?**

3️⃣ When should you **use Lua scripts in Redis?**

### **Hands-On Practice**

✔ Implement **a transactional banking system using Redis Transactions.**

✔ Write **a Lua script to atomically decrement stock in an e-commerce inventory system.**

---

## **🔥 5. Redis Expiry, TTL, and Eviction Policies**

### **Core Topics**

✅ **How Expiry Works in Redis (EX, PX, TTL, PERSIST)**

✅ **Redis Eviction Policies (volatile-lru, allkeys-lru, volatile-random, allkeys-random, noeviction, etc.)**

✅ **Memory Management in Redis**

### **Practice Questions**

1️⃣ What happens **when Redis runs out of memory?**

2️⃣ How do **you ensure that time-sensitive cache entries expire efficiently?**

### **Hands-On Practice**

✔ Set **different TTLs for cached data and analyze Redis behavior.**

✔ Experiment **with different eviction policies using maxmemory settings.**

---

## **🔥 6. Redis Replication & High Availability**

### **Core Topics**

✅ **Redis Master-Slave Replication**

✅ **Read-Scaling Using Replicas**

✅ **Failover Handling in Redis**

✅ **Redis Sentinel (Automatic Failover & Monitoring)**

✅ **Redis Cluster (Partitioning & High Availability)**

### **Practice Questions**

1️⃣ What is **the difference between Master-Slave Replication and Redis Cluster?**

2️⃣ How does **Redis Sentinel work for automatic failover?**

3️⃣ What are **the trade-offs of running Redis in cluster mode?**

### **Hands-On Practice**

✔ Set up **Redis replication and test read-scaling.**

✔ Configure **Redis Sentinel for automatic failover.**

---

## **🔥 7. Redis Caching Strategies & Performance Optimization**

### **Core Topics**

✅ **Cache-Aside vs Write-Through vs Write-Behind vs Read-Through Caching**

✅ **Reducing Cache Stampede (Lazy Loading, Request Coalescing, Leaky Bucket)**

✅ **Redis Search (SCAN)**

✅ **Redis Connection Pooling & Threading Model**

✅ **Redis Distributed Locks**

### **Practice Questions**

1️⃣ What is **the difference between Cache-Aside and Write-Through caching?**

2️⃣ How do **you prevent cache stampede in Redis?**

3️⃣ How does **Redis handle concurrent requests internally?**

### **Hands-On Practice**

✔ Implement **Cache-Aside strategy for a database-driven API.**

✔ Use **Redis pipelines to reduce network round-trips.**

---

## **🔥 8. Redis Pub/Sub & Streaming**

### **Core Topics**

✅ **Redis Pub/Sub Model (Real-Time Messaging, Broadcasting, Chat Apps)**

✅ **Redis Streams (Event Sourcing, Log Processing, Data Pipelines)**

✅ **Message Durability & Consumer Groups**

### **Practice Questions**

1️⃣ How does **Redis Pub/Sub compare to Kafka?**

2️⃣ What are **Consumer Groups in Redis Streams?**

3️⃣ How does **Redis handle message persistence in Streams?**

### **Hands-On Practice**

✔ Implement **a real-time chat application using Redis Pub/Sub.**

✔ Use **Redis Streams to process log events.**

---

## **🔥 9. Redis Security & Debugging**

### **Core Topics**

✅ **Redis Authentication & Role-Based Access Control (ACL)**

✅ **Encrypting Redis Traffic with TLS**

✅ **Preventing Unauthorized Access & Common Security Risks**

✅ **Monitoring Redis Performance (Slow Log, Latency Monitoring, Keyspace Analysis)**

### **Practice Questions**

1️⃣ How do **you secure Redis from unauthorized access?**

2️⃣ What is **the purpose of Redis Slow Log?**

### **Hands-On Practice**

✔ Secure **Redis with authentication & ACLs.**

✔ Analyze **Redis performance using Slow Log & MONITOR.**

---

## **🔥 Final Steps: FAANG-Level Redis Mastery**

🚀 **To Crack FAANG Interviews**, focus on:

✅ **Redis Internals (Data Structures, Persistence, Transactions)**

✅ **Caching Strategies & Expiry Policies**

✅ **Scaling Redis (Replication, Clustering, High Availability)**

✅ **Redis Performance Tuning & Debugging**

✅ **Pub/Sub & Streams for Real-Time Data Processing**