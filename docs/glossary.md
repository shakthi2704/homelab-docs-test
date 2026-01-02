# Glossary

## Nodes

- **Lyra** – Fedora development workstation, main dev environment
- **Proxima** – Proxmox server, container and runtime host
- **Nova** – Windows 11 workstation, administrative node
- **Rhea** – OMV server, media and file storage (out of main dev scope)

---

## Containers & Virtualization

- **LXC (Linux Containers)** – Lightweight OS-level containers on Proxima
- **Docker** – Containerization platform for applications, running inside LXC on Proxima or directly on Lyra
- **VM (Virtual Machine)** – Full OS virtualization; avoided in homelab as per ADR 0002

---

## Service Classes

- **Core** – Production or critical services (e.g., GitLab, Git)
- **Monitoring** – Observability services (e.g., Pulse, Uptime Kuma, Dozzle)
- **Experimental / Sandbox** – Development or testing containers/images

---

## Workflows

- **Lifecycle** – Container lifecycle: Create → Operate → Update → Promote → Retire
- **Promotion** – Moving a container or image from Lyra (dev) to Proxima (production)
- **Runbook** – Step-by-step operational guide for a node or service
- **ADR** – Architectural Decision Record; documents decisions with reasoning and consequences

---

## Git & Versioning

- **Repository** – A collection of source code, Dockerfiles, and documentation
- **Branch** – Isolated line of development in Git (feature, develop, main)
- **Semantic Versioning (SemVer)** – Versioning format: MAJOR.MINOR.PATCH
- **Changelog** – Log of updates and changes to the documentation or repository

---

## Miscellaneous

- **Host** – The physical or virtual machine that runs containers
- **Volume** – Persistent storage attached to a container
- **Observability** – Metrics, logs, and monitoring for services
- **Ephemeral** – Temporary or disposable container/workload
