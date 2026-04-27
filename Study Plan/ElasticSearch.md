# ElasticSearch

---

# ✅ **ElasticSearch — Roadmap**

### **📌 Core Concepts (Must-Know)**

✅ **1️⃣ What is Elasticsearch?**

- Distributed, RESTful search engine
- Full-text search vs. relational databases
- Use cases: Log analytics, monitoring, autocomplete, real-time search

✅ **2️⃣ Elasticsearch Architecture & Internals**

- **Cluster, Node, Shard, and Index**
- **Primary vs Replica Shards** (Data replication & fault tolerance)
- **How Elasticsearch handles data distribution**
- **Elasticsearch vs Solr vs OpenSearch**

✅ **3️⃣ Installing & Running Elasticsearch**

- **Standalone setup vs Cluster setup**
- **Running Elasticsearch with Docker**
- **Basic API requests (`_cat/nodes`, `_cat/indices`)**

---

### **🔥 Indexing & Querying (FAANG-Level Must-Know)**

✅ **4️⃣ Understanding Indexing**

- Index Management (Creation, Updation, Deletion) & index settings
- **Creating, Updating, and Deleting Documents**
- **Mappings & Dynamic Field Types**
- Data types
- **Analyzers & Customizing Analyzers (Standard, Whitespace, Edge NGram, etc.)**
- **Understanding Text vs Keyword Fields**
- **Document Update Internals**: no in-place updates, segment merging & write amplification, how write happens internally
- How elasticsearch handles concurrent writes on same document
- **How ES stores data (Lucene buffer, translog, disk, flush process)**?

✅ **5️⃣ Searching in Elasticsearch**

- **Match Query, Term Query, Range Query, Bool Query**
- **Full-Text Search vs. Exact Match Search**
- **Relevance Scoring & `explain` API, BM25 and it’s tuning**
- **Sorting, Filtering, and Aggregations**

✅ **6️⃣ Elasticsearch Query DSL (Deep Dive)**

- **Match vs Term Query (When & Why)**
- **Phrase Search, Wildcard Search, Fuzzy Search, Prefix match and Multi match**
- **Boosting & Function Score for Ranking**
- **Pagination & Deep Pagination (`from`, `size`, `search_after`)**

---

### **🔥 Deep Internals & Relevance (FAANG-Only)**

✅ **7️⃣ Lucene & Index Internals**

- **How Inverted Index Works**
- **Text Analysis Pipeline**: character filters, tokenizers, token filters
- **FieldData & Doc Values for sorting and aggregations**

✅ **8️⃣ Scoring & Ranking**

- **BM25 vs TF-IDF (Modern scoring model)**
- **Custom Ranking with Function Score**
- **Relevance tuning & `explain` API usage**

---

### **🔥 Advanced Elasticsearch Concepts**

✅ **9️⃣ Performance Optimization & Scaling**

- **Index Lifecycle Management (ILM)**
- **Shard Sizing, Segment Merging**
- **Lazy Queries, Circuit Breakers, Query Caching**
- **Hot-Warm-Cold Architecture**

✅ **🔟 Distributed System Internals**

- **Cluster State, Gossip Protocol, Discovery**
- **Replication, Failover, Split-Brain Handling**
- **Write Consistency & Quorum**

✅ **🔟+ Real-Time Systems & Streaming**

- **ELK Stack (Logstash + Beats + ES + Kibana)**
- **Kafka → Logstash → Elasticsearch**
- **Backpressure, Retry, and DLQ Patterns**
- **Elastic Common Schema (ECS)**

---

### **🧠 Search Design Patterns & Production**

✅ **1️⃣1️⃣ Autocomplete System Design**

- **Edge NGram vs Completion Suggester, NGram**
- **Typo Tolerance: Fuzzy Match, Levenshtein**
- **Infix Matching with NGram**
- **Internationalization, Stemming, Synonyms**

✅ **1️⃣2️⃣ Multi-Tenancy & Index Design**

- **Per-tenant Index vs Shared Index + Routing**
- **Index Aliases & Document-Level Security (DLS)**
- **Field-level access control (FLS)**

✅ **1️⃣3️⃣ Multi-Region Deployment**

- **Read-local, Write-global strategy**
- **Cross-Cluster Search (CCS)**
- **Cross-Cluster Replication (CCR)**
- **Latency, consistency, failover concerns**

✅ **1️⃣4️⃣ Elasticsearch as Primary DB?**

- Tradeoffs vs RDBMS / NoSQL
- Document Update Costs
- Durability, Eventual Consistency
- How ES handles concurrent read/writes

---

### **🔐 Monitoring & Security (Enterprise-Grade)**

✅ **1️⃣5️⃣ Observability**

- Monitoring with Kibana + Elastic Stack
- `_nodes/stats`, `_cluster/health`, slow logs
- Hot threads, heap dumps

✅ **1️⃣6️⃣ Security Best Practices**

- **TLS between nodes**
- **x-pack Security**: Authentication, Authorization
- **RBAC, API Keys, Document-Level Security**
- Audit logging, encrypted snapshots

---

### **🔥 FAANG-Level Practice Questions**

