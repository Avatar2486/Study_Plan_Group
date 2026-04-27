# Docker

### **📌 Core Docker Concepts (Must-Know)**

✅ **1️⃣ What is Docker?**

- Why use containers? Difference between VMs and Containers
- Benefits: Isolation, Portability, Scalability

✅ **2️⃣ Docker Architecture & Internals**

- **Docker Daemon** (Manages Docker objects)
- **Docker CLI** (Command-line interface)
- **Docker Engine** (Runs containers)
- **Container vs Image vs Layer**
- **How Union File System Works in Docker**

✅ **3️⃣ Docker Installation & Setup**

- Install Docker on Windows, Linux, Mac
- Basic Docker Commands (`docker run`, `docker ps`, `docker stop`)

---

### **🔥 Images & Containers (FAANG-Level)**

✅ **4️⃣ Docker Images & Layers**

- **Dockerfile** (How to write an optimized Dockerfile)
- **Build Context & `.dockerignore`**
- **Multi-Stage Builds** (Reduce image size)
- **Alpine vs Ubuntu vs Debian base images**

✅ **5️⃣ Container Lifecycle Management**

- **Start, Stop, Restart, Remove Containers**
- **Inspecting Logs & Debugging (`docker logs`, `docker exec`)**
- **Persistent Storage: Volumes vs Bind Mounts**

✅ **6️⃣ Networking in Docker**

- **Bridge Network (Default)**
- **Host Network**
- **Overlay Network (For Swarm Mode)**
- **How Containers Communicate Internally (`docker network inspect`)**

---

### **🔥 Docker in Production (FAANG-Level Must-Know)**

✅ **7️⃣ Docker Compose (Multi-Container Applications)**

- **Writing `docker-compose.yml`**
- **Scaling Services (`docker-compose up --scale`)**
- **Environment Variables & Secrets in Compose**

✅ **8️⃣ Docker Swarm & Kubernetes Basics**

- **What is Docker Swarm?**
- **Scaling & Load Balancing**
- **Introduction to Kubernetes (Why Use Kubernetes Instead of Swarm?)**

✅ **9️⃣ Docker Security**

- **Container Security Best Practices**
- **Avoid Running as Root (`USER` in Dockerfile)**
- **Scanning Images for Vulnerabilities (`docker scan`)**
- **Docker Seccomp & AppArmor for Process Isolation**

✅ **🔟 Docker Performance Optimization**

- **Reduce Image Size (`.dockerignore`, Multi-Stage Builds)**
- **Efficient Caching in Dockerfile (`COPY` vs `ADD`)**
- **Optimizing Memory & CPU Usage (`docker update`, `cgroups` & `limits`)**

---

### **🔥 FAANG-Level Practice Questions**

✅ **Basic**

1️⃣ Explain the difference between **Docker and a Virtual Machine**.

2️⃣ How do you **list all running & stopped containers**?

3️⃣ What happens internally when you run `docker run hello-world`?

✅ **Intermediate**

4️⃣ How do you **copy a file from a running Docker container to the host**?

5️⃣ How do you **reduce Docker image size**?

6️⃣ How do you **set environment variables in a Docker container**?

✅ **Advanced (FAANG-Level)**

7️⃣ **How would you debug a failing container?**

8️⃣ **What happens when a container crashes? How do you auto-restart it?**

9️⃣ **How does Docker handle networking internally?**

🔟 **Explain the difference between Bind Mounts and Volumes. Which one is better for production?**

1️⃣1️⃣ **How would you deploy a microservices architecture using Docker?**

---

###