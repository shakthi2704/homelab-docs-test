# Homelab & Development Infrastructure – Security Boundaries

## Document Context

This document defines the **security model and trust boundaries** of the homelab
and development infrastructure.

It builds on:

- `00-overview.md`
- `01-architecture.md`
- `02-node-roles.md`
- `03-networking.md`
- `04-storage.md`
- `05-container-strategy.md`

This file describes **where trust exists and where it stops**, not how security
controls are implemented.

---

## Security Philosophy

Security in this environment is achieved primarily through:

- Clear separation of responsibilities
- Minimal exposure
- Explicit trust boundaries
- Predictable system behavior

Complex security mechanisms are intentionally avoided unless required by real
risk.

---

## Trust Zones

### Local Trusted Network

All nodes operate within a **trusted local network zone**.

Assumptions:

- Physical access is controlled
- Devices are known and intentional
- Internal traffic is not hostile by default

This trust zone is the foundation of the security model.

---

### Node-Level Trust Boundaries

Each node has a defined trust posture.

---

#### Lyra — Development Trust Zone

- Trusted for code creation
- Not trusted for service hosting
- No inbound service exposure

A compromise of Lyra must not impact persistent services.

---

#### Proxima — Service Trust Zone

- Trusted to host long-running services
- Holds authoritative service data
- Accepts inbound connections from trusted nodes only

Proxima is the **highest-trust node** in the environment.

---

#### Nova — Access Trust Zone

- Trusted for access only
- No authority over data or services
- Limited impact if compromised

Nova is intentionally low-risk by design.

---

#### Rhea — Storage Trust Zone

- Trusted for media and file storage
- Isolated from development services
- No development authority

Rhea’s compromise must not affect development infrastructure.

---

## Container Isolation Boundaries

- Containers are isolated from the host
- LXC containers isolate service classes
- Monitoring containers are isolated from core services
- Experimental containers are isolated from authoritative data

Isolation failures must not cascade across responsibility boundaries.

---

## Access Control Principles

- Access is role-based by node
- Administrative access is intentional and minimal
- No anonymous or accidental access paths

If access cannot be clearly justified, it should not exist.

---

## Data Protection Boundaries

- Persistent data resides only on Proxima
- Containers do not own their data
- Development machines never hold authoritative service state

Data exposure is limited by **location**, not tooling.

---

## Security Change Management

Any change that affects:

- Trust assumptions
- Exposure scope
- Access paths

Requires:

1. Explicit review
2. Documentation update
3. An Architecture Decision Record (ADR)

Silent security changes are not allowed.

---

## Summary

The security model relies on:

- Clear boundaries
- Minimal exposure
- Explicit trust

When boundaries are respected, the system remains secure by design.
