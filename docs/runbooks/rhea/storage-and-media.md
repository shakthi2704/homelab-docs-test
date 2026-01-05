# Rhea – Storage and Media Runbook

## Document Metadata

- **Node Name:** Rhea
- **OS:** OpenMediaVault (OMV)
- **Role:** Storage & Media Node
- **Scope:** File services, media services, optional backups
- **Out of Scope:** Development, CI/CD, Git services, monitoring stacks

---

## 1. Purpose of Rhea

Rhea is a **dedicated storage and media node** in the homelab.  
Its responsibility is to provide **reliable, low-change services** that support the rest of the infrastructure.

Rhea is intentionally **not part of the compute or orchestration layer**.

---

## 2. Responsibilities

Rhea is responsible for:

- Media services:
  - Plex
  - Jellyfin
- File sharing:
  - SMB (Windows / general use)
  - NFS (Linux / Proxmox use)
- Optional backup target:
  - Backup destination for Proxima LXC snapshots or data volumes
- Long-term and cold data storage

---

## 3. Explicit Non-Responsibilities

The following must **never** be deployed on Rhea:

- Development containers
- CI/CD pipelines
- Git servers (Gitea, GitLab)
- Monitoring or observability stacks
- Reverse proxies
- Infrastructure control services
- Experimental or short-lived containers

This boundary ensures **stability, predictability, and data safety**.

---

## 4. Services Allowed on Rhea

### Core Services

- Plex (media streaming)
- Jellyfin (alternative media server)
- SMB shares
- NFS exports

### Optional Services

- Backup storage endpoint
- Read-only archive shares

All services should prioritize:

- Data persistence
- Minimal updates
- Conservative configuration changes

---

## 5. Storage Model

### Storage Characteristics

- Large-capacity disks (HDD preferred)
- RAID or parity as supported by OMV
- Focus on durability over performance

### Storage Usage

- Media libraries
- User file shares
- Backup data from Proxima
- Archived datasets

Rhea should **not** be used for:

- Active container volumes
- Databases
- Latency-sensitive workloads

---

## 6. Network Access

### Access Patterns

- Proxima → Rhea:
  - Backup writes
  - Read-only access where possible
- Lyra → Rhea:
  - File access
  - Media access
- Nova → Rhea:
  - Administration only

### Network Principles

- Prefer internal LAN access only
- No public exposure
- Firewall rules should restrict access to known nodes

---

## 7. Backup Strategy (Optional)

Rhea may act as a **secondary backup destination**:

- Proxima snapshots copied to Rhea
- Periodic sync of critical data
- Backups should be:
  - Versioned
  - Read-only where possible
  - Verified periodically

Rhea itself should still be backed up externally if data is critical.

---

## 8. Maintenance Guidelines

- Apply OMV updates conservatively
- Avoid frequent configuration changes
- Monitor disk health and SMART status
- Validate backups regularly
- Keep service count minimal

---

## 9. Failure Scenarios

### If Rhea Goes Offline

- Media services become unavailable
- File shares unavailable
- Proxima and Lyra continue operating normally

Rhea failure must **never** block:

- Development
- Git operations
- Monitoring
- Core infrastructure services

---

## 10. Documentation & Inventory

- Rhea configuration details (IPs, shares, disks) must be recorded in:
  - `configs/home-lab-inventory.md`
- Architectural role is defined in:
  - `docs/design/02-node-roles.md`
  - `docs/design/04-storage.md`

---

## 11. Design Principle Reminder

Rhea is a **support node**, not a platform.

Stability > Flexibility  
Storage > Compute  
Predictability > Experimentation

---
