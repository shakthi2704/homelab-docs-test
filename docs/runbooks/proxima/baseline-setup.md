# Runbook – Proxima Baseline Setup

## Purpose

This runbook defines the **baseline configuration of the Proxima node** (Proxmox
server) to prepare it for hosting all persistent development containers and
services.

It ensures a repeatable, predictable environment for all subsequent steps.

---

## Scope

- Proxima physical server
- Local disk(s) preparation
- Network readiness
- LXC and Docker prerequisites

Out of scope:

- Container creation
- Service deployments
- Monitoring or experimental tools (covered in later runbooks)

---

## Baseline Setup Objectives

1. **Install and prepare Proxmox VE**

   - Host OS installation
   - Management interface readiness
   - Base package update and patching

2. **Disk and Storage Preparation**

   - Identify and assign storage for container data
   - Ensure disk authority aligns with storage boundaries
   - Prepare LVM or storage pools for Proxmox and LXC usage

3. **Network Configuration**

   - Ensure node is reachable from trusted LAN
   - Confirm internal IP assignment and connectivity with Lyra, Nova, and Rhea

4. **Service Foundations**

   - Enable SSH or remote access
   - Prepare for LXC creation
   - Confirm host minimalism (no Docker directly on host)

5. **Operational Readiness**
   - Create administrative user(s) as required
   - Confirm time synchronization
   - Apply basic security settings (scope-limited)

---

## Pre-Baseline Checklist

- [ ] Hardware installed and connected
- [ ] 1TB local disk available for container volumes
- [ ] Network cable connected and LAN verified
- [ ] Access to trusted administrative workstation (Nova)

---

## Post-Baseline State

After completing the baseline setup, Proxima will:

- Be reachable over the LAN
- Have storage pools assigned and authoritative
- Be ready for LXC container creation
- Have host security boundaries enforced
- Have no Docker installed on the host

This state represents a **clean, minimal Proxmox host** ready for containerized
development services.

---

## Notes

- Any deviation from baseline requires documentation and possibly an ADR
- Baseline is **repeatable**, designed for disaster recovery and replacement
- No containers or service workloads exist at this stage
