# Home Lab Inventory & Config Reference

> Status: Phase 3 (Core Services & Monitoring LXC deployed) — VALIDATED  
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

| Container Name   | Class      | Service / Role                   | Docker Inside? | Persistent Volume(s)                      | IP Address   | Notes                                                                          |
| ---------------- | ---------- | -------------------------------- | -------------- | ----------------------------------------- | ------------ | ------------------------------------------------------------------------------ |
| core-services    | Core       | Docker host / developer tools    | Yes            | proxima-core-vol                          | 192.168.8.21 | Hosts Gitea (admin email: lyra@proxima.com)                                    |
| monitor-services | Monitoring | Monitoring / observability stack | Yes            | uptime-kuma-data, pulse-data, dozzle-data | 192.168.8.22 | Hosts Uptime Kuma, Pulse, Dozzle; LXC nested Docker enabled; firewall disabled |

---

## Network

- All nodes and containers are on the same LAN subnet: `192.168.8.0/24`
- IP addresses are statically assigned via router DHCP reservations
- Hostname resolution:
  - Router DNS (primary)
  - `/etc/hosts` entries (bootstrap / fallback)
- LXC containers have individual IPs and exposed ports for each service:
  - `monitor-services`:
    - Uptime Kuma → `8081`
    - Pulse → `8082`
    - Dozzle → `8083`

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
- **Container Access**
  - Monitoring services and core services can be accessed via container SSH or host `pct enter <vmid>` commands

---

## Storage (Current State)

- `pve-data` 1TB HDD used for **core-services & monitoring LXC root disks and persistent Docker volumes**
- Persistent Docker volumes:
  - `proxima-core-vol` → core services (Gitea)
  - `uptime-kuma-data` → Uptime Kuma database
  - `pulse-data` → Pulse configuration & metrics
  - `dozzle-data` → Dozzle logs (optional)
- `/mnt/pve/toshiba` mount exists but **not yet used**
- No network mounts from Rhea consumed yet

---

## Notes

- This file reflects **current deployed reality** (Phase 3)
- `core-services` now runs **Gitea** with admin email: `lyra@proxima.com`
- `monitor-services` hosts monitoring stack: **Uptime Kuma, Pulse, Dozzle**
- IPs, volumes, and services should match `docker-runtime.md` and `service-deployment.md`
- Update this file only when:
  - A node is added/removed
  - An IP or role changes
  - A container is created or removed
  - Persistent volumes are added/modified
  - Phase completion is validated
