# Standards – Container Lifecycle

## Purpose

This document defines the **lifecycle of containers** in the homelab and
development environment to ensure predictable, maintainable, and traceable
operations.

Applies to LXC containers on Proxima and Docker containers on Lyra.

---

## Lifecycle Stages

### 1. Create

- Assign container to a **responsibility class**:
  - Core services (`core`)
  - Monitoring & observability (`monitor`)
  - Experimental / sandbox (`sandbox`)
- Define resources: CPU, memory, storage
- Map volumes for persistent or ephemeral data
- Assign naming according to `naming-conventions.md`

**Outcome:** Container exists, isolated, and ready for configuration

---

### 2. Operate

- Start and run container
- Ensure service or development workflow is functional
- Integrate with monitoring and logging as required
- Observe resource usage and limits

**Outcome:** Container is actively providing services or development environment

---

### 3. Update / Maintain

- Apply updates, patches, or configuration changes
- Ensure changes do not violate class or resource boundaries
- Document updates in runbooks or version control
- Validate service after updates

**Outcome:** Container is up-to-date, secure, and functioning correctly

---

### 4. Promote (if applicable)

- For development containers (Lyra → Proxima)
- Validate container readiness for persistent deployment
- Assign to correct class on Proxima
- Version and document promoted container

**Outcome:** Container is ready for production or persistent service use

---

### 5. Retire / Decommission

- Stop container
- Archive or delete persistent data as required
- Remove from monitoring and backup scope
- Update runbooks and documentation

**Outcome:** Container removed cleanly, without leaving orphaned resources

---

## Additional Rules

1. All containers must **follow lifecycle stages**
2. No containers are left unmanaged or undocumented
3. Experimental containers are **ephemeral** and disposable
4. Core and monitoring containers have **persistent volumes and backups**
5. Promotion and retirement are **intentional, documented, and traceable**

---

## Notes

- Lifecycle ensures **predictable operations** and **maintainable infrastructure**
- Deviations require approval or a new ADR
- Lifecycle rules apply equally to Docker containers on Lyra and LXC containers on Proxima
