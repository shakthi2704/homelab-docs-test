# Standards – Documentation Rules

## Purpose

This document defines the **rules and best practices for creating, maintaining,
and versioning documentation** in the homelab and development infrastructure.

Ensures consistency, clarity, traceability, and ease of maintenance across all
design docs, runbooks, ADRs, and standards.

---

## Folder Structure

- `docs/design/` → Architecture, network, storage, container strategy, etc.
- `docs/runbooks/` → Operational step-by-step guides for each node
- `docs/decisions/` → ADRs (Architectural Decision Records)
- `docs/standards/` → Conventions, lifecycle, git workflow, documentation rules
- `docs/glossary.md` → Definitions of terms and abbreviations
- `CHANGELOG.md` → Versioned updates to documentation

---

## File Naming

- Use **numbered prefixes** for design docs (`00-overview.md`, `01-architecture.md`)
- Runbooks should be **organized by node** (`proxima/docker-runtime.md`)
- ADRs should use the format: `adr-<000X>-<short-description>.md`
- Use **lowercase letters, numbers, and dashes** only
- Avoid spaces and special characters

---

## Document Versioning

- Use Git for all documentation
- Commit changes with clear messages: `docs: update <doc-name>`
- Use **semantic versioning** for major updates in `CHANGELOG.md`
- Tag releases if needed for snapshot documentation

---

## Content Guidelines

- Each document should include:

  - **Purpose** – why it exists
  - **Scope** – what is included and excluded
  - **Procedures / Standards** – step-by-step or rules
  - **Notes** – additional context, warnings, or references

- Write in **clear, concise Markdown**
- Use **headings, bullet points, and tables** for readability
- Link to related documents when applicable

---

## Review and Approval

- Documentation must be **reviewed before promotion** to main branch
- ADRs and standards require **peer approval**
- Changes to critical runbooks or design docs should be **logged in CHANGELOG.md**

---

## Maintenance Rules

- Update documents immediately after workflow or architecture changes
- Archive obsolete documents rather than deleting them
- Ensure **links and references are kept up to date**
- Conduct periodic audits of the documentation repository

---

## Notes

- Consistent documentation ensures maintainable and reproducible infrastructure
- Follow all naming, versioning, and folder conventions strictly
- Deviations must be approved and documented
