# Home Lab Inventory & Config Reference

> Status: Phase 1 (Day-0 Infrastructure) — VALIDATED  
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

## Network

- All nodes are on the same LAN subnet: `192.168.8.0/24`
- IP addresses are statically assigned via router DHCP reservations
- Hostname resolution:
  - Router DNS (primary)
  - `/etc/hosts` entries (bootstrap / fallback)

---

## Access Model (High-Level)

- **Lyra**
  - SSH access to all nodes
  - Git and configuration authority
- **Nova**
  - Read-only / administrative access
  - No infrastructure control
- **Proxima & Rhea**
  - No lateral SSH trust between servers
  - Root SSH disabled (console-only where applicable)

---

## Storage (Current State)

- Physical disks mounted and configured on **Rhea**
- No network mounts consumed by Proxima yet
- No application volumes in active use

---

## Notes

- This file reflects **current deployed reality**, not future plans
- Planned containers, ports, and volumes are documented elsewhere
- Update this file only when:
  - A node is added/removed
  - An IP or role changes
  - Phase completion is validated
