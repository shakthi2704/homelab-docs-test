# Core Services

## Overview

Central shared services running on the core-services LXC.
Currently includes:

- Docker
- Monitoring stack (Prometheus/Grafana)
- Gitea

---

## Phase 4 – Core Services Deployment

### Scope

Node: core-services (LXC)  
Purpose: Shared infrastructure services  
Principle: Stability, documentation, and persistence before expansion

---

### Current State (Confirmed)

- [x] core-services LXC provisioned and stable
- [x] Docker installed and operational
- [x] Monitoring stack running
- [x] Gitea deployed
- [x] Gitea admin account created and accessible
- [x] SSH-based Git access enforced for all users
- [x] Baseline repositories created inside `infra` organization:
  - [x] `infra-docs` (documentation)
  - [x] `docker-stacks` (Docker stack definitions)
  - [x] `home-lab-config` (LXC and home-lab configurations)
- [x] Existing homelab documentation migrated into `infra-docs`
- [x] Docker volume mapping and persistence verified for Gitea (`/srv/gitea/data` and `/srv/gitea/logs`)
- [x] Timezone, base URL, and logging settings verified
- [x] Gitea container environment variables recorded (PUID, PGID, TZ, ports)

---

### 4.1 Source Control – Gitea (Hardening & Baseline)

#### Security & Access

- [x] Disable public user registration
- [x] Set default repository visibility to **private**
- [x] Disable anonymous access
- [x] Confirm admin email and instance metadata
- [x] Enforce SSH key–based Git access

#### Configuration & Persistence

- [x] Verify Docker volumes for Gitea (`/data`)
- [x] Confirm repository data persists across container restarts
- [x] Validate timezone and base URL configuration
- [x] Document Gitea container configuration

#### Initial Setup

- [x] Create infrastructure organization/group
- [x] Create baseline repositories:
  - [x] `infra-docs`
  - [x] `docker-stacks`
  - [x] `home-lab-config`
- [x] Add initial README to each repository

---

### 4.2 Documentation Baseline

- [x] Document core-services node:
  - [x] Purpose of node
  - [x] Running services
  - [x] Port usage
  - [x] Storage locations
- [x] Record Phase 4 decisions in ADR format

---

### 4.3 Reverse Proxy Standardization

- [ ] Select reverse proxy solution (Traefik or Nginx Proxy Manager)
- [ ] Deploy reverse proxy via Docker
- [ ] Route Gitea through reverse proxy
- [ ] Standardize internal service URLs
- [ ] Document routing and ports

---

### 4.4 Backup & Recovery (Minimum Viable)

- [x] Enable regular LXC snapshots
- [x] Define backup target for Gitea `/data` volume
- [ ] Test restore procedure for Gitea data
- [ ] Document backup and restore steps

---

### 4.5 Validation & Freeze

- [x] Confirm all Phase 4 services survive reboot
- [x] Verify monitoring visibility for core-services
- [x] Confirm Git operations (clone, push, pull) via SSH
- [x] Freeze Phase 4 (no new services added)

---

### Explicitly Deferred (Phase 5+)

- CI/CD runners
- OAuth / SSO
- Kubernetes / Swarm
- Secrets vaults
- Auto-update tooling (Watchtower)
