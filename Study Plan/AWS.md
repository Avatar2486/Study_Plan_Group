# AWS

---

# 🟢 **Phase 1: Core AWS Foundations**

### 1️⃣ Cloud Computing Basics

- Cloud models: IaaS, PaaS, SaaS, FaaS
- Deployment models: public, private, hybrid, multi-cloud
- Shared responsibility model
- Elasticity, scalability, high availability, disaster recovery

---

### 2️⃣ AWS Global Infrastructure

- Regions & Availability Zones (AZs)
- Edge Locations (CloudFront, caching)
- Data residency & latency considerations
- Multi-region architecture basics

---

### 3️⃣ IAM & Security Fundamentals

- IAM users, groups, roles, policies
- Least privilege principle
- MFA & password policies
- Service-linked roles (Lambda, EC2, ECS)

---

# 🔵 **Phase 2: Networking & Core Infrastructure**

### 1️⃣ VPC & Networking

- VPC design: CIDR planning, subnets (public, private, isolated)
- Internet Gateway, NAT Gateway, Transit Gateway
- VPC Endpoints: S3/DynamoDB Gateway, Interface endpoints, PrivateLink
- Security groups vs NACLs
- Elastic IPs, Route Tables, peering connections

---

### 2️⃣ Route 53 & CloudFront

- Route 53: public vs private hosted zones, routing policies (latency, weighted, geo, failover)
- Health checks & DNS failover
- CloudFront: CDN, caching, origin failover, signed URLs/cookies, Lambda@Edge

---

### 3️⃣ Hybrid & Global Connectivity

- Direct Connect vs VPN vs Transit Gateway
- Multi-region active-active architectures with Route 53 + Global Accelerator
- Cross-region replication for S3 & databases

---

# 🟡 **Phase 3: Compute & Serverless**

### 1️⃣ EC2

- Instance types & families (general-purpose, compute/memory-optimized, GPU, etc.)
- AMIs, key pairs, Elastic IPs
- Auto Scaling Groups: scaling policies, launch configurations
- Spot, On-demand, Reserved Instances, Savings Plans
- Load balancers: ALB (L7), NLB (L4), Gateway LB

---

### 2️⃣ Lambda

- Event triggers (S3, DynamoDB, API Gateway, EventBridge)
- Cold start, concurrency limits, environment variables
- Monitoring & logging (CloudWatch, X-Ray)
- Error handling: DLQ, retries

---

### 3️⃣ Containers (AWS)

- ECS: EC2 vs Fargate launch types, task definitions, service discovery
- App Mesh integration for ECS services
- EKS overview (optional, as a compute alternative)

---

# 🟠 **Phase 4: Storage**

### 1️⃣ S3

- Buckets, versioning, encryption
- Storage classes (Standard, IA, Glacier, Intelligent-Tiering)
- Lifecycle policies & cross-region replication
- Event notifications (Lambda triggers)
- Static website hosting

---

### 2️⃣ EBS, EFS, FSx

- EBS: gp3/io2, snapshots, encryption, performance tuning
- EFS: multi-AZ, throughput & performance modes
- FSx: Windows, Lustre, ONTAP

---

# 🔴 **Phase 5: Databases**

### 1️⃣ Databases

- **RDS / Aurora**: multi-AZ, read replicas, snapshots, failover
- **DynamoDB**: primary/sort key, GSIs/LSIs, TTL, on-demand vs provisioned
- **ElastiCache**: Redis/Memcached for caching

---

# 🟣 **Phase 6: Observability & Monitoring**

### 1️⃣ Monitoring

- **Amazon CloudWatch Metrics**: default metrics, custom metrics, dashboards, alarms
- **Amazon CloudWatch Logs**: log groups, subscription filters, retention policies
- CloudWatch Agent vs FluentBit: EC2 & container logging

---

### 2️⃣ Tracing & Observability

- **AWS X-Ray**: distributed tracing, service maps, annotations, segments
- OpenTelemetry: metrics & traces integration for ECS/EKS (optional)
- Centralized Logging: CloudWatch Logs → OpenSearch/ELK for analytics

---

### 3️⃣ Security & Threat Detection

- GuardDuty: anomaly detection, threat intelligence
- Inspector: vulnerability scanning for EC2 & container images
- Security Hub: central security posture & compliance dashboard
- Detective: root cause analysis of security findings
- EventBridge: event-driven monitoring & automation

