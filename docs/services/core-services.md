---
# core-services.md (trimmed and aligned)

# Core Services

## Overview

Central shared services running on the core-services LXC.
Currently includes:

- Docker
- Gitea

---

## Phase 4 – Core Services Deployment

### Scope

Node: core-services (LXC)  
Purpose: Shared infrastructure services  
Principle: Stability, documentation, and persistence before expansion

---

### Current State (Validated)

- [x] core-services LXC provisioned and stable
- [x] Docker installed and operational
- [x] Gitea container running
- [x] Gitea admin account created

---

### Phase 4 Tasks (Validated)

- [x] SSH-based Git access configured (validation pending)
- [x] Baseline repositories created (infra-docs, docker-stacks, home-lab-config)
- [x] Gitea timezone, base URL, and logging settings verified
- [x] Backup and restore procedures tested

---

### Phase 5 – Advanced Services & Automation

> Planning only — no Phase 5 services are deployed

- [x] CI/CD runner setup
- [x] Secrets and credential management
- [x] Monitoring and alerting expansion
- [x] Security hardening and validation

---
