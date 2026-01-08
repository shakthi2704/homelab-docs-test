# Secrets & Credential Management

## Purpose

Define how secrets and credentials are handled for services deployed
inside LXC containers on Proxima, ensuring security, clarity, and
documentation accuracy without introducing unnecessary tooling.

---

## Scope

In scope:

- Secrets required by deployed core services
- Local credential handling inside Docker and service data volumes
- Manual secret lifecycle management

Out of scope:

- External secrets managers (Vault, SOPS, etc.)
- Encrypted Git repositories
- Cloud IAM or third-party credential providers
- Kubernetes or orchestration-level secrets

---

## Secrets in Use

### Gitea

- Admin account credentials
- User account credentials
- SSH public/private keys for Git access
- Repository access tokens (if enabled)

### Drone CI/CD

- `DRONE_RPC_SECRET`
- Repository activation tokens
- Pipeline-level secrets (defined in Drone UI, not in Git)

---

## Storage Locations

- Gitea secrets stored internally within Gitea data volume
- Drone secrets stored in Drone server data directory
- Runtime secrets injected via Docker environment variables
- Docker volumes provide persistence across container restarts

Explicitly prohibited:

- Plaintext secrets committed to Git repositories
- Secrets stored in documentation files
- `.env` files tracked in version control

---

## Handling Rules

- Secrets are created manually during service setup
- Secrets rotation is manual and event-driven
- SSH keys are user-managed and reviewed periodically
- Access is limited to administrators of `core-services`
- Service containers must be restarted after secret changes

---

## Explicit Non-Goals

The following are intentionally NOT used:

- HashiCorp Vault
- Mozilla SOPS
- Ansible Vault
- Kubernetes Secrets
- Cloud-based secret managers
- Automated secret rotation
- Encrypted configuration repositories

This is a deliberate design decision to maintain simplicity and control.

---

## Notes

- This document reflects the current deployed state only
- Any change to secret handling must be documented before implementation
- Future enhancements require explicit scope approval