---

# 🔐 **Phase 7: Security & Compliance**

### 1️⃣ Security & Compliance

- Encryption at rest: KMS, SSE-S3, RDS encryption
- Encryption in transit: TLS/HTTPS, VPN, PrivateLink
- AWS WAF, Shield (DDoS), Security Hub, GuardDuty, Inspector, Detective
- Logging & auditing: CloudTrail, CloudWatch Logs, Config, Audit Manager

---

# ⚙️ **Phase 8: CI/CD & Infrastructure Automation**

### 1️⃣ CI/CD Pipelines

- CodePipeline: pipeline stages, source → build → deploy
- CodeBuild: buildspec.yml, environment variables, caching
- CodeDeploy: blue/green, canary, in-place deployments
- Integration with GitHub/GitLab/Bitbucket
- Zero-downtime deployments: traffic shifting with ALB/NLB

---

### 2️⃣ Infrastructure as Code (IaC)

- **AWS CloudFormation**: templates, nested stacks, stack sets, drift detection
- **AWS CDK**: high-level constructs, programming language support, multi-account/multi-region deployment
- **Terraform**: state management, modules, remote backends, workspaces
- IaC Best Practices: modularization, versioning, testing

---

### 3️⃣ Automation & Governance

- Systems Manager (SSM): automation runbooks, session manager, patching
- AWS Config: drift detection, compliance rules, conformance packs
- AWS Control Tower: multi-account setup, landing zones, guardrails
- Service Catalog: standardized, pre-approved resources for teams
- Backup & DR automation: AWS Backup, cross-region replication, scheduled snapshots

---

# 📈 **Phase 9: Scaling, High Availability & Disaster Recovery**

### 1️⃣ Auto Scaling

- EC2 Auto Scaling Groups: scaling policies (target tracking, step scaling), lifecycle hooks
- ECS Task Auto Scaling: service scaling with CloudWatch metrics
- RDS & Aurora: read replicas, multi-AZ failover, global databases

---

### 2️⃣ Multi-AZ vs Multi-Region Architecture

- Multi-AZ deployments: high availability within region
- Multi-region deployments: active-active vs active-passive
- Global services: Route 53 latency-based routing, CloudFront for edge delivery
- Disaster Recovery Strategies: pilot-light, warm standby, backup & restore, cross-region replication

---

### 3️⃣ Cost Optimization

- Instance types: On-demand vs Spot vs Reserved vs Savings Plans
- S3 storage tiers: Standard, IA, Glacier, Intelligent-Tiering
- Auto Scaling & right-sizing: EC2, RDS, Lambda concurrency
- Monitoring & alerts: Cost Explorer, budgets, anomaly detection

---

# 🚀 **Phase 10: Advanced Architectures & Well-Architected Patterns**

### 1️⃣ Event-Driven Architectures

- SNS + SQS: fan-out, decoupling, DLQs, FIFO vs Standard queues
- EventBridge: event bus, cron scheduling, multi-target rules
- Serverless pipelines: S3 → Lambda → DynamoDB/RDS → Redshift/ElasticSearch

---

### 2️⃣ Data Lakes & Analytics

- S3 Data Lake: partitioning, lifecycle, versioning
- Glue: ETL, crawlers, jobs
- Athena: serverless query
- Redshift & EMR: batch & real-time analytics, cost-efficient queries

---

### 3️⃣ Hybrid & Multi-Cloud

- AWS Outposts: on-prem AWS services
- Local Zones & Wavelength: low-latency applications
- Hybrid networking: Direct Connect, VPN, Transit Gateway, Route 53 Resolver
- Cross-region replication & failover

---

### 4️⃣ Well-Architected Framework

- Operational Excellence: monitoring, automation, runbooks
- Security: IAM, encryption, auditing, compliance
- Reliability: HA, DR, multi-AZ/multi-region, failover tests
- Performance Efficiency: right-sizing, caching, auto scaling, CDN
- Cost Optimization: Savings Plans, reserved capacity, tiered storage, spot instances

---

### 5️⃣ Global Application Design

- Multi-region apps: Aurora Global DB, DynamoDB global tables
- Latency optimization: CloudFront, Global Accelerator
- Cross-region replication & consistency: S3, RDS, DynamoDB

---