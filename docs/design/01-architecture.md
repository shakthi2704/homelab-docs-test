# Homelab & Development Infrastructure – Architecture

## Document Context

This document defines the logical and physical architecture of the homelab and
development infrastructure.  
It **inherits scope, intent, and versioning** from `00-overview.md` and must be
read in that context.

This file describes **what exists and how it is structured**, not how it is
installed or operated.

---

## Architecture Overview

The architecture is composed of multiple independent nodes, each with a
single, well-defined responsibility. The system is intentionally simple,
Docker-first, and optimized for developer productivity and long-term stability.

The design avoids unnecessary abstraction layers and favors clarity,
predictability, and isolation.

---

## Node-Level Architecture

### Fixed Node Roles

Each node in the system has a **fixed role** that must not overlap with others.

- Development is isolated from runtime
- Runtime is isolated from storage
- Access is isolated from authority

This prevents role creep and operational ambiguity.

---

### Primary Nodes

#### Lyra — Development Node

- Acts as the **only active development environment**
- Hosts local Docker for build and test workflows
- Has no responsibility for persistent services or infrastructure

Lyra is considered **stateless** from an infrastructure perspective.

---

#### Proxima — Runtime & Control Node

- Acts as the **always-on service host**
- Uses Proxmox VE as a minimal orchestration layer
- Runs all services inside LXC containers
- Provides Docker runtime **inside LXC only**

No application workloads run directly on the Proxmox host.

---

#### Nova — Access Node

- Provides administrative and development access
- Has no authoritative state
- Does not participate in runtime or orchestration

Nova exists to enable mobility and recovery access.

---

#### Rhea — Storage & Media Node

- Dedicated to media services and file sharing
- Explicitly out of scope for development infrastructure
- Has no dependency relationship with development services

Rhea is logically isolated from the dev architecture.

---

## Container & Virtualization Model

### Virtual Machines

- Virtual machines are intentionally **not used** for development workloads
- Reasoning: overhead, slower iteration, unnecessary complexity

---

### LXC Containers

- Proxima hosts multiple LXC containers
- Each LXC has **one primary responsibility**
- Docker is installed and managed **inside LXC containers**

This model provides:

- Process isolation
- Clear fault boundaries
- Minimal overhead compared to VMs

---

## Service Placement Principles

Services are placed according to the following rules:

1. Long-running services run only on Proxima
2. Development tools run only on Lyra
3. Monitoring is isolated from core services
4. Storage authority is never mixed with compute authority

Violations of these rules require an explicit architecture decision.

---

## Storage Architecture

- Persistent service data lives on Proxima local storage
- Containers use named volumes mapped to Proxima storage
- Storage is considered authoritative for service state

External storage systems are optional and non-critical for development workflows.

---

## Network Model (Logical)

- All nodes operate within the same trusted LAN
- No public exposure is assumed by default
- Services are accessed internally unless explicitly designed otherwise

Network security is achieved through **scope limitation**, not exposure.

---

## Architecture Stability Rules

This document changes only when:

- A node role changes
- A responsibility boundary changes
- A core architectural constraint is revised

Operational changes do **not** belong here.

---

## Summary

The architecture enforces:

- Clear separation of concerns
- Predictable service placement
- Minimal host-level complexity
- Docker-first workflows

This structure is intentionally boring — and therefore reliable.
