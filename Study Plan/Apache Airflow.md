# Apache Airflow

## FAANG-Level Apache Airflow Study Plan

### 1️⃣ Basics & Foundations

- What is Airflow? Why is it used?
- Airflow vs Cron / vs Luigi / vs Prefect / vs Dagster
- Core Components:
    - **DAG**, **Task**, **Operator**, **Scheduler**, **Executor**, **Worker**, **Webserver**, **Metastore (DB)**
- Directed Acyclic Graph (DAG) concept
- Anatomy of a simple DAG (with example)

---

### 2️⃣ DAG Internals & Configuration

- DAG Structure: `dag_id`, `start_date`, `schedule_interval`, `catchup`, `default_args`, etc.
- DAG Execution Flow:
    - Dependencies: `set_upstream()`, `set_downstream()`, `>>`, `<<`
    - Triggers: `TriggerRule`, `depends_on_past`, `wait_for_downstream`
- DAG Parameters: `params`, `Variable`, `XCom`, `BranchPythonOperator`

---

### 3️⃣ Operators & Hooks

- Types of Operators:
    - `PythonOperator`, `BashOperator`, `DummyOperator`, `BranchPythonOperator`
    - `EmailOperator`, `Sensor`, `SubDagOperator` (deprecated but asked)
    - `DockerOperator`, `KubernetesPodOperator`
- Hooks and Connections
    - What are Hooks?
    - Common Hooks: `PostgresHook`, `S3Hook`, `HttpHook`, `MySqlHook`, etc.
- Sensors & Their Types:
    - `ExternalTaskSensor`, `TimeSensor`, `FileSensor`, `S3KeySensor`

---

### 4️⃣ Scheduling & Execution Engine

- Scheduler Internals:
    - How the Scheduler picks DAGs
    - DAG Parsing vs DAG Execution
- Executors:
    - `SequentialExecutor`, `LocalExecutor`, `CeleryExecutor`, `KubernetesExecutor`
    - When to use which (pros/cons, tradeoffs)
- Task Instances & Queues
- Pools and Priorities: `pool`, `priority_weight`, `concurrency`

---

### 5️⃣ XComs & Data Passing

- What is XCom? Use Cases
- Push and Pull: `xcom_push`, `xcom_pull`
- When NOT to use XCom (avoid large data)
- Alternatives to XCom

---

### 6️⃣ Dependency Management

- `depends_on_past`, `wait_for_downstream`, `TriggerRule`
- `ExternalTaskSensor` for cross-DAG dependencies
- DAG chaining
- Conditional execution with `BranchPythonOperator`

---

### 7️⃣ Real-Time Use Cases & Design Scenarios

- Orchestrating ETL pipelines (daily/hourly jobs)
- Event-driven pipelines (S3 upload, Kafka topic, etc.)
- Backfilling with `catchup`, `start_date`, `end_date`, `retries`
- Dynamic DAG generation
- Airflow for ML/AI workflows

---

### 8️⃣ Scaling & Deployment

- Horizontal scaling using **CeleryExecutor**
- KubernetesExecutor for container-native scheduling
- DAG versioning and Git integration
- Deploying DAGs securely in CI/CD (Git + Airflow)
- Environment setup:
    - `airflow.cfg`, `webserver_config.py`, `.env`

---

### 9️⃣ Monitoring, Logging & Observability

- Web UI and Logs
- Retry strategy: `retries`, `retry_delay`, `max_active_runs`
- SLA Misses and Notifications
- Logging handlers (S3, GCS, local)
- Airflow Metrics with Prometheus & Grafana
- Alerts via Slack/Email/HTTP Callbacks

---

### 🔟 Security, Extensibility, and Best Practices

- RBAC (Role-Based Access Control)
- Secrets backend: AWS Secrets Manager, HashiCorp Vault
- Avoiding anti-patterns:
    - Large XCom data
    - Complex DAGs vs smaller composable DAGs
    - Writing logic inside DAG definitions
- Custom plugins: creating custom Operators, Hooks, Sensors

---

### 🔁 Bonus: Common Interview/Scenario-Based Questions

- How would you backfill missed DAGs for the last 30 days safely?
- How to trigger a DAG on an S3 file upload?
- What’s the difference between `depends_on_past` and `wait_for_downstream`?
- How to ensure task A runs only if task B in another DAG succeeds?
- How to scale an Airflow setup from a single box to high-availability?