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

### 2. Monitoring & Observability

- Observes other containers
- Does not affect service state
- Examples: Uptime monitoring, dashboards, log aggregation

### 3. Experimental / Sandbox

- Short-lived, isolated
- No critical data
- Used for testing, learning, or evaluation

---

## Resource Management

- CPU, memory, and storage allocated at LXC level
- Docker containers inherit LXC limits
- Over-provisioning avoided
- Monitoring containers prioritized for visibility

---

## Lifecycle Rules

1. **Create**
   - Docker container built and assigned class inside LXC
2. **Promote**
   - Validated containers moved from experimental to core or monitoring
3. **Operate**
   - Containers monitored, updated, and maintained
4. **Retire**
   - Containers removed
   - Volumes archived or deleted based on policy

---

## Notes

- Running Docker outside LXC is forbidden
- All Docker workloads must follow lifecycle and class rules
- Observability and isolation are mandatory
- Deviations require an ADR
