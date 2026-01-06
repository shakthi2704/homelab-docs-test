# Runbook – Docker Runtime in LXC Containers on Proxima

## Purpose

This runbook defines the **standards and procedures for running Docker** inside LXC containers on Proxima.  
It ensures all Docker workloads are consistent, isolated, and maintainable.

---

## Scope

- Docker inside LXC containers only
- Persistent and ephemeral Docker workloads
- Integration with monitoring and observability
- Lifecycle management

**Out of scope:**

- Host-level Docker installation (forbidden)
- Docker image design or build processes
- Networking configuration beyond internal container networking

---

## Docker Runtime Principles

1. **LXC-First Isolation**

   - Docker runs only inside LXC containers
   - Each LXC container has a single responsibility class
   - Containers are ephemeral or persistent depending on class

2. **Persistent Volumes**

   - Docker containers never store authoritative data internally
   - All volumes are mapped to Proxima’s storage pool
   - Volume sharing is limited to authorized services

3. **Monitoring**

   - Docker containers are observable from monitoring LXC
   - Logs, metrics, and status must be exposed but cannot interfere

4. **Service Class Alignment**

   - Core services, monitoring, and experimental workloads have separate containers
   - No cross-class interference

5. **Operational Boundaries**
   - Containers follow lifecycle: create → promote → operate → retire
   - Updates must respect boundaries and document changes
   - Ephemeral containers are deleted without impacting persistent workloads

---

## Docker Container Categories

### 1. Core Services

- Persistent workloads
- Examples: Git services, CI services, developer tools

**Example: Gitea Deployment**  
**Container:** `core-services`  
**Role:** Git service (self-hosted)  
**Admin Email:** `lyra@proxima.com`

**Ports:**

| Service | Container Port | Host Port | Notes                                 |
| ------- | -------------- | --------- | ------------------------------------- |
| Web UI  | 3000           | 3000      | Access via `http://192.168.8.21:3000` |
| SSH     | 22             | 2222      | Git over SSH                          |

**Persistent Volumes:**

```text
/srv/gitea/data   → Git repositories
/srv/gitea/config → Gitea configuration
/srv/gitea/logs   → Logs
uptime-kuma-data  → stores Uptime Kuma database
pulse-data        → stores Pulse configuration & metrics
dozzle-data       → stores Dozzle logs (optional)
```

## Deployment Steps

### 1. Core Services

```text
pct create 101 /var/lib/vz/template/cache/ubuntu-22.04-standard_22.04-1_amd64.tar.zst \
  -hostname monitor-services \
  -cores 2 \
  -memory 2048 \
  -swap 1024 \
  -net0 name=eth0,bridge=vmbr0,ip=192.168.8.22/24,gw=192.168.8.1,firewall=0 \
  -features nesting=1 \
  -ostype ubuntu \
  -unprivileged 1 \
  -rootfs pve-data:30

```

### 2. Deploy Core Services and Monitoring Containers:

```text
# Gitea
docker run -d \
  --name gitea \
  -p 3000:3000 \
  -p 2222:22 \
  -v /srv/gitea/data:/data \
  -v /srv/gitea/config:/etc/gitea \
  -v /srv/gitea/logs:/var/log/gitea \
  --restart unless-stopped \
  gitea/gitea:latest

# Uptime Kuma
docker run -d \
  --name uptime-kuma \
  --restart unless-stopped \
  -p 8081:3001 \
  -v uptime-kuma-data:/app/data \
  louislam/uptime-kuma

# Pulse
docker run -d \
  --name pulse \
  --restart unless-stopped \
  -p 8082:7655 \
  -v pulse-data:/data \
  rcourtman/pulse:latest

# Dozzle
docker run -d \
  --name dozzle \
  --restart unless-stopped \
  -p 8083:8080 \
  -v dozzle-data:/app/data \
  amir20/dozzle:latest

```
