# HLD (High Level Design) — Answer Bank

---

**Q: What is the CAP theorem?**

**Short:** A distributed system can guarantee only 2 of 3: Consistency, Availability, Partition Tolerance. Since partition tolerance is unavoidable, you choose between CP or AP.

**Detailed:**
- **Consistency:** Every read gets the most recent write (or an error).
- **Availability:** Every request gets a response (not guaranteed to be the latest).
- **Partition Tolerance:** System continues operating when network partitions occur.
- **CP systems:** PostgreSQL, MongoDB (with w:majority), HBase — may reject requests during partition.
- **AP systems:** Cassandra, DynamoDB, CouchDB — serve possibly stale data during partition.
- Real systems pick a default but often let you tune per operation (e.g., DynamoDB strongly consistent reads).

---

**Q: What is the difference between horizontal and vertical scaling?**

**Short:** Vertical = bigger machine (more CPU/RAM). Horizontal = more machines. Horizontal is preferred for cloud-scale systems.

**Detailed:**
| | Vertical | Horizontal |
|--|--|--|
| How | Upgrade hardware | Add more nodes |
| Limit | Physical hardware ceiling | Nearly unlimited |
| Cost | Expensive jumps | Linear, commodity hardware |
| Downtime | Often requires restart | Rolling update, no downtime |
| Complexity | Low | High (distributed coordination) |

Vertical first (easier) → then horizontal when vertical limit is hit. Design for horizontal from the start if you expect scale.

---

**Q: What is consistent hashing and why is it used?**

**Short:** Maps both data keys and servers onto a virtual ring. Adding/removing a server only remaps a fraction of keys — unlike naive modulo hashing which remaps almost everything.

**Detailed:**
- Each server and each key is hashed to a position on a ring (0 to 2^32).
- A key is assigned to the first server clockwise on the ring.
- Add server: only keys between new server and its predecessor remapped.
- Remove server: only its keys move to the next server.
- Used in: Cassandra, DynamoDB, Redis Cluster, Memcached, CDN routing.
- Virtual nodes: each server gets multiple positions → better distribution.

---

**Q: How do you design a rate limiter?**

**Short:** Use token bucket (smooth bursts) or sliding window counter (precise). Store state in Redis for distributed systems.

**Detailed:**
```
Token Bucket:
- Bucket holds max N tokens. Refills at rate R tokens/second.
- Each request consumes 1 token. Reject if empty.
- Allows short bursts up to N.

Sliding Window Counter:
- Count requests per user in the last 60 seconds.
- Redis: ZADD key timestamp timestamp; ZREMRANGEBYSCORE key 0 (now-60s); ZCARD key

Fixed Window Counter (simplest):
- INCR rate:user:minute — reset every minute.
- Problem: burst at window boundary (2x rate possible).
```
Store in Redis with TTL. For global rate limiting across services, use a central Redis cluster.

---

**Q: How do you design a URL shortener (like bit.ly)?**

**Short:** Hash long URL to short code → store mapping → redirect on lookup. Use Base62 encoding. Cache hot URLs.

**Detailed:**
```
Components:
1. ID Generator — auto-increment or Snowflake ID
2. Base62 encoder — convert ID to ~7 char string (a-zA-Z0-9)
3. DB — store {short_code: long_url, created_at, expiry, user_id}
4. Cache (Redis) — hot short codes → long URLs (LRU, TTL 24h)
5. Redirect service — 301 (permanent, browser caches) or 302 (temp, track every click)

Scale:
- Read-heavy (reads >> writes) — cache aggressively
- DB: read replicas for lookups
- CDN: cache 301 redirects at edge
- Analytics: async click events → Kafka → aggregation pipeline
```

---

**Q: How do you design a notification system?**

**Short:** Producer sends events → message queue → workers route to push/email/SMS channels → delivery services.

**Detailed:**
```
Components:
1. API Service — receives notification requests
2. Message Queue (Kafka/SQS) — decouples production from delivery
3. Notification Workers — consume from queue, fan-out by type
4. Channel services:
   - Push: Firebase FCM / APNs
   - Email: SendGrid / AWS SES
   - SMS: Twilio
5. User Preferences DB — which channels each user wants
6. Retry mechanism — DLQ for failed deliveries

Flow: event → API → Kafka topic → workers → filter by preferences → channel APIs

Scale considerations:
- Rate limiting per channel (FCM: 4000 msg/sec limit)
- Batch notifications for efficiency
- Idempotency: track delivered notification IDs to avoid duplicates
```

---

**Q: How do you scale from 1 million to 100 million users?**

**Short:** Add caching → scale reads with replicas → shard DB → CDN for static → async for heavy operations → partition services.

**Detailed:**
```
1M users:
- Single DB with read replicas
- Redis cache for hot data
- CDN for static assets

10M users:
- DB sharding (horizontal partition)
- Message queues for async processing
- Dedicated cache layer
- Separate services (auth, user, content)

100M users:
- Multi-region deployment
- Global CDN
- Separate read/write paths (CQRS)
- Event-driven architecture (Kafka)
- Database federation (different DBs for different domains)
- Microservices with service mesh
```

---

**Q: What is the Saga pattern for distributed transactions?**

**Short:** Break a distributed transaction into local transactions per service. On failure, execute compensating transactions to undo previous steps.

**Detailed:**
```
Order Saga:
1. Order Service: create order (pending)
2. Payment Service: charge card
3. Inventory Service: reserve items
4. Shipping Service: schedule pickup

If step 3 fails:
- Compensate step 2: refund card
- Compensate step 1: cancel order

Two implementations:
- Choreography: each service emits events, next service listens → decoupled but hard to debug
- Orchestration: central saga orchestrator tells each service what to do → easier to track, central point of failure
```

---

**Q: How do you do back-of-envelope estimation in system design interviews?**

**Short:** Start with users/day → requests/second → storage/day → bandwidth. Use round numbers and communicate assumptions.

**Detailed:**
```
Example: Design Twitter
- 300M users, 50% active daily = 150M DAU
- Each user makes 2 requests/day = 300M requests/day
- 300M / 86400 seconds ≈ 3,500 RPS average, ~10K peak

Storage:
- 500M tweets/day, 280 chars = ~300 bytes each
- Text: 500M × 300B = 150GB/day
- Images (30% tweets, 1MB each): 500M × 0.3 × 1MB = 150TB/day
- 5-year retention: ~274PB (mostly images/video)

Common numbers to know:
- 1 day = 86,400 seconds
- 1 month = 2.5M seconds
- 1KB = 10^3, 1MB = 10^6, 1GB = 10^9, 1TB = 10^12
```

---

## Links
- [[Study Plan/HLD]] — topic list + full question list
- [[Study Plan/Answer Bank/README]] — all answer files
