# Kafka

---

## **🔥 1. Kafka Internals (Deep Dive)**

### **Core Topics**

✅ **Kafka Architecture** (Brokers, Partitions, Topics, Zookeeper)

✅ **Leader-Follower Replication** (ISR, AR, Leader Election)

✅ **Kafka Log Segments & Retention Policy**

✅ **Message Storage & Compaction**

✅ **Kafka Exactly-Once Semantics (EOS)**

### **Practice Questions**

1️⃣ How does Kafka **ensure fault tolerance**?

2️⃣ What happens **internally when a producer sends a message**?

3️⃣ Explain **Kafka’s replication mechanism and leader election**.

4️⃣ How does **Kafka handle backpressure**?

5️⃣ What happens if a Kafka broker **crashes**?

6️⃣ How does **Kafka achieve exactly-once processing**?

### **Hands-On Practice**

✔ Inspect Kafka logs and **analyze segment files**.

✔ Simulate a **broker failure** and observe leader election.

✔ Configure **Kafka retention policy** and observe log compaction.

---

## **🔥 2. Kafka Producers (High-Performance Optimization)**

### **Core Topics**

✅ **Producer Acknowledgments (acks=0, 1, all)**

✅ **Batching & Compression (LZ4, Snappy, GZIP)**

✅ Kafka Producer Retries & Idempotency **& Exactly-Once Guarantees**

✅ **Partitioning Strategies (Custom Partitioners)**

### **Practice Questions**

1️⃣ What is the **impact of acks=all vs acks=1**?

2️⃣ How does Kafka **handle duplicate messages**?

3️⃣ Explain **Kafka producer retries and their impact on ordering**.

4️⃣ When should you **use a custom partitioner**?

### **Hands-On Practice**

✔ Write a **high-throughput producer with batching & compression**.

✔ Implement a **custom Kafka partitioner**.

✔ Simulate **duplicate message scenarios and fix them**.

---

## **🔥 3. Kafka Consumers (Scalability & Parallelization)**

### **Core Topics**

✅ **Consumer Group Rebalancing**

✅ **Offset Management (Committed, Uncommitted, Auto-Offset Reset)**

✅ **Manual vs Auto-Commit Strategies**

✅ **Consumer Lag Monitoring & Tuning**

✅ **Kafka Consumer Multithreading Best Practices**

### **Practice Questions**

1️⃣ How does Kafka **handle rebalancing when a consumer joins or leaves**?

2️⃣ What is the **difference between at-least-once and at-most-once semantics**?

3️⃣ How do you **efficiently consume messages with multiple threads**?

4️⃣ What happens if a **consumer crashes before committing an offset**?

5️⃣ How can you **reduce consumer lag in a high-throughput system**?

### **Hands-On Practice**

✔ Implement a **consumer that manually commits offsets**.

✔ Simulate a **rebalance event and monitor lag**.

✔ Run **multiple consumers in parallel and tune performance**.

---

## **🔥 4. Kafka Scalability & Performance Tuning**

### **Core Topics**

✅ **Kafka Partitioning & Parallelism**

✅ **Optimizing Throughput & Latency**

✅ **Kafka Cluster Sizing & Capacity Planning**

✅ **Kafka Tuning (log.segment.bytes, num.network.threads, fetch.max.bytes)**

✅ **ISR Shrinking & Impact on Availability**

✅ Kafka Replication

### **Practice Questions**

1️⃣ How does **partitioning impact Kafka’s scalability**?

2️⃣ What are the **trade-offs between increasing partitions vs increasing brokers**?

3️⃣ How can you **optimize Kafka for low-latency streaming applications**?

4️⃣ What Kafka metrics should be **monitored for performance tuning**?

5️⃣ How do you **benchmark Kafka throughput**?

### **Hands-On Practice**

✔ Run a **performance test using Kafka’s built-in producer performance tool**.

✔ Tune **broker and producer configurations for max throughput**.

