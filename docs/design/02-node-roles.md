# Homelab & Development Infrastructure – Node Roles

## Document Context

This document defines **explicit responsibilities and boundaries** for each
node in the homelab.

It builds on `01-architecture.md` and inherits scope and intent from
`00-overview.md`.

This file exists to eliminate ambiguity about **what runs where and why**.

> Status: Phase 1 (Day-0 Infrastructure) — Roles validated against deployed reality

---

## Role Design Principles

Each node in the homelab adheres to the following principles:

- One primary responsibility per node
- No overlap of authority
- No hidden secondary roles
- Clear inclusion and exclusion rules

If a workload does not clearly belong to a node, it does not belong anywhere
until the architecture is revisited.

---

## Node Role Definitions

### Lyra — Development Workstation

**Primary Role**

- Development control node and code authoring environment

**Responsibilities**

- Writing application code
- Running local Docker containers for development and testing
- Building and validating container images
- Performing Git operations (commit, push, pull)
- Acting as SSH control node for infrastructure access

**Explicit Non-Responsibilities**

- No long-running services
- No production or production-like workloads
- No persistent infrastructure state
- No monitoring or orchestration services

Lyra is intentionally treated as **disposable** from an infrastructure
perspective.

---

### Proxima — Compute & Runtime Host

**Primary Role**

- Hosting all persistent, production-like development services

**Responsibilities**

- Running LXC containers
- Providing Docker runtime inside LXC containers
- Hosting shared services (e.g., Git, monitoring, internal tools)
- Maintaining runtime isolation and resource governance
- Integrating with external storage providers (Rhea)

**Explicit Non-Responsibilities**

- No application logic on the Proxmox host itself
- No developer-facing code editing
- No ad-hoc or experimental workloads outside defined containers

Proxima is the **authoritative runtime and execution environment**.

---

### Nova — Operations & Access Node

**Primary Role**

- Human-facing operations, access, and visibility

**Responsibilities**

- Documentation authoring and review
- Accessing services hosted on Proxima
- Client communication (Teams, Skype, AnyDesk)
- Monitoring dashboards (web/UI access only)
- Emergency or fallback administrative access

**Explicit Non-Responsibilities**

- No Docker runtime
- No containers or virtual machines
- No persistent services
- No infrastructure authority or secrets management

Nova is an **operations interface**, not part of the compute fabric.

---

### Rhea — Storage & Stateful Services Node

**Primary Role**

- Storage backbone and stateful service host

**Responsibilities**

- Persistent data storage
- Media services (e.g., Plex, Jellyfin)
- File sharing
- Hosting stateful Docker services where appropriate
- Providing mounted storage to Proxima workloads

**Explicit Non-Responsibilities**

- No development tooling
- No Git or CI services
- No monitoring or orchestration authority
- No experimental workloads

Rhea prioritizes **data integrity and stability** over flexibility.

---

## Cross-Node Interaction Rules

- Lyra and Nova may access services hosted on Proxima
- Proxima does not depend on Lyra or Nova for runtime operation
- Proxima may depend on Rhea for persistent storage
- Nova never acts as a dependency for any runtime workload
- No node assumes responsibilities of another node during failure

---

## Role Violation Handling

If a new requirement causes role overlap:

1. Pause implementation
2. Document the conflict
3. Record an Architecture Decision Record (ADR)
4. Update architecture documents only if required

Temporary exceptions are not allowed.

---

## Summary

Clear node roles ensure:

- Predictable behavior
- Easier troubleshooting
- Safer scaling
- Cleaner documentation

When roles are respected, the system remains stable even as tools evolve.
