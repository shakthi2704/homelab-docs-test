# Homelab & Development Infrastructure – Overview

---

**Architecture Version:** 1.0  
**Status:** Stable  
**Last Updated:** 2026-01-01

---

## 1. Purpose of This Documentation

This repository is the **single source of truth** for the homelab and development infrastructure. It defines the architecture, responsibilities, standards, and operational intent of the environment.

The goal of this documentation is to ensure that the system:

- Is understandable after long gaps of time
- Can be rebuilt from first principles
- Evolves deliberately rather than accidentally

This documentation is treated as **infrastructure**, not notes.

---

## 2. Scope

This documentation covers:

- System architecture and node roles
- Container and virtualization strategy
- Development workflow and lifecycle
- Operational standards and guardrails

This documentation intentionally does **not** include:

- Secrets or credentials
- Host-specific IP addresses
- Temporary experiments
- One-off commands without context

---

## 3. Versioning Model

The documentation follows a **centralized versioning model**:

- The current architecture version is defined **only in this file**
- All design documents implicitly inherit this version
- Version changes are summarized in `CHANGELOG.md`

### Version Semantics

- **MAJOR version change (X.0)**

  - Fundamental architectural changes
  - Node role changes
  - Virtualization or orchestration model changes

- **MINOR version change (1.X)**

  - New sections added
  - Clarifications or refinements
  - Tooling additions without architectural impact

Runbooks are not strictly versioned; they evolve continuously.

---

## 4. Document Structure

The repository is structured as follows:

- `docs/design/` – Stable, high-level architecture and strategy
- `docs/runbooks/` – Step-by-step operational procedures
- `docs/decisions/` – Architecture Decision Records (ADR)
- `docs/standards/` – Naming, workflow, and lifecycle rules

Each folder has a clearly defined purpose and should not be misused.

---

## 5. Authoritative Design Reference

The authoritative architecture definition is located at:

- `docs/design/01-architecture.md`

All implementation guides, runbooks, and decisions must align with that document.

---

## 6. Change Discipline

All meaningful changes to architecture or standards must:

1. Be reflected in the relevant design document
2. Update the version here if required
3. Be recorded in `CHANGELOG.md`

Ad-hoc or undocumented changes are explicitly discouraged.

---

## 7. Intended Audience

This documentation is written for:

- The system owner (primary)
- A future version of the system owner
- Any technically competent operator who needs to understand or rebuild the system

It assumes basic familiarity with Linux, Docker, and Git.

---

## 8. Stability Statement

Architecture Version **1.0** represents a **stable baseline**. Changes beyond this point should be incremental and intentional.

This overview file acts as the **contract** between design and implementation.
