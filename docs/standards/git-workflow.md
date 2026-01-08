# Standards – Git Workflow

## Purpose

This document defines the **Git workflow and branching strategy** for the homelab
and development infrastructure to ensure consistency, traceability, and
predictable promotion from Lyra to Proxima.

Applies to all code and container-related repositories.

---

## Repository Structure

- **Local repositories:** Gitea or Forgejo on Proxima
- **Remote repositories:** GitHub or GitLab for public access or backups
- **Directory organization:**

---

## Branching Strategy

- **main / master:** stable, production-ready code
- **develop:** integration branch for testing and pre-promotion code
- **feature/<name>:** feature development branches
- **hotfix/<name>:** urgent fixes for main branch
- **experiment/<name>:** ephemeral experiments, discarded after validation

---

## Commit Guidelines

- Use **clear, concise messages**
- Prefix with type where applicable:
- `feat:` new feature
- `fix:` bug fix
- `docs:` documentation changes
- `chore:` infrastructure or non-code updates
- Reference issue numbers when available
- One logical change per commit

---

## Promotion Workflow

1. **Development on Lyra**

- Work on `feature/<name>` or `experiment/<name>` branches
- Test containers locally

2. **Integration**

- Merge validated feature into `develop` branch
- Run automated tests if available

3. **Promotion to Proxima**

- Merge `develop` into `main` branch when ready for deployment
- Build and tag Docker images for production LXC containers
- Document promotion in runbooks

4. **Backup & Sync**

- Push all main/develop branches to remote repository (GitHub/GitLab)
- Ensure local copies on Proxima are synchronized with Lyra

---

## Versioning

- Follow **semantic versioning**: `MAJOR.MINOR.PATCH`
- Tag Docker images and Git commits for traceability
- Maintain a changelog (`CHANGELOG.md`) for repository updates

---

## Notes

- Git workflow ensures **reproducibility and traceability** across Lyra and Proxima
- Experimentation branches must never bypass the promotion workflow
- All repository and branch names must follow **naming-conventions.md**
- Deviations require documentation and justification in ADR or runbooks
