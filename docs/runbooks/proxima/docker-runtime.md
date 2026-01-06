# Runbook – Docker Runtime in LXC Containers on Proxima

## Purpose

This runbook defines the **standards and procedures for running Docker** inside
LXC containers on Proxima.

It ensures all Docker workloads are consistent, isolated, and maintainable.

---

## Scope

- Docker inside LXC containers only
- Persistent and ephemeral Docker workloads
- Integration with monitoring and observability
- Lifecycle management

Out of scope:

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

   - Core services, monitoring, and experimental workloads have separate
     containers
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

#### Example: Gitea Deployment

**Container:** `core-services`  
**Role:** Git service (self-hosted)  
**Admin Email:** `lyra@proxima.com`  
**Ports:**

- Web UI: `3000` → access via `http://192.168.8.21:3000`
- SSH: `2222` → Git over SSH

**Persistent Volumes:**

```text
/srv/gitea/data   → Git repositories
/srv/gitea/config → Gitea configuration
/srv/gitea/logs   → Logs
```

#### Gitea container deployment snippet

docker run -d \
 --name gitea \
 -p 3000:3000 \
 -p 2222:22 \
 -v /srv/gitea/data:/data \
 -v /srv/gitea/config:/etc/gitea \
 -v /srv/gitea/logs:/var/log/gitea \
 --restart unless-stopped \
 gitea/gitea:latest
