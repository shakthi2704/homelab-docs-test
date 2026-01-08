# Runbook – Proxima Baseline Setup

> Status: Phase 1 (Day-0 Infrastructure) — Baseline validated and node reachable

## Purpose

This runbook defines the **baseline configuration of the Proxima node** (Proxmox
server) to prepare it for hosting persistent development containers and services.

It ensures a **repeatable, predictable environment** for all subsequent steps.

---

## Scope

- Proxima physical server
- Local disk(s) preparation (currently mounted and recognized)
- Network readiness verified
- LXC and Docker prerequisites (planned, not yet created)

Out of scope:

- Container creation
- Service deployments
- Monitoring or experimental tools (covered in later runbooks)

---

## Baseline Setup Objectives (Phase 1 Completed)

1. **Install and prepare Proxmox VE**

   - Host OS installed and updated
   - Management interface accessible
   - Base packages patched

2. **Disk and Storage Verification**

   - Storage device(s) mounted and available
   - Disk authority aligned with storage boundaries
   - Storage pools **not yet assigned to containers** (reserved for Phase 2)

3. **Network Configuration**

   - Node reachable from trusted LAN
   - Static IP: `192.168.8.20`
   - Connectivity confirmed with Lyra (`192.168.8.10`), Nova (`192.168.8.30`), and Rhea (`192.168.8.50`)

4. **Service Foundations**

   - SSH enabled and tested
   - Host minimalism verified (no Docker installed on host)
   - Ready for LXC creation in next phases

5. **Operational Readiness**

   - Administrative user confirmed
   - Time synchronized via NTP
   - Basic security boundaries enforced (root SSH console-only)

---

## Pre-Baseline Checklist (Confirmed)

- [x] Hardware installed and connected
- [x] Local disk available for container volumes
- [x] Network cable connected and LAN verified
- [x] Access from trusted workstation (Lyra) confirmed

---

## Post-Baseline State (Phase 1)

After completing Phase 1:

- Node is reachable over the LAN
- Hostname and IP correctly assigned (`proxima` / `192.168.8.20`)
- SSH access from Lyra and Nova verified
- Storage devices mounted and recognized
- Host is clean and minimal (no Docker or containers yet)

This state represents a **clean, minimal Proxmox host**, ready for Phase 2 deployment.

---

## Notes

- Any deviation from baseline requires documentation and possibly an ADR
- Baseline is **repeatable**, designed for disaster recovery or replacement
- No containers or service workloads exist at this stage
