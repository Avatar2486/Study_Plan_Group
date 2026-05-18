# Kubernetes — Answer Bank

---

**Q: What are the control plane components?**

**Short:** API Server (entry point), etcd (state store), Scheduler (assigns pods to nodes), Controller Manager (runs controllers).

**Detailed:**
- **API Server:** All requests go through it. Validates, stores to etcd, serves REST API. `kubectl` talks to this.
- **etcd:** Distributed key-value store. Single source of truth for all cluster state. Uses Raft consensus.
- **Scheduler:** Watches for unscheduled pods, picks the best node based on resources, affinity, taints.
- **Controller Manager:** Runs control loops — ReplicaSet controller (ensure N pods running), Node controller (detect failures), Job controller, etc.

---

**Q: What is the difference between Deployment, StatefulSet, and DaemonSet?**

**Short:** Deployment = stateless apps. StatefulSet = stateful apps with stable identity + storage. DaemonSet = one pod per node.

**Detailed:**
| | Deployment | StatefulSet | DaemonSet |
|--|--|--|--|
| Pod identity | Random names | Stable ordered names (pod-0, pod-1) | One per node |
| Storage | Shared or no persistence | Stable persistent volume per pod | Usually no |
| Scaling | Any order | Ordered (0→1→2) | Node count determines count |
| Use case | Web servers, APIs | Databases, Kafka, Zookeeper | Log agents, monitoring, networking |

StatefulSets guarantee: stable DNS name, stable storage, ordered startup/shutdown.

---

**Q: What is the difference between ClusterIP, NodePort, and LoadBalancer services?**

**Short:** ClusterIP = internal only. NodePort = expose on each node's IP. LoadBalancer = cloud load balancer for external traffic.

**Detailed:**
| Type | Accessible From | Use Case |
|------|----------------|---------|
| **ClusterIP** | Inside cluster only | Internal service-to-service communication |
| **NodePort** | Outside cluster via `NodeIP:Port` | Dev/testing, not production |
| **LoadBalancer** | Internet via cloud LB (AWS ELB, GCP LB) | Production external traffic |
| **ExternalName** | DNS alias to external service | Pointing to external databases |

In production: use `LoadBalancer` or `Ingress` (L7 routing with a single LB for multiple services).

---

**Q: How does Horizontal Pod Autoscaler (HPA) work?**

**Short:** HPA watches metrics (CPU, memory, custom) and scales pod replicas up/down to maintain target utilization.

**Detailed:**
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: app
  minReplicas: 2
  maxReplicas: 20
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
```
- Requires `metrics-server` installed in cluster.
- Checks every 15 seconds by default. Scale-up is fast; scale-down has a cooldown (5 min default).

---

**Q: How do you debug a CrashLoopBackOff?**

**Short:** Pod keeps crashing and restarting. Check logs → describe pod → check exit code → fix the root cause.

**Detailed:**
```bash
kubectl get pods                        # see CrashLoopBackOff status
kubectl describe pod <pod-name>         # events, last state, exit code
kubectl logs <pod-name>                 # current container logs
kubectl logs <pod-name> --previous      # logs from last crashed container

# Exit code clues:
# 0  = clean exit (misconfigured CMD?)
# 1  = application error
# 137 = OOMKilled (out of memory → increase limits)
# 139 = segfault
# 143 = SIGTERM not handled
```
Common causes: wrong image, missing env vars, wrong command, OOM, health check failing, missing ConfigMap/Secret.

---

**Q: What is RBAC in Kubernetes?**

**Short:** Role-Based Access Control — define what actions (verbs) on what resources are allowed for which subjects (users, service accounts).

**Detailed:**
```yaml
# Role — namespace scoped
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
---
# RoleBinding — attach Role to a subject
kind: RoleBinding
subjects:
- kind: ServiceAccount
  name: my-app
roleRef:
  kind: Role
  name: pod-reader
```
- `Role` + `RoleBinding` = namespace scope.
- `ClusterRole` + `ClusterRoleBinding` = cluster-wide scope.

---

**Q: What is the difference between a PersistentVolume and a PersistentVolumeClaim?**

**Short:** PV = cluster-wide storage resource (provisioned by admin). PVC = request for storage by a pod (the pod asks for X GB with Y access mode).

**Detailed:**
```yaml
# PVC — pod requests storage
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: db-storage
spec:
  accessModes: [ReadWriteOnce]
  resources:
    requests:
      storage: 10Gi
  storageClassName: gp3
---
# Pod uses PVC
volumes:
- name: db-vol
  persistentVolumeClaim:
    claimName: db-storage
```
With `StorageClass`, PVs are dynamically provisioned when a PVC is created. No need to pre-create PVs manually.

---

**Q: What is a rolling update and how does Kubernetes do it?**

**Short:** Gradually replaces old pods with new ones — zero downtime. Old pods stay until new ones are healthy.

**Detailed:**
```yaml
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxSurge: 1         # max extra pods during update
    maxUnavailable: 0   # no pods unavailable at any time
```
- Kubernetes creates 1 new pod → waits until ready (passes readinessProbe) → deletes 1 old pod → repeat.
- Rollback: `kubectl rollout undo deployment/app`
- Blue-Green: deploy new version alongside old, then switch traffic.
- Canary: send small % of traffic to new version first.

---

**Q: What is etcd and why is backing it up important?**

**Short:** etcd is the cluster's brain — stores all state (pods, deployments, secrets, configs). If corrupted with no backup, the entire cluster state is lost.

**Detailed:**
```bash
# Backup etcd
ETCDCTL_API=3 etcdctl snapshot save snapshot.db \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key

# Restore
etcdctl snapshot restore snapshot.db --data-dir=/var/lib/etcd-backup
```
Run etcd with 3 or 5 members (odd number for quorum). Back up before every cluster upgrade.

---

**Q: What is a NetworkPolicy?**

**Short:** Defines which pods can communicate with which other pods/services — like a firewall for pods. Default: all traffic allowed.

**Detailed:**
```yaml
# Deny all ingress to app, except from frontend
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-frontend-only
spec:
  podSelector:
    matchLabels:
      app: backend
  policyTypes: [Ingress]
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: frontend
```
Requires a CNI plugin that supports NetworkPolicy (Calico, Cilium). Flannel alone does NOT enforce NetworkPolicy.

---

## Links
- [[Study Plan/Kubernetes]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
