# Homelab & Development Documentation

## Overview

This repository contains the full documentation of the homelab and development
infrastructure, including **design, operational runbooks, standards, decisions,
glossary, and changelog**. It provides a single source of truth for setup,
maintenance, and operational procedures.

---

## Design Documents

High-level architecture, node responsibilities, networking, storage, and
container strategies.

- [00-Overview](docs/design/00-overview.md) – Homelab & Development Infrastructure Overview
- [01-Architecture](docs/design/01-architecture.md) – Architecture and High-Level Layout
- [02-Node Roles](docs/design/02-node-roles.md) – Responsibilities of Lyra, Proxima, Nova, and Rhea
- [03-Networking](docs/design/03-networking.md) – Network design, addressing, and subnets
- [04-Storage](docs/design/04-storage.md) – Storage layout, volumes, and disks
- [05-Container Strategy](docs/design/05-container-strategy.md) – LXC and Docker strategy
- [06-Security Boundaries](docs/design/06-security-boundaries.md) – Security zones and access
- [07-Backup & Recovery](docs/design/07-backup-recovery.md) – Backup strategies and recovery
- [08-Failure Scenarios](docs/design/08-failure-scenarios.md) – Failure handling and mitigation
- [09-Design Principles](docs/design/09-design-principles.md) – Guiding principles

---

## Runbooks

Operational step-by-step guides for each node and service.

### Proxima (Proxmox)

- [Baseline Setup](docs/runbooks/proxima/baseline-setup.md)
- [LXC Management](docs/runbooks/proxima/lxc-management.md)
- [Docker Runtime](docs/runbooks/proxima/docker-runtime.md)
- [Service Deployment](docs/runbooks/proxima/service-deployment.md)

### Lyra (Fedora Dev)

- [Development Environment](docs/runbooks/lyra/dev-environment.md)
- [Docker Workflow](docs/runbooks/lyra/docker-workflow.md)
- [Image Promotion](docs/runbooks/lyra/image-promotion.md)

### Nova (Windows 11)

- [Access and Administration](docs/runbooks/nova/access-and-admin.md)

---

## Standards

Rules and best practices for naming, lifecycle, Git, and documentation.

- [Naming Conventions](docs/standards/naming-conventions.md)
- [Container Lifecycle](docs/standards/container-lifecycle.md)
- [Git Workflow](docs/standards/git-workflow.md)
- [Documentation Rules](docs/standards/documentation-rules.md)

---

## Architectural Decisions (ADRs)

Documented decisions with reasoning and consequences.

- [ADR 0001 – Docker in LXC](docs/decisions/adr-0001-docker-in-lxc.md)
- [ADR 0002 – No Full VMs](docs/decisions/adr-0002-no-vms.md)
- [ADR 0003 – Storage Layout](docs/decisions/adr-0003-storage-layout.md)

---

## Glossary

- [Glossary](docs/glossary.md) – Definitions and abbreviations used throughout documentation

---

## Changelog

- [CHANGELOG](CHANGELOG.md) – Version history of documentation

---

## Contribution Guidelines

1. **Clone the repository**
2. **Create a branch** for your changes:
   ```bash
   git checkout -b feature/<topic>
   ```
