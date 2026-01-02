# ADR 0002 – Avoid Full Virtual Machines

## Status

Accepted

---

## Context

When designing Proxima, we considered whether to run services in full virtual
machines (VMs) or use LXC containers.

Constraints and goals:

- Minimize host resource overhead
- Keep services lightweight, isolated, and predictable
- Simplify management and promotion workflow
- Align with Docker-first, containerized architecture

---

## Decision

We will **not use full virtual machines** for service hosting.

- All services run in **Docker containers inside LXC containers**
- Proxmox VMs may exist only for exceptional or legacy cases (rare)
- LXC containers provide sufficient isolation for our homelab goals

---

## Consequences

- **Pros:**

  - Lower resource overhead
  - Faster container provisioning
  - Easier backup and lifecycle management

- **Cons:**
  - Slightly less strict isolation compared to full VMs
  - Cannot run certain OS-level experiments without LXC tweaks

---

## Alternatives Considered

1. **Full VMs for each service:**

   - Pros: maximum isolation
   - Cons: high resource usage, slower provisioning, harder promotion workflow

2. **Mixed approach (VM + LXC):**
   - Pros: flexibility for legacy workloads
   - Cons: increases complexity, breaks uniform workflow

---

## Notes

- All service workloads should follow this ADR
- Any future VM usage requires a new ADR to justify deviation
