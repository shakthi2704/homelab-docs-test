# Homelab & Development Infrastructure – Networking

## Document Context

This document defines the **logical networking model** for the homelab and
development infrastructure.

It builds on:

- `00-overview.md`
- `01-architecture.md`
- `02-node-roles.md`

This file describes **connectivity expectations and boundaries**, not physical
topology or configuration steps.

---

## Networking Design Goals

The networking model is designed to be:

- Simple and predictable
- Easy to reason about
- Secure by default through scope limitation
- Sufficient for development and internal services

Complex network segmentation is intentionally avoided unless justified by
actual requirements.

---

## Trust Model

The homelab operates within a **single trusted local network**.

- Nodes trust each other by placement, not by exposure
- No service is assumed to be internet-facing
- Internal access is the default

Security is achieved primarily through **non-exposure**, not perimeter defense.

---

## Node Connectivity Model

### Lyra (Development Node)

- Acts as a client on the network
- Initiates outbound connections to services
- Does not accept inbound service traffic

Lyra is a **consumer**, not a provider.

---

### Proxima (Runtime Node)

- Acts as the primary service endpoint
- Hosts internal-facing services
- Accepts inbound connections from trusted nodes only

Proxima is the **center of gravity** for service traffic.

---

### Nova (Access Node)

- Acts as a mobile client
- Initiates connections for administration and access
- Does not provide services

Nova mirrors Lyra’s network posture with fewer responsibilities.

---

### Rhea (Storage & Media Node)

- Provides media and file services
- Operates independently from development services
- Has no required dependency on Proxima or Lyra

Rhea remains network-adjacent but logically separate.

---

## Service Exposure Rules

Services follow strict exposure rules:

- Internal-only by default
- No public exposure without explicit design approval
- No direct exposure from development nodes
- No accidental exposure via convenience shortcuts

Any public-facing service requires:

- A documented design change
- Explicit justification
- Appropriate security controls

---

## Inter-Service Communication

- Services communicate only when necessary
- Monitoring services observe but do not control
- Development tooling does not directly manipulate runtime state

Implicit coupling between services is avoided.

---

## Future Networking Considerations

The architecture allows for future enhancements such as:

- Reverse proxies
- TLS termination
- Network segmentation

These are deferred until they provide clear, measurable value.

---

## Summary

The networking model prioritizes:

- Clarity over complexity
- Internal trust over public exposure
- Stability over experimentation

This keeps the system understandable and safe as it grows.
