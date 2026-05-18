# AWS — Answer Bank

---

**Q: What is the difference between IAM users, roles, and policies?**

**Short:** Users = people with long-term credentials. Roles = temporary credentials assumed by services or people. Policies = permission documents attached to users/roles.

**Detailed:**
- **User:** Has access key + secret. Used for humans or apps with long-term access. Avoid for services.
- **Role:** No permanent credentials. Assumed temporarily. EC2 instance, Lambda, ECS task can assume a role.
- **Policy:** JSON document defining what is allowed/denied. Attached to users, groups, or roles.
- **Least privilege:** Only grant what's needed. Use roles for service-to-service auth — never hardcode access keys.

```json
// Policy example
{ "Effect": "Allow", "Action": ["s3:GetObject"], "Resource": "arn:aws:s3:::mybucket/*" }
```

---

**Q: What is the difference between Security Groups and NACLs?**

**Short:** Security Groups are stateful (return traffic auto-allowed), attached to instances. NACLs are stateless (must allow both directions), attached to subnets.

**Detailed:**
| | Security Group | NACL |
|--|--|--|
| Level | Instance / ENI | Subnet |
| Stateful | Yes | No |
| Allow/Deny | Allow only | Allow + Deny |
| Rule evaluation | All rules evaluated | Rules evaluated in number order |
| Default | Deny all inbound, allow all outbound | Allow all |

Use Security Groups for most cases. Use NACLs to block specific IPs at subnet level (e.g., known bad actors).

---

**Q: What is the difference between S3 storage classes?**

**Short:** Standard (hot data), IA (infrequent access), Glacier (archive). Intelligent-Tiering auto-moves between tiers.

**Detailed:**
| Class | Use Case | Retrieval |
|-------|---------|---------|
| Standard | Frequently accessed data | Immediate |
| Standard-IA | Monthly access, lower cost | Immediate (retrieval fee) |
| One Zone-IA | Non-critical infrequent data | Immediate |
| Glacier Instant | Archive, accessed once/quarter | Milliseconds |
| Glacier Flexible | Long-term archive | Minutes to hours |
| Deep Archive | Compliance, 7+ year retention | 12+ hours |
| Intelligent-Tiering | Unknown access patterns | Auto-optimizes |

Use Lifecycle Policies to auto-transition objects between classes based on age.

---

**Q: What is the difference between EC2 On-Demand, Reserved, and Spot instances?**

**Short:** On-Demand = pay per hour (flexible). Reserved = 1–3 year commitment (up to 72% cheaper). Spot = spare capacity (up to 90% cheaper, can be interrupted).

**Detailed:**
| Type | Cost | Best For | Risk |
|------|------|---------|------|
| On-Demand | Full price | Dev, unpredictable loads | None |
| Reserved (Standard) | Up to 72% off | Steady-state production | 1–3 year lock-in |
| Reserved (Convertible) | Up to 54% off | When you might change instance type | Less savings |
| Savings Plans | Up to 72% off | Flexible compute commitment | Need to commit $/hour |
| Spot | Up to 90% off | Batch, data processing, fault-tolerant | 2-min interruption notice |

---

**Q: What is the difference between ALB and NLB?**

**Short:** ALB = Layer 7 (HTTP/HTTPS, path/host routing). NLB = Layer 4 (TCP/UDP, ultra-low latency).

**Detailed:**
| | ALB (Application LB) | NLB (Network LB) |
|--|--|--|
| Layer | 7 (HTTP/HTTPS/gRPC) | 4 (TCP/UDP/TLS) |
| Routing | Path, host, header, query string | IP + Port |
| Use case | Web apps, microservices | Gaming, IoT, low latency, static IPs |
| SSL termination | Yes | Yes (TLS passthrough also supported) |
| WebSockets | Yes | Yes |

Use ALB for most web applications. Use NLB when you need static IPs, TCP passthrough, or sub-millisecond latency.

---

**Q: What is the difference between RDS Multi-AZ and Read Replica?**

**Short:** Multi-AZ = HA (standby for failover, not for reads). Read Replica = scale reads (separate endpoint, eventual consistency).

**Detailed:**
| | Multi-AZ | Read Replica |
|--|--|--|
| Purpose | High availability | Read scaling |
| Standby accessible | No (automatic failover only) | Yes (separate read endpoint) |
| Replication | Synchronous | Asynchronous |
| Data lag | None | Seconds (replica lag) |
| Automatic failover | Yes (60–120 sec) | Manual promotion |
| Cross-region | No | Yes |

Combine both: Multi-AZ for HA + Read Replicas for offloading SELECT queries.

---

**Q: What is Lambda cold start and how do you reduce it?**

**Short:** The first invocation initializes the container — takes 100ms–10s. Subsequent invocations reuse the warm container.

**Detailed:**
- Cold start time varies by runtime: Go/Python ≈ 100ms. Java/C# ≈ 1–10s (JVM startup).
- **Reduce cold starts:**
  - Use Provisioned Concurrency (keep N instances warm — costs money)
  - Keep Lambda package size small (smaller = faster init)
  - Avoid heavy initialization at module level (lazy-load connections)
  - Use Snapstart (Java) — saves initialized state
  - Use Go/Python/Node.js runtimes (faster than Java/.NET)
- Move DB connections outside handler function — reused across warm invocations.

---

**Q: What is the difference between SQS, SNS, and EventBridge?**

**Short:** SQS = message queue (point-to-point). SNS = pub/sub fan-out. EventBridge = event bus with routing rules.

**Detailed:**
| | SQS | SNS | EventBridge |
|--|--|--|--|
| Model | Queue (pull) | Topic (push) | Event bus (rules-based routing) |
| Fan-out | No (one consumer per message) | Yes (multiple subscribers) | Yes (multiple targets) |
| Retention | Up to 14 days | No retention | Archive option |
| Filtering | No | Message filter policies | Rich rule-based filtering |
| Use case | Decouple services, task queue | Broadcast to multiple services | AWS service events, routing |

Common pattern: SNS → SQS (fan-out to multiple queues, then process independently).

---

**Q: What are the 5 pillars of the Well-Architected Framework?**

**Short:** Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization.

**Detailed:**
| Pillar | Key Practices |
|--------|--------------|
| **Operational Excellence** | Infrastructure as code, monitoring, runbooks, small reversible changes |
| **Security** | IAM least privilege, encryption at rest/transit, GuardDuty, CloudTrail |
| **Reliability** | Multi-AZ, auto-scaling, backups, chaos engineering, health checks |
| **Performance** | Right-sizing, caching (CloudFront, ElastiCache), read replicas, async |
| **Cost Optimization** | Reserved instances, right-sizing, S3 lifecycle, auto-scaling, spot |

---

## Links
- [[Study Plan/AWS]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
