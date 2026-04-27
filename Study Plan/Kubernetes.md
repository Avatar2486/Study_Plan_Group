# Kubernetes

---

# 🚀 **Kubernetes Roadmap**

## **1️⃣ Introduction & Basics**

- **Why Kubernetes?** Problems it solves (manual scaling, resilience, deployments)
- **Containers vs VMs vs Kubernetes**
- **Core benefits:** scalability, resilience, declarative infra, portability
- **Kubernetes versions & community ecosystem**

---

## **2️⃣ Kubernetes Architecture**

### **Control Plane Components**

- API Server
- Scheduler
- Controller Manager
- etcd (state store) → MVCC, snapshots, restore, high availability

### **Worker Node Components**

- Kubelet
- Kube-proxy (iptables vs IPVS)
- Container Runtime (Docker, containerd, CRI-O, why Docker deprecated)

### **Pod Lifecycle & Scheduling**

- Pod phases: Pending, Running, Succeeded, Failed
- Init Containers
- Pod scheduling basics
- **Taints & Tolerations**, **Node/Pod Affinity & Anti-Affinity**

---

## **3️⃣ Kubernetes Objects (Core Building Blocks)**

- Pod (single & multi-container)
- ReplicaSet
- Deployment
- Service (ClusterIP, NodePort, LoadBalancer, ExternalName)
- ConfigMap & Secret
- PersistentVolume & PersistentVolumeClaim

---

## **4️⃣ Workloads & Controllers**

### **Pod & Multi-Container Patterns**

- Sidecar pattern
- Ambassador pattern
- Adapter pattern

### **Deployment Strategies**

- Rolling Update
- Blue-Green
- Canary Deployments
- Pausing/Resuming Deployments
- Argo Rollouts / Flagger for progressive delivery

### **Stateful Workloads**

- StatefulSets & Headless Services
- DaemonSets
- Jobs & CronJobs
- Running databases (Postgres, MongoDB, Cassandra)
- Volume resizing & backup/restore

---

## **5️⃣ Networking in Kubernetes**

### **Cluster Networking**

- Pod-to-Pod communication
- Service-to-Pod communication
- CNI plugins (Flannel, Calico, Cilium, Weave)
- kube-proxy internals (iptables, IPVS)

### **Service Discovery**

- CoreDNS
- Environment variables vs DNS resolution
- Headless Services & DNS SRV records

### **Ingress & Load Balancing**

- Ingress Controller (NGINX, Traefik, HAProxy, Istio gateway)
- Path-based routing
- TLS termination

### **Network Policies**

- Egress & Ingress controls
- Isolation between pods & namespaces

---

## **6️⃣ Storage & Data Management**

- Volumes (ephemeral vs persistent)
- PersistentVolumes (PV) & PersistentVolumeClaims (PVC)
- StorageClass & Dynamic Provisioning
- CSI Drivers
- Volume snapshot & restore

---

## **7️⃣ Config & Secrets Management**

- ConfigMaps vs Secrets
- Environment variables vs mounted files
- Secret encryption at rest (KMS, Vault integration)
- Sealed Secrets & External Secrets Operator

---

## **8️⃣ Security in Kubernetes**

### **Authentication & Authorization**

- RBAC (Roles, ClusterRoles, RoleBindings)
- Service Accounts
- API Access Control

### **Pod Security**

- Security Context
- Pod Security Admission / Policies
- Running non-root containers
- Network Policies

### **Cluster Security**

- Audit Logs & API auditing
- TLS everywhere (control plane & data plane)
- Image scanning & vulnerability checks
- Admission Controllers (OPA/Gatekeeper, Kyverno, Falco)

---

## **9️⃣ Scaling & High Availability**

### **Scaling Applications**

- Horizontal Pod Autoscaler (HPA)
- Vertical Pod Autoscaler (VPA)
- Cluster Autoscaler

### **High Availability**

- HA control plane setup
- Multi-zone, multi-region clusters
- etcd backup & restore
- Zero-downtime upgrades

---

## **10️⃣ Observability & Debugging**

- Logging (kubectl logs, exec, describe)
- Metrics Server
- Prometheus + Grafana
- EFK/ELK stack (Elasticsearch, Fluentd, Kibana)
- Distributed Tracing (Jaeger / OpenTelemetry)
- Debugging Pods (CrashLoopBackOff, ImagePullBackOff)
- Network debugging (`kubectl exec`, tcpdump, curl inside pods)

---

## **11️⃣ Advanced Kubernetes (FAANG-Level)**

### **Operators & CRDs**

- Custom Resource Definitions (CRD)
- Operators (automation of apps like DBs, Kafka, Prometheus)

### **Service Mesh**

- Istio, Linkerd, Consul Connect
- Sidecar proxy (Envoy)
- Features: mTLS, traffic shifting, observability

### **Multi-Tenancy & Namespaces**

- Resource Quotas & LimitRanges
- Namespace isolation

### **Multi-Cluster & Hybrid Cloud**

- Federation
- Cluster API
- Service discovery across clusters

### **CI/CD with Kubernetes**

- GitOps (ArgoCD, Flux)
- Helm charts & Kustomize
- Progressive delivery

### **Cost Optimization**

- Right-sizing pods
- Spot instances
- Autoscaling with cost awareness
- Bin packing strategies

---

## **12️⃣ Kubernetes API & Controller Internals**

- Controller pattern & informers
- Work queues & event loops
- Leader election in controllers
- How kube-proxy & network routing work internally
- etcd internals: MVCC, compaction, snapshots

---

## **13️⃣ Production Best Practices**

- Node & control plane upgrades
- Cluster monitoring & alerting
- Security hardening & audits
- Backup & disaster recovery
- Multi-tenant design patterns

---

## **14️⃣ FAANG-Level Practice Questions**

### **Basic**

1. Pod vs Container
2. Service vs Ingress
3. Kubernetes networking basics

### **Intermediate**

1. Scaling applications automatically
2. StatefulSet vs Deployment
3. `kubectl apply -f` workflow

### **Advanced**

1. Leader election in controllers
2. etcd state storage & recovery
3. kube-proxy internals (iptables/IPVS)
4. Multi-tenant cluster design for 100+ teams

---