# ADR-0002: Use OpenMediaVault (OMV) for Dedicated Media & Storage Node (Rhea)

## Status

Accepted

## Context

The homelab requires persistent storage for media and shared files.  
Key considerations included:

- Media streaming (Plex, Jellyfin)
- File sharing (SMB/NFS)
- Stability and uptime
- Minimal interference with development infrastructure
- Ease of management and monitoring

Several options were considered:

1. Use Proxima’s storage for media and development services together
2. Use a general-purpose Linux server for storage
3. Use a dedicated NAS operating system (OpenMediaVault)

---

## Decision

A dedicated node **Rhea** running **OpenMediaVault (OMV)** will host all media and file storage services.

- Rhea will serve **media libraries** (Plex, Jellyfin)
- Rhea will serve **file-sharing services** (SMB/NFS)
- Rhea will be **isolated from development workloads**
- Rhea will operate independently from Proxima, Lyra, and Nova

OMV provides a **lightweight, stable, and purpose-built NAS OS**, minimizing overhead and operational complexity.

---

## Alternatives Considered

### 1. Share Proxima Storage

- Pros: Fewer nodes, easier hardware management
- Cons: Mixing development and media workloads could cause instability and resource contention
- Rejected: violates separation-of-concerns principle

### 2. General-purpose Linux Server

- Pros: Flexible, full control
- Cons: Requires more setup and maintenance, less optimized for NAS features
- Rejected: OMV provides easier maintenance and native NAS functionality

### 3. Dedicated NAS OS (OMV)

- Pros: Optimized for file and media services, simple management, reliable uptime
- Cons: Limited flexibility outside NAS scope
- Accepted: aligns with principle of single-purpose node

---

## Consequences

### Positive

- Clear separation of responsibilities
- Stable and predictable media/storage services
- Simplified administration and monitoring
- Reduced risk of resource conflicts with development workloads

### Negative

- Slightly more hardware overhead (dedicated node)
- Any expansion of development services on Rhea would require migration

---

## Notes

- Rhea’s storage is authoritative for media and shared files
- Backup, replication, or high-availability strategies will be documented separately in runbooks
- Any future development workloads on Rhea require a **new ADR**

---

## Summary

Rhea will remain a **single-purpose media and storage node** running OpenMediaVault, isolated from development and container workloads, ensuring predictable and reliable service.
