# Home Lab Inventory & Config Reference

> Status: Phase 2 (Core Services LXC deployed) — VALIDATED  
> This document represents the current, deployed state of the home lab.

---

## Nodes

| Node    | Hostname | OS         | IP Address   | Role / Scope                                                         |
| ------- | -------- | ---------- | ------------ | -------------------------------------------------------------------- |
| Dev PC  | lyra     | Fedora     | 192.168.8.10 | Development workstation, infra authoring, SSH control node           |
| Proxmox | proxima  | Proxmox VE | 192.168.8.20 | Compute host (LXC-first strategy). No application logic on host      |
| Laptop  | nova     | Windows 11 | 192.168.8.30 | Ops endpoint: documentation, monitoring access, client communication |
| OMV     | rhea     | OMV        | 192.168.8.50 | Storage backbone: persistent data, stateful services only            |

---

## LXC Containers on Proxima

| Container Name | Class | Service / Role | Docker Inside? | Persistent Volume | IP Address   | Notes                                       |
| -------------- | ----- | -------------- | -------------- | ----------------- | ------------ | ------------------------------------------- |
| core-services  | Core  | Docker host    | Yes            | proxima-core-vol  | 192.168.8.21 | Hosts Gitea (admin email: lyra@proxima.com) |

---

## Network

- All nodes and containers are on the same LAN subnet: `192.168.8.0/24`
- IP addresses are statically assigned via router DHCP reservations
- Hostname resolution:
  - Router DNS (primary)
  - `/etc/hosts` entries (bootstrap / fallback)

---

## Access Model (High-Level)

- **Lyra**
  - SSH access to all nodes and LXC containers
  - Git and configuration authority
- **Nova**
  - Read-only / administrative access
  - No infrastructure control
- **Proxima & Rhea**
  - No lateral SSH trust between servers
  - Root SSH disabled on host (console-only where applicable)

---

## Storage (Current State)

- `pve-data` 1TB HDD used for **core-services LXC root disk and future container volumes**
- `/mnt/pve/toshiba` mount exists but **not yet used**
- No network mounts from Rhea consumed yet

---

## Notes

- This file reflects **current deployed reality** (Phase 2)
- `core-services` now runs **Gitea** with admin email: `lyra@proxima.com`
- Planned containers, ports, and volumes are documented elsewhere
- Update this file only when:
  - A node is added/removed
  - An IP or role changes
  - A container is created or removed
  - Phase completion is validated
