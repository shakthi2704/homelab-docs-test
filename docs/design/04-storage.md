# Homelab & Development Infrastructure – Storage

## Document Context

This document defines **storage responsibilities, ownership, and boundaries**
within the homelab and development infrastructure.

It builds on:

- `00-overview.md`
- `01-architecture.md`
- `02-node-roles.md`
- `03-networking.md`

This file describes **where data lives and who owns it**, not how storage is
configured or mounted.

---

## Storage Design Principles

All storage in this environment follows these principles:

- Data ownership is explicit
- Storage authority is centralized
- Compute is replaceable; data is not
- Persistence is intentional, not accidental

If data cannot be clearly classified, it should not persist.

---

## Authoritative Storage Node

### Proxima — Service Data Authority

Proxima is the **authoritative storage location** for all development-related
services.

**Responsibilities**

- Persist container data
- Store service state
- Host volumes required for long-running services

All persistent service data must be recoverable independently of compute.

---

## Storage Scope by Node

### Lyra (Development Node)

- May store source code and temporary artifacts
- No authoritative service data
- All data is disposable

Lyra’s storage is considered **non-critical**.

---

### Nova (Access Node)

- Stores no authoritative data
- May contain cached or temporary files
- No persistence guarantees

Nova is storage-neutral.

---

### Rhea (Storage & Media Node)

- Owns media libraries and shared files
- Does not store development service data
- No dependency from development services

Rhea remains outside the development storage model.

---

## Container Storage Model

- Containers are stateless by default
- Persistent state is externalized via volumes
- Volumes are managed and backed by Proxima storage

Containers must be replaceable without data loss.

---

## Data Classification

All data falls into one of the following categories:

1. **Ephemeral**

   - Build artifacts
   - Temporary logs
   - Cache data

2. **Persistent**

   - Git repositories
   - Databases
   - Service configuration

3. **External**
   - Media libraries
   - File shares

Each category has a single authoritative owner.

---

## Disallowed Storage Patterns

The following are not allowed:

- Persistent data inside containers
- Shared volumes across unrelated services
- Development services depending on external storage nodes
- Silent persistence on development machines

---

## Backup & Recovery Relationship

This document defines **what must be backed up**, not how.

Backup strategy and recovery procedures are defined in
`07-backup-recovery.md`.

---

## Summary

The storage model ensures:

- Clear data ownership
- Predictable recovery
- Minimal accidental persistence
- Safe service replacement

When storage boundaries are respected, recovery becomes straightforward.
