# Homelab & Development Infrastructure – Backup & Recovery

## Document Context

This document defines the **backup and recovery intent** for the homelab and
development infrastructure.

It builds on:

- `00-overview.md`
- `01-architecture.md`
- `02-node-roles.md`
- `03-networking.md`
- `04-storage.md`
- `05-container-strategy.md`
- `06-security-boundaries.md`

This file defines **what must be recoverable and why**, not how backups are
performed.

---

## Backup Philosophy

Backups exist to support **recovery**, not archival perfection.

The strategy prioritizes:

- Service continuity
- Data integrity
- Predictable restoration paths

Anything that cannot be restored is treated as disposable.

---

## Recovery Objectives

The environment is designed to support:

- Rebuilding any compute node from scratch
- Restoring service data independently of compute
- Recovering from single-node failure without architectural changes

Perfect uptime is not a goal; **recoverability is**.

---

## Data Recovery Scope

### Authoritative Data (Must Be Recoverable)

The following data must always be recoverable:

- Local Git repositories
- Service databases
- Service configuration data
- Persistent container volumes

This data is considered **critical**.

---

### Non-Authoritative Data (Disposable)

The following data does not require backup:

- Development containers
- Build artifacts
- Cache data
- Temporary logs

Loss of this data must not impact recovery.

---

## Node-Level Recovery Expectations

### Lyra

- Can be rebuilt at any time
- No recovery requirements beyond source code
- No dependency on backups for infrastructure continuity

---

### Proxima

- Must support full service restoration
- Loss of compute must not imply loss of data
- Recovery focuses on restoring services, not host state

---

### Nova

- No recovery requirements
- Treated as disposable access tooling

---

### Rhea

- Backup scope limited to media and file data
- Not part of development recovery objectives

---

## Container Recovery Model

- Containers are recreated, not restored
- Data is restored separately from containers
- Configuration is reapplied, not recovered blindly

Recovery favors **known-good redeployment** over snapshot resurrection.

---

## Backup Boundary Rules

- Only authoritative data is backed up
- Backups do not include ephemeral state
- Backup scope is explicit and minimal

Expanding backup scope requires justification.

---

## Recovery Testing Principle

Backups are only considered valid if:

- Restoration is possible
- Recovery steps are documented
- Recovery does not rely on tribal knowledge

Testing cadence is defined in runbooks.

---

## Summary

The backup and recovery model ensures:

- Data survives hardware failure
- Services are reproducible
- Recovery remains predictable

The system is designed to fail safely and recover cleanly.
