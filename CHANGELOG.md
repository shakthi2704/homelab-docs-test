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

## Notes

- Documentation reflects deployed reality only
- No planned or speculative components are recorded
