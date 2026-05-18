# Kafka — Answer Bank

---

**Q: What is Kafka's architecture? Explain brokers, topics, partitions, consumer groups.**

**Short:** Brokers store data. Topics are categories. Partitions are ordered logs within a topic. Consumer groups enable parallel consumption.

**Detailed:**
- **Broker:** A Kafka server. A cluster has multiple brokers for fault tolerance.
- **Topic:** Named stream of records (like a table). Append-only log.
- **Partition:** A topic is split into N partitions. Each partition is an ordered, immutable sequence. More partitions = more parallelism.
- **Consumer Group:** Multiple consumers sharing a topic — each partition is assigned to exactly one consumer in the group. 3 partitions = max 3 consumers run in parallel.
- **Offset:** Each message has an offset (position) within its partition. Consumers track which offset they've processed.

---

**Q: What is ISR (In-Sync Replicas)?**

**Short:** The set of replicas that are fully caught up with the leader. Only ISR members can be elected as the new leader on failure.

**Detailed:**
- Each partition has 1 leader + N-1 followers.
- Followers continuously fetch from the leader. If a follower falls behind (> `replica.lag.time.max.ms`), it's removed from ISR.
- `acks=all` → producer waits for ALL ISR members to acknowledge. Safe but slower.
- `min.insync.replicas=2` → require at least 2 ISR before accepting writes. Prevents data loss on single broker failure.

---

**Q: What is the difference between acks=0, acks=1, acks=all?**

**Short:** `acks=0` = fire and forget. `acks=1` = leader acknowledged. `acks=all` = all ISR acknowledged. Trade-off: latency vs durability.

**Detailed:**
| Setting | Durability | Latency | When to Use |
|---------|-----------|---------|-------------|
| `acks=0` | None (may lose data) | Lowest | Metrics, logs where loss is OK |
| `acks=1` | Leader only (loses data if leader fails before replicating) | Medium | General use |
| `acks=all` | All ISR | Highest | Financial, critical data |

For guaranteed delivery: `acks=all` + `min.insync.replicas=2` + `enable.idempotence=true`.

---

**Q: What is exactly-once semantics (EOS) in Kafka?**

**Short:** Each message is processed exactly once — no duplicates, no loss. Achieved via idempotent producer + transactions.

**Detailed:**
- **At-most-once:** Producer sends without retry → may lose messages.
- **At-least-once:** Producer retries on failure → may duplicate.
- **Exactly-once:** Idempotent producer (assigns sequence numbers, broker deduplicates) + transactional API (atomic write across partitions + consumer offset commit).

```javascript
// Transactional producer
producer.initTransactions();
producer.beginTransaction();
producer.send(record1);
producer.send(record2);
producer.sendOffsetsToTransaction(offsets, groupId);
producer.commitTransaction(); // all or nothing
```

---

**Q: How does consumer rebalancing work?**

**Short:** When a consumer joins or leaves a group, Kafka pauses all consumers, redistributes partitions, then resumes. This is a rebalance.

**Detailed:**
- Triggered by: consumer joining, consumer leaving, consumer missing heartbeat, partition count change.
- During rebalance: ALL consumers in the group stop processing (stop-the-world).
- **Cooperative Sticky Rebalancing** (Kafka 2.4+): incremental rebalance — only reassigned partitions stop, others continue. Reduces downtime significantly.
- `session.timeout.ms` and `heartbeat.interval.ms` control how quickly a dead consumer is detected.
- `max.poll.interval.ms` — if consumer doesn't poll within this time → kicked out → rebalance.

---

**Q: What is the difference between auto-commit and manual offset commit?**

**Short:** Auto-commit is easy but can cause duplicate processing or data loss. Manual commit gives you control — commit after successful processing.

**Detailed:**
```javascript
// Auto-commit (default) — commits every 5 seconds
// Problem: if app crashes after processing but before commit → reprocessed on restart
// OR: commits before processing completes → message "lost"

// Manual commit — commit AFTER successful processing
consumer.on('message', async (msg) => {
  await processMessage(msg);
  consumer.commitOffset(msg); // only commit after processing succeeds
});
```
For exactly-once: commit offset as part of the same database transaction as the business operation.

---

**Q: How is Kafka different from RabbitMQ?**

**Short:** Kafka is a distributed log (messages retained, replayable, pull-based). RabbitMQ is a message broker (messages deleted after consume, push-based, routing).

**Detailed:**
| | Kafka | RabbitMQ |
|--|--|--|
| Model | Distributed commit log | Message broker |
| Message retention | Configurable (days/weeks) | Deleted after ACK |
| Replay | Yes — consumers control offset | No |
| Consumption | Pull (consumer fetches) | Push (broker pushes) |
| Ordering | Per-partition | Per-queue |
| Throughput | Millions/sec | ~50K/sec |
| Use case | Event streaming, CDC, audit log | Task queues, routing, RPC |

---

**Q: What is Kafka's zero-copy mechanism?**

**Short:** Kafka uses the OS `sendfile()` syscall to transfer data from disk directly to the network socket, bypassing the user space — dramatically reducing CPU and memory usage.

**Detailed:**
- Normal path: disk → kernel buffer → user space → socket buffer → network (4 copies, 2 context switches)
- Zero-copy: disk → kernel buffer → socket buffer → network (2 copies, 0 context switches)
- This is why Kafka can handle high throughput (hundreds of MB/s) with minimal CPU.
- Combined with sequential disk I/O and batching, Kafka is extremely I/O efficient.

---

**Q: What is log compaction vs log retention in Kafka?**

**Short:** Retention deletes old messages after time/size limit. Compaction keeps only the latest value per key — useful for state snapshots.

**Detailed:**
- **Retention:** `log.retention.hours=168` (7 days default) — delete old segments.
- **Compaction:** `cleanup.policy=compact` — keep only the latest message per key. Old versions of a key are removed. A tombstone (null value) marks deletion.
- Use compaction for: user preferences, account state, configuration — where you only need current value.
- Kafka Streams changelog topics use compaction to maintain state stores.

---

**Q: What is a Dead Letter Queue (DLQ) in Kafka?**

**Short:** A separate topic where failed messages are sent after N retry attempts — allows investigation without blocking the main consumer.

**Detailed:**
```javascript
// Consumer with DLQ pattern
consumer.on('message', async (msg) => {
  try {
    await processMessage(msg);
  } catch (err) {
    if (msg.retryCount >= 3) {
      await producer.send({ topic: 'orders.dlq', messages: [{ value: msg.value, headers: { error: err.message } }] });
    } else {
      await producer.send({ topic: 'orders.retry', messages: [{ value: msg.value, headers: { retryCount: msg.retryCount + 1 } }] });
    }
  }
});
```
DLQ messages should include: original topic, error message, timestamp, retry count, original partition/offset.

---

## Links
- [[Study Plan/Kafka]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
