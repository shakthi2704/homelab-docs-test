# Homelab & Development Infrastructure – Container Responsibility Map

## Document Context

This document defines **where containers are allowed to run** and **what class
of responsibility each container may have**.

It builds on:

- `00-overview.md`
- `01-architecture.md`
- `02-node-roles.md`

This file establishes **enforceable placement rules** for all containers.

---

## Container Design Principles

All containers in this environment follow these principles:

- Containers are long-running, not ad-hoc
- Each container has a single, well-defined purpose
- Containers do not cross responsibility boundaries
- Containers are replaceable; data is not

If a container cannot be clearly categorized, it should not exist.

---

## Container Execution Locations

### Lyra (Development Node)

**Allowed Container Types**

- Local development containers
- Test and sandbox environments
- Temporary build containers

**Characteristics**

- Short-lived
- Developer-initiated
- No persistent data

**Explicitly Disallowed**

- Infrastructure services
- Monitoring tools
- Databases with persistent state

All containers on Lyra are considered **ephemeral**.

---

### Proxima (Runtime Node)

Proxima is the **only node** where persistent containers may run.

Containers on Proxima run **inside LXC containers**.

---

## LXC-Level Responsibility Classes

Each LXC container on Proxima must belong to **one responsibility class**.

### Core Services LXC

**Purpose**

- Host foundational development services

**Container Examples**

- Local Git services
- CI-related services (local)
- Developer tooling services

**Constraints**

- No monitoring workloads
- No experimental services

---

### Monitoring & Observability LXC

**Purpose**

- Visibility into system and service health

**Container Examples**

- Container management UI
- Log aggregation
- Availability monitoring
- System health dashboards

**Constraints**

- Read-only or observational access
- No modification of core service state

---

### Experimental / Sandbox LXC (Optional)

**Purpose**

- Isolated experimentation
- Learning or evaluation workloads

**Characteristics**

- Non-critical
- Easily disposable
- No authoritative data

This class is optional and must never host required services.

---

## Disallowed Patterns

The following are explicitly disallowed:

- Running Docker directly on the Proxmox host
- Mixing monitoring and core services in the same LXC
- Sharing persistent volumes across unrelated containers
- Running persistent services on Lyra or Nova

---

## Promotion Model (High-Level)

Container lifecycle follows a simple model:

1. Develop locally on Lyra
2. Validate behavior
3. Promote to Proxima as a persistent service
4. Retire when no longer needed

Implementation details are defined in runbooks.

---

## Summary

This responsibility map ensures:

- Clean separation of concerns
- Predictable container placement
- Easier scaling and recovery
- Reduced operational risk

When container boundaries are respected, the system remains maintainable.

# Homelab & Development Infrastructure – Container Strategy

## Document Context

This document defines the **containerization strategy** for the homelab and
development infrastructure.

It builds on:

- `00-overview.md`
- `01-architecture.md`
- `02-node-roles.md`
- `03-networking.md`
- `04-storage.md`

This file describes **how containers are classified, placed, and promoted**,
not how they are built or deployed.

---

## Container Strategy Goals

The container strategy is designed to:

- Enforce clear responsibility boundaries
- Keep hosts minimal and predictable
- Support fast development iteration
- Enable safe promotion to persistent runtime

Containers are treated as **first-class runtime units**, not ad-hoc processes.

---

## Container Execution Policy

### Development Containers (Lyra)

**Purpose**

- Local development
- Testing and validation
- Image building

**Characteristics**

- Short-lived
- Developer-initiated
- No authoritative data
- Safe to destroy at any time

All containers on Lyra are considered **ephemeral**.

---

### Runtime Containers (Proxima)

Proxima is the **only location** for persistent containers.

All runtime containers:

- Run inside LXC containers
- Use externalized storage
- Are treated as long-running services

No runtime containers are allowed on Lyra or Nova.

---

## LXC Responsibility Classes

Each LXC container on Proxima must belong to **one responsibility class**.

---

### Core Services LXC

**Purpose**

- Host foundational development services

**Examples**

- Local Git services
- CI-related tooling (local)
- Developer-facing service infrastructure

**Constraints**

- No monitoring workloads
- No experimental services
- Persistent by default

---

### Monitoring & Observability LXC

**Purpose**

- Provide visibility into system and service health

**Examples**

- Container management interfaces
- Log viewers
- Availability monitoring
- Health dashboards

**Constraints**

- Observational access only
- No direct modification of core service state
- Failure must not impact core services

---

### Experimental / Sandbox LXC

**Purpose**

- Learning, testing, and evaluation

**Characteristics**

- Non-critical
- No authoritative data
- Easily disposable

This class is optional and must never host required services.

---

## Container Lifecycle Model

Containers follow a strict lifecycle:

1. **Create**

   - Built and tested locally on Lyra
   - No persistence assumptions

2. **Promote**

   - Approved for long-running use
   - Deployed to Proxima
   - Assigned to the appropriate LXC class

3. **Operate**

   - Monitored and maintained
   - Data persisted externally

4. **Retire**
   - Decommissioned intentionally
   - Data archived or removed as required

Lifecycle procedures are defined in runbooks.

---

## Disallowed Patterns

The following patterns are explicitly forbidden:

- Running Docker directly on the Proxmox host
- Mixing monitoring and core services in the same LXC
- Sharing persistent volumes across unrelated containers
- Running persistent containers on development machines

Exceptions require an Architecture Decision Record (ADR).

---

## Strategy Sta
