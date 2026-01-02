# Runbook – Lyra Development Environment

## Purpose

This runbook defines the **setup and usage of Lyra** as a development node.  
It ensures a consistent workflow for building, testing, and preparing containers
for promotion to Proxima.

---

## Scope

- Lyra (Fedora development workstation)
- Local Docker and development containers
- Source code management and build artifacts
- Workflow alignment with Proxima promotion

Out of scope:

- Runtime service deployment
- Persistent container hosting
- Monitoring and observability for production

---

## Development Environment Principles

1. **Ephemeral Workloads**

   - Containers on Lyra are short-lived
   - Safe to destroy or rebuild at any time
   - No persistent state except local source code

2. **Docker-First Workflow**

   - All development and testing occur inside Docker containers
   - No processes run natively outside containers if avoidable

3. **Promotion Path**

   - Containers or images built on Lyra are prepared for Proxima
   - Only validated containers are promoted

4. **Isolation**

   - Development containers are isolated from host system
   - No interference with Proxima or other nodes

5. **Observability**
   - Logs and outputs are available locally
   - Optional integration with monitoring on Proxima

---

## Workflow Overview

1. **Code Development**

   - Write and test code inside Docker containers
   - Use local volumes for source code

2. **Build & Test Containers**

   - Build images or containers for the service
   - Run tests and validation locally

3. **Promotion Preparation**

   - Validate readiness for Proxima deployment
   - Document changes and configuration

4. **Clean Up**
   - Remove ephemeral containers when no longer needed
   - Keep only essential artifacts for promotion

---

## Resource & Isolation Rules

- Containers should use limited CPU and memory
- Host system remains stable and unpolluted
- Volumes are temporary unless part of source code or promotion pipeline
- Experimental workloads are isolated

---

## Notes

- Lyra is **disposable from a system perspective**, but source code must persist
- All work prepares for promotion to Proxima
- Any deviation from workflow should be documented and justified
