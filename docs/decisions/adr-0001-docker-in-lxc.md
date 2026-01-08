# ADR 0001 – Docker inside LXC Containers on Proxima

## Status

Accepted

---

## Context

We need to run multiple services in a predictable, isolated, and recoverable
environment. Options considered:

1. Install Docker directly on Proxmox host
2. Run services directly in LXC containers without Docker
3. Use Docker inside LXC containers

Constraints:

- Proxmox host should remain minimal and stable
- Services must be isolated, observable, and recoverable
- Containers must follow a predictable lifecycle

---

## Decision

We will run **Docker inside LXC containers** on Proxima.

- Each LXC container represents a class (Core, Monitoring, Experimental)
- Docker workloads are confined to LXC containers
- Host does not run Docker directly

---

## Consequences

- **Pros:**

  - Strong isolation between service classes
  - Host stability maintained
  - Predictable container lifecycle

- **Cons:**
  - Slight overhead due to LXC layer
  - Requires developer awareness of nested container management

---

## Alternatives Considered

1. **Docker directly on host:**

   - Pros: simpler setup
   - Cons: risk of host contamination, less isolation

2. **Direct LXC services without Docker:**
   - Pros: lightweight
   - Cons: harder to manage service images, inconsistent workflows

---

## Notes

- All future Docker services must follow this decision
- Any deviation requires a new ADR
