# Runbook – Lyra Image Promotion

## Purpose

This runbook defines the **process for promoting Docker images or containers**
from Lyra (development) to Proxima (runtime).

It ensures that all promoted workloads are validated, documented, and correctly
classified.

---

## Scope

- Docker images and containers created on Lyra
- Promotion to Proxima LXC containers
- Validation and documentation prior to deployment

Out of scope:

- Container creation on Lyra (covered in `docker-workflow.md`)
- Proxima deployment specifics (covered in `service-deployment.md`)
- Runtime monitoring and observability

---

## Promotion Principles

1. **Validation First**

   - Only tested and functional containers/images are eligible for promotion
   - Ensure compatibility with Proxima runtime

2. **Class Assignment**

   - Assign promoted container to the correct LXC responsibility class:
     - Core services
     - Monitoring & observability
     - Experimental (rarely)

3. **Isolation**

   - Promotion must not introduce cross-class dependencies
   - Container configuration and volumes must remain consistent

4. **Versioning**

   - Images/containers must have clear version or tag identifiers
   - Historical tracking for rollback and traceability

5. **Documentation**
   - Record promotion in runbooks
   - Include environment, configuration, and validation results
   - Any deviation must be justified with an ADR

---

## Promotion Workflow

1. **Prepare Image**

   - Verify container runs correctly on Lyra
   - Ensure all dependencies are included
   - Confirm volume mappings and environment variables

2. **Validate for Proxima**

   - Check compatibility with target LXC container
   - Confirm storage and resource requirements

3. **Tag and Document**

   - Assign version or tag
   - Document validation results and promotion readiness
   - Include promotion date and responsible developer

4. **Deploy to Proxima**

   - Move container/image to Proxima LXC
   - Confirm class alignment
   - Record deployment in runbook

5. **Post-Promotion Verification**
   - Verify container runs as expected on Proxima
   - Ensure monitoring and observability integration
   - Confirm no cross-class interference

---

## Notes

- Promotion is **intentional, controlled, and traceable**
- Containers must never bypass validation and documentation
- All promoted containers/images must comply with lifecycle rules
- Rollback and historical versioning must be possible
