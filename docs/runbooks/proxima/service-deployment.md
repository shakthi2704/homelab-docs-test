# Runbook – Service Deployment on Proxima

## Purpose

This runbook defines the **process for deploying services** inside Docker
containers on Proxima, ensuring all deployments are consistent, isolated,
and maintainable.

---

## Scope

- Deploying Dockerized services within LXC containers on Proxima
- Observability and monitoring integration
- Lifecycle compliance and class alignment

Out of scope:

- Container creation (covered in `lxc-management.md`)
- Docker runtime configuration (covered in `docker-runtime.md`)
- Development or ephemeral deployment on Lyra or Nova

---

## Service Deployment Principles

1. **Class Alignment**

   - Services must be deployed in the correct LXC container class
   - Core services, monitoring, and experimental services must remain separate

2. **Persistent State Management**

   - Service data is externalized to Proxima storage
   - Containers are replaceable without losing state

3. **Observability**

   - All services must integrate with monitoring containers
   - Logs, metrics, and health status must be accessible

4. **Promotion**

   - New services are first validated in experimental containers (if needed)
   - Approved services are promoted to the correct persistent LXC class

5. **Operational Isolation**
   - Services must not interfere with other containers
   - Failures must be contained to the service scope

---

## Deployment Workflow

1. **Prepare Service**

   - Determine container image
   - Identify persistent volumes
   - Classify service (core, monitoring, experimental)

2. **Deploy to LXC Container**

   - Map volumes and resources
   - Ensure service class isolation
   - Enable observability hooks

3. **Validate**

   - Confirm service is running as intended
   - Verify monitoring integration
   - Ensure no dependency violations

4. **Promote / Scale**

   - Move validated service to production LXC class
   - Scale containers if necessary
   - Document promotion in runbook

5. **Operate**

   - Monitor health and metrics
   - Apply updates according to lifecycle rules

6. **Retire**
   - Decommission service intentionally
   - Archive data if needed
   - Remove container cleanly

---

## Deployment Constraints

- No core services in experimental LXC
- No monitoring services in core LXC
- Persistent data must remain on Proxima storage
- All deployment changes must be documented

---

## Notes

- Service deployment is **predictable and repeatable**
- Deviations from the deployment process require an ADR
- Observability, class alignment, and lifecycle rules ensure maintainable infrastructure