✅ **Basic**

1. What is the difference between **Elasticsearch and a relational DB**?
2. How do you **create and delete an index** safely?
3. Difference between **match and term query**?

✅ **Intermediate**

4. How does ES ensure **replication, availability, and fault tolerance**?

5. What are **shards**, and how does ES use them for scaling?

6. What’s the impact of **segment merging** on performance?

✅ **Advanced**

7. Explain **CAP Theorem trade-offs in Elasticsearch**

8. How do you **optimize for 1B+ documents**?

9. Design an **autocomplete engine with typo tolerance**

10. How would you **scale Elasticsearch to multiple regions** with low latency?

11. Compare **Elasticsearch vs OpenSearch** for enterprise use

12. What are the risks of using **Elasticsearch as a primary datastore**?

---

✅ With this enhanced roadmap, you're now **fully FAANG-ready** for:

- Infra/System Design Interviews
- Backend + Distributed Systems rounds
- Real-time streaming + log analytics roles
- Search Infrastructure (autocomplete, scoring, etc.)
- Elasticsearch Production & Observability use cases

---

Practice:

# **Elasticsearch Practice Questions**

---

## **1️⃣ Creating, Updating, and Deleting Documents**

1. Insert a new product with `name`, `brand`, `price`, `description`, `in_stock`, `release_date`.
2. Update the `price` and `in_stock` status of an existing product by its ID.
3. Upsert a product: if it exists, update its `description`; if not, create it.
4. Delete a product by ID and verify it no longer exists.

---

## **2️⃣ Match Query, Term Query, Range Query, Bool Query**

1. Write a **match query** to find products with `"gaming"` in `name`.
2. Write a **term query** to find products with `brand.keyword = "Dell"`.
3. Write a **range query** to find products with `price < 50000`.
4. Write a **bool query**: must match `"laptop"` in `name`, should match `"Dell"` or `"HP"` in brand, and filter for `in_stock = true`.

---

## **3️⃣ Sorting, Filtering, and Aggregations**

1. Retrieve products **sorted by price descending**.
2. Filter products **where in_stock = true** and `price < 50000`.
3. Create a **terms aggregation** on `brand.keyword` to count products per brand.
4. Create a **range aggregation** for `price` with ranges: `0-30000`, `30001-50000`, `50001+`.

---

## **4️⃣ Phrase Search, Wildcard, Fuzzy, Prefix, Multi-Match, Exists**

1. Write a **match_phrase query** to find `"gaming laptop"` in `description`.
2. Write a **wildcard query** to find products with `brand` starting with `"H*"`.
3. Write a **fuzzy query** to find `"laptpo"` in `name`.
4. Write a **prefix query** to find products with `name` starting with `"Gam"`.
5. Write a **multi_match query** for `"gaming laptop"` across `name` and `description`.
6. Write an **exists query** to find all products where `release_date` exists.

---

## **5️⃣ Boosting**

1. Write a **field-level boost** query: boost `name` matches over `description`.
2. Write a **query-level boost**: boost products with `brand = "Dell"` by 2.
3. Write a **boosting query**: promote `"gaming laptop"` in name, demote `description = "refurbished"` with `negative_boost = 0.3`.
4. Combine **bool query** with boosting: must `"laptop"` in name, boost `"Dell"` in brand, demote `"refurbished"` in description.

---

## **6️⃣ Pagination & Deep Pagination**

1. Retrieve the first 5 products using `from` and `size`.
2. Retrieve products **page 2** with 5 products per page.
3. Use `search_after` to paginate deeply (e.g., after product with `price = 45000`).
4. Compare performance of `from/size` vs `search_after` on 1000+ documents.

---

# **7️⃣ Mixed / Combination Questions (15–20)**

1. Find **gaming laptops**, must be **in stock**, sorted by price descending, top 5 results.
2. Find **products with `"laptop"` in name or `"gaming"` in description**, boost `"Dell"` in brand, demote `"refurbished"`.
3. Aggregate **brands** for products **with price < 50000**, show top 3 brands.
4. Retrieve products **with `"gaming laptop"` phrase**, filter `in_stock = true`, boost `name` over description.
5. Find all products **with `brand` starting with "H"`**, sorted by release_date, paginate first 5.
6. Search `"laptpo"` fuzzily in name, multi_match across name and description, aggregate by brand.
7. Filter products **price between 30000–50000**, sort descending, include only products with `release_date`.
8. Retrieve nested reviews **with rating >= 4**, highlight matched comments, sort by rating.
9. Use `query_string` to search `"gaming AND laptop NOT refurbished"` across name and description.
10. Combine **bool + filter + terms aggregation**: in_stock = true, name contains `"laptop"`, count brands.
11. Use `prefix` query `"Gam"` in name, filter price < 50000, return top 3 results.
12. Boost `"Dell"` products 2x, fuzzy search `"lapto"` in name, filter in_stock = true.
13. Use `search_after` to retrieve next page of products sorted by price.
14. Combine **exists + range**: products where `release_date` exists and `price > 40000`.
15. Nested query: find products with **review.rating >= 5** and highlight `comment`.