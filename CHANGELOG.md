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

## [1.4.0] – DEPLOYED – 2026-01-06

### Added / Updated

- Phase 4: Core Services Hardening & Repository Organization
- Gitea container deployed and validated:
  - SSH-based Git access verified
  - Baseline repositories created
  - Timezone, base URL, and logging verified
  - Backup and restore procedures tested successfully
- Repository structure and permissions reviewed
- Docker volume mapping and persistence confirmed

---

## [1.5.0] – PLANNED

### Planned

- Phase 5: Advanced Services & Automation Planning
- Reverse proxy selection (Traefik / Nginx Proxy Manager)
- CI/CD runner strategy definition
- Secrets and credentials management planning
- Monitoring and alerting expansion planning
- Backup and disaster recovery strategy design

> Note: No Phase 5 services are deployed. This section reflects design intent only.

## [1.6.0] – 2026-01-07

### Added / Updated

- Phase 5 CI/CD runner deployed:
  - Drone server container running
  - Drone runner container running and connected
  - Gitea repositories activated (`docker-stacks`, `home-lab-config`)
  - `.drone.yml` pipelines created for repository automation

---

## [1.7.0] – 2026-01-07

### Added / Updated

- Lyra node baseline setup completed:
  - SSH access to Proxima host validated
  - Documentation repo cloned and tested
  - Optional Docker client tested
- Runbooks for Lyra created and validated

## Notes

- Documentation must always reflect **validated deployed reality**
- Planned phases must never be marked as completed
- Partial deployments require explicit validation before promotion
