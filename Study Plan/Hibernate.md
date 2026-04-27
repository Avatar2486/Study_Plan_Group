# Hibernate

### **. Hibernate Basics & Core Concepts**

- What is Hibernate? Why is it used?
- ORM (Object-Relational Mapping) vs JDBC
- JPA vs Hibernate (Specification vs Implementation)
- Hibernate Architecture & Components
    - `SessionFactory`, `Session`, `Transaction`, `Query`, `Criteria`
    - First-Level Cache & Second-Level Cache
- Hibernate Lifecycle & States of an Entity (`Transient`, `Persistent`, `Detached`, `Removed`)
- save, persist, merge and update difference

---

### **2. Hibernate Configuration**

- Configuring Hibernate with `hibernate.cfg.xml` and `persistence.xml`
- Hibernate Properties (`hibernate.dialect`, `hibernate.show_sql`, etc.)
- Difference between `persistence.xml` and `hibernate.cfg.xml`
- Programmatic Configuration (without XML)

---

### **3. Entity Mapping & Annotations**

- **Basic Annotations**: `@Entity`, `@Table`, `@Column`, `@Id`, `@GeneratedValue`
- **Primary Key Strategies**: `AUTO`, `IDENTITY`, `SEQUENCE`, `TABLE`
- **Column Constraints**: `@UniqueConstraint`, `@NotNull`, `@Size`, `@Column(nullable = false)`
- **Attribute Overrides** (`@AttributeOverride`, `@AttributeOverrides`)
- **Enumerations & Converters** (`@Enumerated`, `AttributeConverter`)
- **Embedded Objects** (`@Embedded`, `@Embeddable`, @EmbeddedId)
- **Immutable Entities & Read-Only Tables** (`@Immutable`)

---

### **4. Relationships in Hibernate (One-to-One, One-to-Many, Many-to-Many, Many-to-One)**

- **Bidirectional vs Unidirectional Relationships**
- **Join Column Strategies** (`@JoinColumn`, `@PrimaryKeyJoinColumn`)
- **Cascade Types (`ALL`, `PERSIST`, `MERGE`, `REMOVE`, `REFRESH`, `DETACH`)**
- **Fetching Strategies (`LAZY`, `EAGER`) and Performance Implications**
- **MappedBy vs JoinTable in Bidirectional Relationships**
- **Handling Orphan Removal (`orphanRemoval=true`)**
- **Using `@MapsId` to Share Primary Key in Relations**
- **Difference Between `@OneToMany` and `@ManyToOne`**

---

### **5. Hibernate Caching (First-Level Cache, Second-Level Cache, Query Cache)**

- **First-Level Cache (`Session` Level, Automatic)**
- **Second-Level Cache (`SessionFactory` Level) – Ehcache, Redis, Infinispan, Hazelcast**
- **Query Caching (`@Cacheable`, `hibernate.cache.use_query_cache`, @Cache)**
- **Evicting Entities from Cache (`session.evict()`, `session.clear()`)**
- **Cache Invalidation Strategies**
- **Common Cache Pitfalls (Dirty Reads, Cache Staleness, Expiry Policies)**

---

### **6. Transactions & Concurrency Handling**

- **ACID Properties & Hibernate Transaction Management**
- **Propagation Levels (`REQUIRED`, `SUPPORTS`, `MANDATORY`, `NEVER`, `NESTED`)**
- **Isolation Levels (`READ_UNCOMMITTED`, `READ_COMMITTED`, `REPEATABLE_READ`, `SERIALIZABLE`)**
- **Optimistic Locking (`@Version`, `OptimisticLockException`)**
- **Pessimistic Locking (`PESSIMISTIC_READ`, `PESSIMISTIC_WRITE`, PESSIMISTIC_FORCE_INCREMENT)**
- **Deadlocks in Hibernate & How to Avoid Them**
- **Savepoints in Hibernate Transactions**
- **Automatic Rollback & Transaction Timeouts**

---

### **7. Hibernate Query Mechanisms (HQL, JPQL, Criteria API, Native SQL, Named Queries)**

- **HQL (Hibernate Query Language) – Queries on Entities, Not Tables**
- **JPQL (Java Persistence Query Language) – JPA-compliant Queries**
- **Named Queries (`@NamedQuery`, `@NamedNativeQuery`)**
- **Criteria API – Dynamic Queries, Projections, Filters**
- **Native SQL Queries & Result Mappings (`@SqlResultSetMapping`)**
- **Pagination Strategies (`setMaxResults()`, `setFirstResult()`)**
- **Common Query Optimization Techniques (JOIN FETCH, INDEX HINTS, BATCH FETCHING)**

---

### **8. Hibernate Performance Tuning & Optimization**

- **N+1 Problem and How to Solve It (`JOIN FETCH`, `@BatchSize`)**
- **Lazy vs Eager Loading – When to Use What?**
- **Batch Processing & Bulk Inserts/Updates (`jdbc_batch_size`, `StatelessSession`)**
- **Connection Pooling (`c3p0`, `HikariCP`, `Apache DBCP`)**
- **SQL Query Logging & Performance Analysis (`hibernate.show_sql`, `hibernate.format_sql`)**
- **Indexing Strategies for Large Tables (`@Index`)**
- **When to Use `StatelessSession` for High-Throughput Transactions**
- **Hibernate Fetch Strategies (`JOIN`, `SELECT`, `SUBSELECT`, `BATCH`, `DYNAMIC`)**
- **Using Projection Queries Instead of Fetching Full Entities**

---

### **9. Hibernate Event Listeners & Interceptors**

- **Lifecycle Callbacks (`@PrePersist`, `@PostPersist`, `@PreUpdate`, `@PostUpdate`, `@PreRemove`, `@PostRemove`)**
- **Custom Hibernate Event Listeners (`PreInsertEventListener`, `PreUpdateEventListener`)**
- **Interceptors in Hibernate (`EmptyInterceptor`, `onSave()`, `onDelete()`)**
- **Auditing Changes with `@PreUpdate` and `@PostUpdate`**
- **Multi-Tenancy Support in Hibernate (SCHEMA, DATABASE, DISCRIMINATOR)**

---

### **10. Advanced Hibernate Topics & FAANG-Level Scenarios**

- **Implementing Soft Deletes (`@SQLDelete`, `@Where`)**
- @Modifying
- **Concurrency Issues in a Multi-Threaded Environment**
- **Sharding & Partitioning with Hibernate**
- **Migrating from Hibernate to JOOQ for High Performance**
- **GraphQL with Hibernate – Efficient Querying**
- **Distributed Hibernate (Using Hibernate in Microservices)**
- **Handling Huge Datasets in Hibernate (Parallel Queries, Scrollable Results, Cursors)**
- **Implementing Custom Hibernate Dialects for Non-Standard Databases**
- **Best Practices for Using Hibernate in Production Systems**

---

### **11. Interview Questions & Scenario-Based Problems**

- **Hibernate Query Optimization Techniques in Large Systems**
- **How to Handle Large-Scale Hibernate Applications with Multi-Tenancy?**
- **How Does Hibernate Handle High-Throughput Transactions?**
- **Explain Hibernate Caching Strategies in a Distributed System**
- **How to Debug Hibernate Performance Issues?**
- **What Are the Most Common Hibernate Pitfalls & How to Avoid Them?**