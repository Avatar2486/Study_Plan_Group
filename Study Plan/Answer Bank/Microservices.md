# Microservices — Answer Bank

---

**Q: What is the difference between Monolithic and Microservices architecture?**

**Short:** Monolith = single deployable unit, simple but hard to scale. Microservices = independent services, each owning its domain, independently deployable.

**Detailed:**
| | Monolith | Microservices |
|--|--|--|
| Deployment | Single unit | Independent per service |
| Scaling | Scale entire app | Scale only bottleneck service |
| Tech stack | Single stack | Polyglot (each service can differ) |
| Data | Shared DB | Database per service |
| Failure | One failure = whole app down | Isolated failures |
| Complexity | Low initially | High (distributed systems) |
| Best for | Small teams, early stage | Large teams, scale, clear domain boundaries |

---

**Q: What is a Circuit Breaker pattern?**

**Short:** Wraps calls to an unreliable service. After N failures, "opens" the circuit and returns a fallback immediately — preventing cascade failures.

**Detailed:**
```
States:
- CLOSED: requests pass through normally (monitoring failure rate)
- OPEN: requests fail fast without calling the service (for `timeout` duration)
- HALF-OPEN: let a few test requests through — if they succeed, close the circuit

Example with resilience4j:
@CircuitBreaker(name = "paymentService", fallbackMethod = "paymentFallback")
public Response processPayment(Order order) {
    return paymentClient.charge(order);
}

public Response paymentFallback(Order order, Exception e) {
    return Response.queued("Payment queued for retry");
}
```

---

**Q: What is the Saga pattern vs 2PC for distributed transactions?**

**Short:** 2PC = blocking, requires all services to lock resources. Saga = async, eventual consistency with compensating transactions. Saga is preferred in microservices.

**Detailed:**
- **2PC (Two-Phase Commit):** Coordinator asks all services to "prepare" (lock), then "commit". Problem: if coordinator dies after prepare but before commit → all services stuck locked forever.
- **Saga (Choreography):** Services emit events. Each service listens and reacts. No central coordinator. Hard to debug.
- **Saga (Orchestration):** Central Saga Orchestrator tells each service what to do. Easier to track state.
- **Compensating transaction:** reverse an already-completed step (e.g., refund payment if inventory fails).

---

**Q: What is the Transactional Outbox Pattern?**

**Short:** Write to DB + write event to an outbox table in the same transaction. A separate process reads the outbox and publishes to Kafka/queue. Guarantees no lost events.

**Detailed:**
```
Problem: Writing to DB and publishing to Kafka are two separate actions — one can fail.

Solution:
1. In same DB transaction:
   - INSERT INTO orders (...)
   - INSERT INTO outbox (event_type, payload) VALUES ('order.created', ...)
2. Outbox publisher (separate process/CDC):
   - Reads unpublished outbox rows
   - Publishes to Kafka
   - Marks as published

OR use Debezium (CDC) to watch outbox table → auto-publish to Kafka
```

---

**Q: What is the difference between synchronous and asynchronous communication in microservices?**

**Short:** Sync (REST/gRPC) = immediate response, tight coupling. Async (Kafka/RabbitMQ) = decoupled, eventual consistency, more resilient.

**Detailed:**
| | Synchronous | Asynchronous |
|--|--|--|
| Protocol | REST, gRPC, Feign | Kafka, RabbitMQ, SQS |
| Coupling | Tight (caller waits) | Loose (caller doesn't wait) |
| Latency | Low for simple calls | Higher (queue overhead) |
| Resilience | Cascading failures if downstream is down | Caller continues if consumer is down |
| Consistency | Immediate | Eventual |
| Use case | Query data, user-facing operations | Events, notifications, long processing |

---

**Q: What is the Backend for Frontend (BFF) pattern?**

**Short:** A dedicated API layer per client type (web BFF, mobile BFF) that aggregates and shapes data from multiple services for that client's specific needs.

**Detailed:**
```
Problem: Mobile and web clients have different data needs.
Mobile needs: minimal data, optimized for battery/bandwidth
Web needs: richer data, more fields

Solution:
Mobile App → Mobile BFF → [User Service, Order Service, Product Service]
Web App    → Web BFF    → [same services, different aggregation]

Benefits:
- Each BFF is owned by the frontend team
- Reduces over-fetching / under-fetching
- Client-specific caching, auth logic
- Shields clients from service-level changes
```

---

**Q: What is service discovery and how does it work?**

**Short:** Services register their location (IP:port) in a registry. Clients look up the registry to find the service address — handles dynamic IPs in container environments.

**Detailed:**
- **Client-side discovery (Eureka + Ribbon):** Client queries registry, gets list of instances, load balances itself.
- **Server-side discovery (Consul + NGINX/AWS ALB):** Client calls load balancer, which queries registry and routes.
- In Kubernetes: built-in DNS service discovery — `http://service-name.namespace.svc.cluster.local`.
- When to use: any environment where service IPs change dynamically (containers, VMs with auto-scaling).

---

**Q: How do you implement distributed tracing?**

**Short:** Inject a Correlation ID (Trace ID) into every request. Each service logs with this ID. Visualize the full request flow across services.

**Detailed:**
```javascript
// Middleware — generate/propagate trace ID
app.use((req, res, next) => {
  req.traceId = req.headers['x-trace-id'] || uuid();
  res.setHeader('x-trace-id', req.traceId);
  logger.info({ traceId: req.traceId, method: req.method, path: req.path });
  next();
});

// When calling another service — pass trace ID
await axios.get(serviceUrl, { headers: { 'x-trace-id': req.traceId } });
```
Tools: **OpenTelemetry** (standard instrumentation) → **Jaeger** or **Zipkin** (visualization). In Spring Boot: Spring Cloud Sleuth auto-injects trace/span IDs.

---

**Q: What are microservices anti-patterns to avoid?**

**Short:** Shared database, chatty services, too-fine granularity, synchronous chains, no service contracts.

**Detailed:**
- **Shared DB:** Services sharing a database = tight coupling. Changes to schema break multiple services.
- **Chatty services:** A single user request triggers 10+ synchronous calls between services. Fix: aggregate at API Gateway or BFF.
- **Too fine granularity:** Splitting too small creates distributed monolith. Each operation needs to call 20 services. Align services with business domains (DDD bounded contexts).
- **Sync chain:** A→B→C→D synchronously. If D is slow, everything is slow. Fix: async or aggregate.
- **No versioning:** Changing an API breaks consumers. Always version APIs. Use backward-compatible changes (add fields, don't remove).

---

## Links
- [[Study Plan/Microservices]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
