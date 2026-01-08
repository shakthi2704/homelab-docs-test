# Runbook – Lyra Docker Workflow

## Purpose

This runbook defines the **Docker workflow on Lyra** for development,
testing, and preparation for promotion to Proxima.

It ensures a consistent, isolated, and predictable container lifecycle.

---

## Scope

- Docker on Lyra
- Container lifecycle: create → test → prepare for promotion
- Local build artifacts and temporary volumes

Out of scope:

- Deployment to Proxima
- Persistent service data
- Monitoring and production observability

---

## Workflow Principles

1. **Ephemeral Containers**

   - All containers on Lyra are temporary
   - Containers can be destroyed without consequence
   - Persistent data only in local source code or promotion artifacts

2. **Class-Free Containers**

   - Containers are not tied to LXC classes
   - Designed for testing and iteration

3. **Promotion-Oriented Build**

   - Containers are validated for eventual deployment to Proxima
   - Include necessary configuration and volume mappings for later migration

4. **Isolation**

   - Docker containers remain isolated from the host system
   - Host contamination is avoided

5. **Observability**
   - Logs and output must be easily accessible for debugging and testing

---

## Workflow Steps

1. **Create**

   - Initialize development container
   - Assign temporary volumes for source code
   - Ensure environment matches Proxima-compatible runtime

2. **Test**

   - Run service in container
   - Validate functional and integration requirements
   - Observe logs and metrics locally

3. **Prepare for Promotion**

   - Package container or image for Proxima
   - Document configuration, environment variables, and volume requirements
   - Tag or version the container for identification

4. **Clean Up**
   - Remove ephemeral containers
   - Keep only artifacts necessary for promotion
   - Ensure local host remains clean and stable

---

## Resource Management

- Containers use limited CPU, memory, and disk
- Avoid over-committing host resources
- Ensure development workflow does not interfere with Proxima or other nodes

---

## Notes

- Lyra’s Docker workflow is **developer-first, ephemeral, and promotion-oriented**
- All changes and workflows should be documented for traceability
- Any deviation from this workflow requires justification and documentation
