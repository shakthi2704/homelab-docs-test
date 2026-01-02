# Runbook – LXC Management on Proxima

## Purpose

This runbook defines the **management of LXC containers** on Proxima.  
It ensures that all containers are created, classified, and maintained in a
consistent and predictable manner.

LXC containers are the foundation for all persistent services in the homelab.

---

## Scope

- Creation of new LXC containers
- Classification according to responsibility
- Resource assignment and isolation
- Lifecycle management

Out of scope:

- Container internals (Docker images, services)
- Networking specifics (covered in `03-networking.md`)
- Backup and recovery operations (covered in `07-backup-recovery.md`)

---

## LXC Responsibility Classes

Each container must be assigned to a **single responsibility class**:

1. **Core Services LXC**

   - Hosts essential development infrastructure
   - Examples: Git services, CI/CD services, foundational tooling

2. **Monitoring & Observability LXC**

   - Hosts all observability, logging, and monitoring services
   - Isolated from core service containers
   - Observes but does not control state

3. **Experimental / Sandbox LXC**
   - Hosts isolated test or learning environments
   - Must never contain authoritative data
   - Can be safely deleted without consequence

---

## LXC Lifecycle Management

All LXC containers follow this lifecycle:

1. **Create**

   - Assigned class at creation
   - Storage and resource boundaries defined

2. **Operate**

   - Run container in isolation
   - Respect class-specific boundaries
   - Monitoring and observability as required

3. **Update**

   - Maintenance only within class limits
   - Changes documented in runbooks and ADRs if necessary

4. **Retire**
   - Decommission container
   - Remove persistent volumes if not needed
   - Archive configuration if required

---

## Resource Assignment

Each LXC container must have:

- Clear CPU, memory, and storage allocation
- Access only to its assigned volumes
- No cross-class volume sharing
- Priority for core services if resources are limited

---

## Isolation Rules

- Containers of different classes must not interfere
- Experimental containers must never compromise core or monitoring containers
- All containers respect the host boundaries (no Docker on host)

---

## Monitoring & Visibility

- LXC containers should be observable from monitoring class containers
- Failures must be detectable without impacting other classes

---

## Notes

- Any deviation from class or lifecycle requires an ADR
- LXC containers are the **authoritative runtime units** on Proxima
- Proper management ensures predictable, maintainable infrastructure
