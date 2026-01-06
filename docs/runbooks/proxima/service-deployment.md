# Runbook – Service Deployment on Proxima

## Purpose

Defines how Docker services are deployed inside existing LXC containers
on Proxima.

---

## Scope

- Docker service deployment inside LXC
- Monitoring integration
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

### Core Services (`core-services`)

- Docker runtime only
- No application services deployed yet

---

## Service Exposure Model

- Docker containers use bridge networking
- Ports are published to the LXC interface
- Services are accessed via `LXC_IP:PORT`

---

## Operational Rules

- Monitoring services must not manage application state
- Core services must not embed monitoring tooling
- All service changes must be intentional and documented

---

## Notes

- This document reflects deployed services only
- Future services are documented elsewhere after deployment
