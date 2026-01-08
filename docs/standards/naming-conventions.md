# Standards – Naming Conventions

## Purpose

This document defines **naming rules and conventions** for the homelab and
development infrastructure to ensure clarity, consistency, and traceability.

All nodes, containers, services, images, and volumes should follow these rules.

---

## Node Naming

| Node       | Name    | Description                   |
| ---------- | ------- | ----------------------------- |
| Fedora Dev | Lyra    | Main development workstation  |
| Proxmox    | Proxima | Container and runtime host    |
| Windows    | Nova    | Administrative workstation    |
| OMV        | Rhea    | File sharing and media server |

- Use **short, memorable names** for nodes
- Node names are used in container, volume, and service references

---

## LXC Container Naming

## Format:

- `<class>` → core, monitor, sandbox
- `<service>` → service name or role abbreviation
- `<index>` → optional numeric suffix if multiple instances exist

**Examples:**

- `core-git-01` → first core Git service container
- `monitor-uptime-01` → monitoring container for Uptime Kuma
- `sandbox-test-01` → experimental container

---

## Docker Container Naming

Format:

- `<class>` → core, monitor, sandbox
- `<service>` → service name or role abbreviation
- `<index>` → optional numeric suffix if multiple instances exist

**Examples:**

- `core-git-01` → first core Git service container
- `monitor-uptime-01` → monitoring container for Uptime Kuma
- `sandbox-test-01` → experimental container

---

## Docker Container Naming

Format:

- `<lxc-class>` → core, monitor, sandbox
- `<service>` → service name
- `<env>` → dev, test, prod (optional for clarity)

**Examples:**

- `core-git-dev` → development Git container in core class
- `monitor-pulse-prod` → production Pulse monitoring container

---

## Volume Naming

Format:

- `<node>` → hosting node (Proxima)
- `<lxc>` → LXC container name
- `<service>` → service inside container
- `vol` → literal suffix to identify as volume

**Examples:**

- `proxima-core-git-vol` → persistent volume for Git core container
- `proxima-monitor-uptime-vol` → volume for Uptime monitoring

---

## Image Naming

Format:

- `<service>` → name of service
- `<version>` → semantic version or timestamp for traceability

**Examples:**

- `gitlab:1.0.0` → first version of GitLab image
- `pulse:20260102` → Pulse image built on Jan 2, 2026

---

## General Rules

1. Use **lowercase letters**, digits, and dashes only
2. Avoid spaces or special characters
3. Names must be **unique within their scope**
4. Document any deviations from the standard
5. Consistency is mandatory for automated scripts, monitoring, and backups

---

## Notes

- Naming conventions apply to all nodes, containers, Docker images, and volumes
- Following conventions ensures **predictable management and easier troubleshooting**
- Any new service or node must adhere to these rules
