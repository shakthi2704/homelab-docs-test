# Home Lab Inventory & Config Reference

> Status: Phase 3 (Core Services & Monitoring LXC deployed) — VALIDATED  
> This document represents the current, deployed state of the home lab.

---

## Nodes

| Node    | Hostname | OS         | IP Address   | Role / Scope                                                    |
| ------- | -------- | ---------- | ------------ | --------------------------------------------------------------- |
| Dev PC  | lyra     | Fedora     | 192.168.8.10 | Development workstation, infra authoring, SSH control node      |
| Proxmox | proxima  | Proxmox VE | 192.168.8.20 | Compute host (LXC-first strategy). No application logic on host |
| Laptop  | nova     | Windows 11 | 192.168.8.30 | Ops endpoint: documentation, monitoring access                  |
| OMV     | rhea     | OMV        | 192.168.8.50 | Storage node (present, not yet consumed by Proxima)             |

---

## LXC Containers on Proxima (Authoritative)

| Container Name   | Class      | Role / Responsibility            | Docker Inside | Persistent Volume(s)                      | IP Address   | Notes                                |
| ---------------- | ---------- | -------------------------------- | ------------- | ----------------------------------------- | ------------ | ------------------------------------ |
| core-services    | Core       | Docker runtime only              | Yes           | proxima-core-vol                          | 192.168.8.21 | No application services deployed yet |
| monitor-services | Monitoring | Observability & monitoring stack | Yes           | uptime-kuma-data, pulse-data, dozzle-data | 192.168.8.22 | Runs Uptime Kuma, Pulse, Dozzle      |

---

## Network

- All nodes and LXC containers are on `192.168.8.0/24`
- IPs assigned via router DHCP reservations
- Hostname resolution:
  - Router DNS
  - `/etc/hosts` fallback

### Service Exposure

- Docker containers use **bridge networking inside LXC**
- Ports are published on the **LXC IP**, not on the Proxmox host

Monitoring services (`monitor-services` – `192.168.8.22`):

- Uptime Kuma → `8081`
- Pulse → `8082`
- Dozzle → `8083`

---

## Access Model

- **Lyra**
  - SSH access to all nodes and LXC containers
- **Nova**
  - Monitoring and documentation access only
- **Proxima & Rhea**
  - No lateral SSH trust
  - Root SSH disabled on host
- **LXC Access**
  - SSH or `pct enter <vmid>`

---

## Storage

- `pve-data` (1TB HDD):
  - LXC root disks
  - Persistent Docker volumes
- Active volumes:
  - `proxima-core-vol`
  - `uptime-kuma-data`
  - `pulse-data`
  - `dozzle-data`
- `/mnt/pve/toshiba` exists but unused
- No network mounts from Rhea consumed

---

## Notes

- Reflects deployed reality only
- Update only when containers, IPs, or volumes change
