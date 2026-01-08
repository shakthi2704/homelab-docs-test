# Runbook – Service Deployment on Proxima

## Purpose

Defines how Docker services are deployed inside existing LXC containers
on Proxima.

---

## Scope

- Docker service deployment inside LXC
- Monitoring services deployment (isolated LXC)
- Lifecycle control

Out of scope:

- LXC creation
- Docker engine configuration
- Development or sandbox workloads

---

## Deployment Rules

- Services deploy **only inside existing LXC containers**
- Correct class alignment is mandatory:
  - Core services → `core-services`
  - Monitoring services → `monitor-services`
- Persistent data must use Docker volumes

---

## Current Deployed Services

### Monitoring (`monitor-services`)

- Uptime Kuma
- Pulse
- Dozzle

Characteristics:

- Docker bridge networking
- Ports exposed via LXC IP
- Persistent Docker volumes in use

---

### Core Services (`core-services`)

- Gitea (Git service)
- Drone CI/CD server
- Drone Docker runner

Characteristics:

- Docker bridge networking
- Ports exposed via LXC IP
- Persistent Docker volumes for service data
- CI/CD workloads isolated from monitoring stack

## Service Exposure Model

- Docker containers use bridge networking
- Ports are published to the LXC interface
- Services are accessed via `LXC_IP:PORT`

---

## Operational Rulesvsvs

- Monitoring services must not manage application state
- Core services must not embed monitoring tooling
- All service changes must be intentional and documented

---

## Notes

- This document reflects deployed services only
- Future services are documented elsewhere after deployment
- Secrets and credentials are governed by `secrets-credential-management.md`
- All persistent infrastructure services MUST use restart: unless-stopped or equivalent Docker restart policy.
