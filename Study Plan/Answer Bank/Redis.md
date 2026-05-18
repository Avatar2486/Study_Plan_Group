# Redis — Answer Bank

---

**Q: What is Redis and how is it different from Memcached?**

**Short:** Redis is an in-memory data structure store supporting complex types, persistence, pub/sub, and scripting. Memcached is simpler — only strings, no persistence.

**Detailed:**
| | Redis | Memcached |
|--|--|--|
| Data types | String, List, Set, SortedSet, Hash, Stream, HyperLogLog | String only |
| Persistence | RDB + AOF | No |
| Replication | Yes | No |
| Pub/Sub | Yes | No |
| Lua scripting | Yes | No |
| Cluster/HA | Sentinel + Cluster | Basic (consistent hashing) |
| Use case | Caching + much more | Simple key-value cache |

---

**Q: What are Redis data structures and their use cases?**

**Short:** String (cache, counters), List (queues), Set (unique tags), Sorted Set (leaderboards), Hash (user sessions), Stream (event log), HyperLogLog (unique count approximation).

**Detailed:**
| Type | Commands | Use Case |
|------|---------|---------|
| String | SET, GET, INCR, EXPIRE | Cache, counters, rate limiting |
| List | LPUSH, RPOP, LRANGE | Task queue, recent items, activity feed |
| Set | SADD, SMEMBERS, SINTER | Tags, unique users, followers |
| Sorted Set | ZADD, ZRANGE, ZRANK | Leaderboards, time-series, priority queue |
| Hash | HSET, HGET, HGETALL | User sessions, object storage |
| Stream | XADD, XREAD, XGROUP | Event sourcing, message queue with consumer groups |
| HyperLogLog | PFADD, PFCOUNT | Count unique visitors (approximate, <1% error, 12KB memory) |

---

**Q: What is the difference between RDB and AOF persistence?**

**Short:** RDB = periodic snapshot to disk (fast recovery, some data loss). AOF = log every write command (minimal data loss, larger file, slower recovery).

**Detailed:**
| | RDB | AOF |
|--|--|--|
| What's saved | Binary snapshot | Log of every write command |
| Data loss risk | Since last snapshot (minutes) | At most 1 second (with `appendfsync everysec`) |
| Recovery speed | Fast | Slow (replays all commands) |
| File size | Compact | Grows large (AOF rewrite compacts it) |
| Performance impact | Periodic fork | Slight write overhead |

Best practice: enable BOTH. RDB for fast restarts, AOF for minimal data loss. `appendfsync everysec` is the best balance.

---

**Q: How do Redis transactions work (MULTI/EXEC/WATCH)?**

**Short:** MULTI queues commands, EXEC runs them atomically. WATCH implements optimistic locking — EXEC fails if watched key changed.

**Detailed:**
```redis
MULTI
INCR counter
SET last_updated "2024-01-01"
EXEC   -- runs both atomically, no other client can interleave

-- Optimistic locking with WATCH
WATCH balance
MULTI
DECRBY balance 100
EXEC  -- returns nil if balance was modified between WATCH and EXEC → retry
```
Unlike SQL, Redis transactions don't rollback on command errors — other commands still execute. Use Lua scripts for true atomicity with logic.

---

**Q: What are Redis eviction policies?**

**Short:** When memory is full, Redis evicts keys based on the policy. `allkeys-lru` is most common for pure cache use cases.

**Detailed:**
| Policy | Behavior |
|--------|---------|
| `noeviction` | Return error when memory full (default) |
| `allkeys-lru` | Evict least recently used key from ALL keys |
| `volatile-lru` | Evict LRU key from keys WITH expiry |
| `allkeys-lfu` | Evict least frequently used from ALL keys |
| `volatile-lfu` | Evict LFU from keys with expiry |
| `allkeys-random` | Evict random key from ALL |
| `volatile-random` | Evict random from keys with expiry |
| `volatile-ttl` | Evict key with soonest expiry |