✔ Monitor Kafka **JMX metrics using Prometheus/Grafana**.

---

## **🔥 5. Kafka Transactions & Exactly-Once Processing**

### **Core Topics**

✅ **Kafka Transaction API**

✅ **Idempotent Producer vs Transactional Producer** 

✅  **Idempotent Consumer vs Transactional Consumer**

✅  Maintaing order of messages on producer and consumer

✅ **EOS (Exactly-Once Semantics) with Kafka Streams**

✅ **How Kafka Ensures Atomicity Across Partitions**

### **Practice Questions**

1️⃣ What is the difference between **idempotent and transactional producers**?

2️⃣ How does Kafka **guarantee atomic writes across partitions**?

3️⃣ How do you **achieve exactly-once processing with Kafka Streams**?

### **Hands-On Practice**

✔ Implement a **Kafka producer with transactional writes**.

✔ Analyze **Kafka Streams exactly-once behavior**.

---

**🔥 6. Kafka Security & Access Control**

✅ **SSL/TLS Encryption (Securing Data in Transit)**

✅ **SASL Authentication (Plain, SCRAM, Kerberos, OAuth2)**

✅ **Kafka ACLs (Access Control with Zookeeper/KRaft Mode)**

🔹 **Practice Questions**

1️⃣ How does **Kafka secure producer-consumer communication**?

2️⃣ What are **different authentication mechanisms in Kafka**?

3️⃣ How do **Kafka ACLs work**, and how can you restrict access to a topic?

🔹 **Hands-On**

✔ Set up **Kafka with SSL and SASL authentication**.

✔ Configure **ACLs to restrict access to a Kafka topic**.

---

### **🔥 7. Kafka with Microservices & Event-Driven Architecture**

✅ **Kafka as an Event Bus (CQRS, Event Sourcing)**

✅ **Debezium for Change Data Capture (CDC)**

✅ **Kafka Schema Evolution with Avro & Schema Registry**

✅ **Handling Out-of-Order Messages & Idempotency**

✅ Dead Letter Queue and why kafka writes are fast

✅ Backpressure & Zero Copy 

🔹 **Practice Questions**

1️⃣ How do **Kafka-based microservices ensure idempotency**?

2️⃣ How do you handle **schema evolution in Kafka**?

3️⃣ What are the **trade-offs of using Kafka vs RabbitMQ vs Pulsar**?

🔹 **Hands-On**

✔ Implement a **Kafka-based event-driven microservice**.

✔ Use **Debezium to capture database changes and publish to Kafka**.

---

### **🔥 8. Kafka Streams & Real-Time Processing**

✅ **Kafka Streams vs Spark Streaming vs Flink**

✅ **Stateful vs Stateless Stream Processing**

✅ **Joins, Windows, and Aggregations in Kafka Streams**

🔹 **Practice Questions**

1️⃣ How does **Kafka Streams ensure exactly-once processing**?

2️⃣ What is the **difference between stream-table joins and windowed joins**?

3️⃣ How do you **scale Kafka Streams applications**?

🔹 **Hands-On**

✔ Implement a **Kafka Streams pipeline for real-time data processing**.

✔ Create a **windowed aggregation for a stock price ticker**.

---

### **🔥 9. Kafka in Large-Scale Distributed Systems**

✅ **Cross-Data Center Replication (MirrorMaker 2.0, Confluent Replicator)**

✅ **Geo-Distributed Kafka Clusters**

✅ **Eventual Consistency & Ordering Guarantees**

🔹 **Practice Questions**

1️⃣ How does **Kafka MirrorMaker 2.0 work for cross-cluster replication**?

2️⃣ What are the **challenges of running Kafka in multiple data centers**?

3️⃣ How do you **handle message ordering across Kafka clusters**?

🔹 **Hands-On**

✔ Set up **Kafka MirrorMaker 2.0 for cross-cluster replication**.

✔ Simulate a **Kafka failover scenario between data centers**.

---