# Changelog

All notable changes to the homelab documentation repository are recorded here.
Semantic versioning and date-based entries are followed.

---

## [1.0.0] – 2026-01-02

### Added

- Initial architecture, design, and runbook documentation
- LXC-first strategy and Docker-in-LXC ADRs
- Baseline node definitions and security boundaries

---

## [1.1.0] – 2026-01-05

### Added / Updated

- Phase 1: Day-0 infrastructure validation
- Verified node IPs, hostnames, and access model
- No containers deployed

---

## [1.2.0] – 2026-01-06

### Added / Updated

- Phase 2: Core Services LXC created
- `core-services` LXC deployed
- Docker runtime verified inside LXC
- Persistent Docker volume created (`proxima-core-vol`)

---

## [1.3.0] – 2026-01-06

### Added / Updated

- Phase 3: Monitoring LXC deployed
- `monitor-services` LXC created
- Monitoring stack deployed:
  - Uptime Kuma
  - Pulse
  - Dozzle
- Persistent volumes created:
  - `uptime-kuma-data`
  - `pulse-data`
  - `dozzle-data`
- Inventory and runbooks updated to reflect deployed state

---

## [1.4.0] – 2026-01-06

### Added / Updated

- Phase 4: Core Services Hardening & Repository Organization
- Gitea container deployed and configured:
  - SSH-based Git access enforced for all users
  - Admin accounts reviewed; strong password policy applied
  - Public user registration disabled
  - Default repository visibility set to private
- Baseline repositories created inside `infra` organization:
  - `infra-docs` → documentation, ADRs, runbooks
  - `docker-stacks` → Docker Compose files and container stack definitions
  - `home-lab-config` → LXC manifests, scripts, and home-lab configuration files
- Existing homelab documentation migrated into `infra-docs` repository
- Docker volume mapping and persistence verified for Gitea (`/srv/gitea/data` and `/srv/gitea/logs`)
- Timezone, base URL, and logging settings verified and confirmed
- Repository structure and permissions reviewed
- SSH key onboarding workflow documented for all users
- Backup and persistence strategy verified

---

## Notes

- Documentation reflects deployed reality only
- No planned or speculative components are recorded
