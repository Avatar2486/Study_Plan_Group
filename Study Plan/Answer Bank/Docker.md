# Docker — Answer Bank

---

**Q: What is the difference between Docker and a Virtual Machine?**

**Short:** VMs virtualize the hardware (full OS per VM). Docker containers share the host OS kernel — lighter, faster to start, less memory.

**Detailed:**
| | Docker Container | Virtual Machine |
|--|--|--|
| OS | Shares host kernel | Full OS per VM |
| Start time | Milliseconds | Minutes |
| Size | MBs | GBs |
| Isolation | Process/namespace level | Hardware level |
| Overhead | Minimal | Significant |

Docker uses Linux namespaces (PID, network, mount, UTS) and cgroups (resource limits) for isolation. VMs use a hypervisor.

---

**Q: What happens when you run `docker run hello-world`?**

**Short:** Docker CLI → Docker daemon → checks local image → pulls from registry → creates container → runs process → outputs text → exits.

**Detailed:**
1. CLI sends `POST /containers/create` to Docker daemon via Unix socket
2. Daemon checks local image cache — not found
3. Pulls `hello-world` image from Docker Hub (registry)
4. Creates a container (assigns namespace, cgroup, writable layer)
5. Starts the container (runs the default CMD in the image)
6. Process outputs text, exits with code 0
7. Container is in `Exited` state (not deleted unless `--rm` flag used)

---

**Q: How do you write an optimized Dockerfile?**

**Short:** Order layers from least to most frequently changed. Use multi-stage builds. Use `.dockerignore`. Run as non-root.

**Detailed:**
```dockerfile
# Multi-stage build — final image has no build tools
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./          # copy deps first (cached layer)
RUN npm ci --only=production   # cached unless package.json changes
COPY . .

FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app .
USER node                      # non-root
EXPOSE 3000
CMD ["node", "server.js"]
```
- `COPY package.json ./` then `RUN npm install` before `COPY . .` — npm install layer is cached until package.json changes.
- Alpine base = ~5MB vs Ubuntu ~70MB.

---

**Q: What is the difference between Volumes and Bind Mounts?**

**Short:** Volumes are managed by Docker (stored in Docker's area). Bind Mounts map a specific host path into the container.

**Detailed:**
| | Volume | Bind Mount |
|--|--|--|
| Managed by | Docker | Host OS |
| Host path | Docker's `/var/lib/docker/volumes/` | Any host path you specify |
| Portability | High — works the same on any host | Low — host path must exist |
| Use in production | ✓ Preferred | Not recommended (path coupling) |
| Use in dev | Fine | ✓ For live reloading code |

```bash
docker run -v myvolume:/app/data nginx          # named volume
docker run -v $(pwd)/src:/app/src nginx          # bind mount (dev)
```

---

**Q: How do you debug a failing container?**

**Short:** Check logs → inspect exit code → exec into container → check events → rebuild with debugging tools.

**Detailed:**
```bash
docker logs <container>              # stdout/stderr
docker logs --tail 50 -f <container> # follow last 50 lines
docker inspect <container>           # full config + exit code, state
docker stats <container>             # CPU/memory usage live
docker exec -it <container> sh       # get shell inside running container

# If container exits immediately:
docker run -it --entrypoint sh <image>  # override entrypoint, start shell

# Check events
docker events --since '1h'
```

---

**Q: How do you auto-restart a crashed container?**

**Short:** Use `--restart` policy: `no` (default), `always`, `unless-stopped`, `on-failure[:N]`.

**Detailed:**
```bash
docker run --restart=always nginx          # always restart, even on Docker daemon restart
docker run --restart=unless-stopped nginx  # restart unless manually stopped
docker run --restart=on-failure:3 nginx    # restart up to 3 times on non-zero exit

# In docker-compose.yml:
services:
  app:
    restart: unless-stopped
```
In production use orchestration (Docker Swarm, Kubernetes) — they have richer health-check-based restart policies.

---

**Q: How does Docker networking work internally?**

**Short:** Each container gets a virtual network interface. The default `bridge` network uses Linux bridge + iptables for routing. Containers on the same bridge network communicate by container name.

**Detailed:**
- **Bridge (default):** Virtual bridge `docker0`. Containers get IPs like `172.17.0.x`. NAT for outbound. Port mapping via iptables.
- **Host:** Container uses host's network stack directly. No isolation. Fastest.
- **Overlay:** Multi-host networking (Docker Swarm). Uses VXLAN encapsulation.
- **None:** No networking. Fully isolated.

```bash
docker network create mynet
docker run --network=mynet --name=db postgres
docker run --network=mynet app  # can reach db at hostname "db"
```

---

**Q: How do you reduce Docker image size?**

**Short:** Multi-stage builds, Alpine base image, `.dockerignore`, combine RUN commands, remove caches.

**Detailed:**
```dockerfile
# Combine RUN layers
RUN apt-get update && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/*    # clean cache in same layer

# Use .dockerignore
# node_modules, .git, *.log, .env

# Multi-stage — build image vs runtime image
FROM golang:1.21 AS build
RUN go build -o app .

FROM alpine:3.19
COPY --from=build /app .   # only the binary, not the full Go toolchain
```

---

**Q: How do you use environment variables and secrets in Docker?**

**Short:** Use `-e` flag, `.env` files, or Docker secrets. Never hardcode secrets in Dockerfile.

**Detailed:**
```bash
# Single env var
docker run -e DATABASE_URL=postgres://... app

# Env file
docker run --env-file .env app

# docker-compose.yml
services:
  app:
    env_file: .env
    environment:
      - NODE_ENV=production

# Docker Swarm secrets (production)
echo "mypassword" | docker secret create db_password -
docker service create --secret db_password app
# Secret available at /run/secrets/db_password inside container
```

---

**Q: What is docker-compose and what is it used for?**

**Short:** Tool to define and run multi-container applications from a single `docker-compose.yml` file.

**Detailed:**
```yaml
version: '3.9'
services:
  app:
    build: .
    ports: ["3000:3000"]
    environment:
      - DB_URL=postgres://user:pass@db:5432/mydb
    depends_on: [db]
    restart: unless-stopped

  db:
    image: postgres:15
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: pass

volumes:
  pgdata:
```
```bash
docker-compose up -d       # start in background
docker-compose down -v     # stop + remove volumes
docker-compose logs -f app # follow app logs
```

---

## Links
- [[Study Plan/Docker]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
