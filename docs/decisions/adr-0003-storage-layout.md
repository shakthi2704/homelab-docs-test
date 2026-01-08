# ADR 0003 – Proxima Storage Layout

## Status

Accepted

---

## Context

Proxima requires a storage layout to host LXC containers, Docker volumes, and
persistent service data. Considerations:

- Dedicated 1TB disk available
- Core services must have persistent storage
- Experimental containers should not impact persistent data
- Backups and snapshots must be feasible

---

## Decision

We will use the following storage layout on Proxima:

1. **Local 1TB disk** (`/mnt/pve/toshiba`) as the main container storage pool
2. **LXC containers**
   - Core services: mapped to persistent volumes on main disk
   - Monitoring & observability: mapped to persistent but isolated volumes
   - Experimental/sandbox: ephemeral volumes, easily deletable
3. **No Docker volumes on host**
   - All Docker volumes are mapped inside LXC containers
4. **Snapshots and backups**
   - Core and monitoring LXC volumes are snapshot-ready and included in backup routines

---

## Consequences

- **Pros:**

  - Clear separation of persistent and ephemeral data
  - Predictable volume management
  - Simplifies backup and recovery

- **Cons:**
  - Requires proper mapping and discipline to avoid accidental data loss
  - Limited flexibility if disk space becomes tight

---

## Alternatives Considered

1. **Multiple disks for LXC classes:**

   - Pros: stronger isolation
   - Cons: increases complexity and hardware requirements

2. **Docker volumes on host:**
   - Pros: simpler container management
   - Cons: violates host minimalism and isolation principles

---

## Notes

- All LXC and Docker workloads must respect this layout
- Any deviation or disk reallocation requires a new ADR
