# Homelab & Development Infrastructure – Node Roles

## Document Context

This document defines **explicit responsibilities and boundaries** for each
node in the homelab.  
It builds on `01-architecture.md` and inherits scope and intent from
`00-overview.md`.

This file exists to eliminate ambiguity about **what runs where and why**.

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

- Code authoring and local development

**Responsibilities**

- Writing application code
- Running local Docker containers for development and testing
- Building and validating container images
- Performing Git operations (commit, push, pull)

**Explicit Non-Responsibilities**

- No long-running services
- No production-like workloads
- No persistent infrastructure state
- No monitoring or orchestration services

Lyra is intentionally treated as **disposable** from an infrastructure
perspective.

---

### Proxima — Runtime & Service Host

**Primary Role**

- Hosting all persistent development-related services

**Responsibilities**

- Running LXC containers
- Providing Docker runtime inside LXC
- Hosting Git services (local)
- Hosting monitoring and observability tools
- Maintaining persistent container volumes

**Explicit Non-Responsibilities**

- No application workloads on the Proxmox host
- No developer-facing code editing
- No experimental or ad-hoc containers outside defined services

Proxima is the **authoritative runtime environment**.

---

### Nova — Access & Mobility Node

**Primary Role**

- Administrative and development access

**Responsibilities**

- Accessing services hosted on Proxima
- Performing remote administration
- Acting as a fallback development access point

**Explicit Non-Responsibilities**

- No Docker runtime
- No persistent services
- No authoritative data storage

Nova is an **interface**, not infrastructure.

---

### Rhea — Storage & Media Node

**Primary Role**

- Media and file storage

**Responsibilities**

- Media services (Plex, Jellyfin)
- File sharing

**Explicit Non-Responsibilities**

- No development tooling
- No Git services
- No monitoring or infrastructure workloads

Rhea is **logically isolated** from the development stack.

---

## Cross-Node Interaction Rules

- Lyra and Nova may access services on Proxima
- Proxima does not depend on Lyra or Nova for runtime
- Development workflows must function even if Rhea is unavailable
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
