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

---

## [1.1.0] – 2026-01-05

### Added / Updated

- **Phase 1 – Day-0 Infrastructure Deployment**:

  - Inventory (`configs/home-lab-inventory.md`) updated with verified IPs and roles
  - Node roles (`docs/design/02-node-roles.md`) updated to reflect locked responsibilities
  - Networking (`docs/design/03-networking.md`) updated with confirmed IP assignments
  - Runbooks updated to reflect as-built state:
    - Proxima: `baseline-setup.md` (host ready, storage recognized, SSH tested)
    - Nova: `access-and-admin.md` (access, monitoring, and boundaries verified)
  - Phase 1 status markers added to all files for clarity
  - Documentation reflects **current deployed reality**, not planned future state

### Notes

- Phase 1 completes **baseline validation**:
  - Node hostnames, IPs, and connectivity verified
  - SSH trust model implemented
  - Minimal host setups confirmed
  - No containers or services deployed yet
- Provides a **stable foundation** for Phase 2 (storage mounts and container deployment)

---

## [1.2.0] – 2026-01-06

### Added / Updated

- **Phase 2 – Core Services LXC Deployment**:

  - Inventory (`configs/home-lab-inventory.md`) updated with **core-services LXC**:
    - IP: `192.168.8.21`
    - Role: Docker host for Gitea and future containers
  - Runbooks updated:
    - Proxima: `docker-runtime.md` now includes **Gitea deployment** with admin email `lyra@proxima.com`
  - LXC container `core-services` created on Proxima using Ubuntu 22.04 template
  - Docker runtime verified and active inside `core-services` container
  - Volumes created for persistent service data (`proxima-core-vol`)
  - Phase 2 status markers added to all files for clarity

### Notes

- Phase 2 reflects **live container deployment** for core services
- Docker lifecycle rules enforced: create → promote → operate → retire
- Gitea is running with web UI accessible (`3000`) and SSH Git (`2222`)
- Documentation now represents **current deployed state of core services** within LXC
