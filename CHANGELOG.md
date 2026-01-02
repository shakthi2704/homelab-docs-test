# Changelog

All notable changes to the homelab documentation repository are
recorded in this file. Follow **semantic versioning** and date entries.

---

## [1.0.0] – 2026-01-02

### Added

- **Design docs**:

  - `00-overview.md` – Overview of homelab & development infrastructure
  - `01-architecture.md` – Architecture and high-level layout
  - `02-node-roles.md` – Node responsibilities and roles
  - `03-networking.md` – Network design and addressing
  - `04-storage.md` – Storage layout, volumes, and disks
  - `05-container-strategy.md` – LXC and Docker strategy
  - `06-security-boundaries.md` – Security zones and access rules
  - `07-backup-recovery.md` – Backup and recovery plan
  - `08-failure-scenarios.md` – Failure handling and mitigation
  - `09-design-principles.md` – Guiding principles for homelab

- **Runbooks**:

  - Proxima: `baseline-setup.md`, `lxc-management.md`, `docker-runtime.md`, `service-deployment.md`
  - Lyra: `dev-environment.md`, `docker-workflow.md`, `image-promotion.md`
  - Nova: `access-and-admin.md`

- **Standards**:

  - `naming-conventions.md`, `container-lifecycle.md`, `git-workflow.md`, `documentation-rules.md`

- **Decisions (ADRs)**:

  - `adr-0001-docker-in-lxc.md`
  - `adr-0002-no-vms.md`
  - `adr-0003-storage-layout.md`

- **Glossary**:
  - `glossary.md`

### Changed

- Initial version; no prior changes

### Notes

- Repository structure finalized
- Version 1.0.0 reflects complete baseline documentation of the homelab