Set with `maxmemory-policy allkeys-lru` in redis.conf. Set `maxmemory 2gb` to cap usage.

---

**Q: What are caching strategies? Cache-Aside vs Write-Through?**

**Short:** Cache-Aside = app manages cache (most common). Write-Through = every write goes to cache + DB simultaneously.

**Detailed:**
| Strategy | Flow | Pro | Con |
|----------|------|-----|-----|
| **Cache-Aside** | Miss → load DB → store in cache | Simple, flexible | Cache can be stale |
| **Write-Through** | Write → cache + DB together | Always fresh | Write latency |
| **Write-Behind** | Write → cache first, async to DB | Fast writes | Risk of data loss |
| **Read-Through** | Cache handles DB loading | Transparent to app | Cold start miss |

Cache-Aside pattern:
```javascript
const cached = await redis.get(key);
if (cached) return JSON.parse(cached);
const data = await db.query(...);
await redis.set(key, JSON.stringify(data), 'EX', 300); // 5 min TTL
return data;
```

---

**Q: What is a cache stampede and how do you prevent it?**

**Short:** When a popular cached key expires, many requests simultaneously hit the DB. Prevention: locking, probabilistic early expiry, or background refresh.

**Detailed:**
```javascript
// Prevention: distributed lock (only one request refreshes)
const lock = await redis.set('lock:key', '1', 'NX', 'EX', 10);
if (lock) {
  const data = await db.query(...);
  await redis.set(key, JSON.stringify(data), 'EX', 300);
  await redis.del('lock:key');
} else {
  // wait briefly and retry
  await sleep(100);
  return await redis.get(key);
}
```
Other approaches: `GETEX` with extended TTL on every read (lazy expiry), background cron that refreshes before expiry, or staggered TTLs.

---

**Q: What is the difference between Redis Pub/Sub and Redis Streams?**

**Short:** Pub/Sub is fire-and-forget (no persistence, missed if offline). Streams persist messages with consumer groups, ACK, and replay capability.

**Detailed:**
| | Pub/Sub | Streams |
|--|--|--|
| Persistence | No | Yes |
| Message history | No | Yes (queryable) |
| Consumer groups | No | Yes |
| ACK | No | Yes |
| Missed messages | Lost | Can replay |
| Use case | Real-time broadcast, chat | Event log, reliable queue, CDC |

Use Pub/Sub for real-time notifications where losing a message is OK. Use Streams where you need guaranteed delivery.

---

**Q: What is the difference between Redis Sentinel and Redis Cluster?**

**Short:** Sentinel = HA for a single Redis instance (automatic failover). Cluster = horizontal sharding across multiple nodes.

**Detailed:**
| | Sentinel | Cluster |
|--|--|--|
| Purpose | High availability | Sharding + HA |
| Nodes | 1 master + replicas + 3+ sentinels | 3+ master shards, each with replicas |
| Data | Full dataset on each node | Data split across shards |
| Max data | RAM of one node | Sum of all shards |
| Complexity | Simple | Higher |
| Use when | HA needed, dataset fits one node | Dataset > one node's RAM |

---

**Q: When should you use Lua scripts in Redis?**

**Short:** When you need atomic read-modify-write logic that spans multiple commands — Lua scripts run atomically on the server without another client interrupting.

**Detailed:**
```lua
-- Atomic decrement only if value > 0 (inventory check + decrement)
local stock = redis.call('GET', KEYS[1])
if tonumber(stock) > 0 then
  return redis.call('DECR', KEYS[1])
else
  return -1
end
```
```javascript
const script = `
  local stock = redis.call('GET', KEYS[1])
  if tonumber(stock) > 0 then return redis.call('DECR', KEYS[1]) else return -1 end
`;
const result = await redis.eval(script, 1, 'product:123:stock');
```
Lua scripts execute atomically — no other commands run during execution. Better than MULTI/EXEC for conditional logic.

---

## Links
- [[Study Plan/Redis]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
