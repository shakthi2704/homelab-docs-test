# Runbook – LXC Management on Proxima

## Purpose

Defines how LXC containers are created and managed on Proxima.
LXC containers are the authoritative runtime boundary.

---

## Scope

- LXC creation and classification
- Resource assignment
- Lifecycle management

Out of scope:

- Docker internals
- Service configuration
- Backup and recovery

---

## Responsibility Classes

### Core Services LXC

- Hosts Docker runtime for core services
- Persistent by design
- Currently deployed: `core-services`

### Monitoring LXC

- Hosts observability tooling only
- No control over application state
- Currently deployed: `monitor-services`

---

## Current LXC State

- Two LXC containers exist:
  - `core-services` (Core)
  - `monitor-services` (Monitoring)
- Both use Ubuntu LXC templates
- Docker runs **inside** each container
- Docker is **forbidden on Proxmox host**

---

## Lifecycle Rules

1. **Create**

   - Assign class at creation
   - Define storage and IP

2. **Operate**

   - Respect class boundaries
   - No cross-container dependencies

3. **Update**

   - Container-level updates only
   - Document significant changes

4. **Retire**
   - Intentional decommission
   - Remove volumes only if confirmed

---

## Isolation Rules

- No service runs directly on Proxmox host
- No cross-class volume sharing
- Monitoring LXC observes but does not modify state
- Core services remain isolated from monitoring logic

---

## Notes

- Any deviation requires an ADR
- LXC containers are treated as long-lived infrastructure units
