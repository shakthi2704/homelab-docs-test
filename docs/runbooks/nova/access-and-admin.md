# Runbook – Nova Access and Administration

> Status: Phase 1 (Day-0 Infrastructure) — Role and access validated

## Purpose

This runbook defines the **access, administration, and operational boundaries**
for Nova (Windows 11 workstation) within the homelab.

It ensures Nova is used safely for administrative tasks and monitoring without
impacting Lyra, Proxima, or Rhea.

---

## Scope

- Nova workstation operations
- Administrative access to Proxima and Lyra (SSH / RDP)
- Access to monitoring dashboards (read-only)
- Temporary local documentation or non-critical tools

Out of scope:

- Core service deployment
- Persistent container or storage operations
- Direct changes on Rhea (OMV) beyond file access

---

## Access Principles

1. **Minimal Privilege**

   - Administrative access only where required
   - Standard user for daily tasks
   - Elevated privileges only for authorized maintenance or configuration

2. **Scoped Responsibilities**

   - Nova can access nodes and monitor services
   - Cannot host containers or manage persistent data
   - No authority over core infrastructure

3. **Isolation**

   - Tools and access from Nova must **not interfere** with Proxima or Lyra
   - Development workflows remain strictly on Lyra

4. **Observability**

   - Nova is used for monitoring dashboards or remote administrative access
   - Read-only access preferred where possible

---

## Administrative Workflow (Phase 1 Validated)

1. **Access Nodes**

   - Use secure, trusted methods (SSH / RDP) to connect to Lyra, Proxima, or Rhea
   - Verify identity and connection before any action

2. **Monitoring & Troubleshooting**

   - Observe service status and logs
   - Nova serves only as an administrative console

3. **Maintenance Tasks**

   - Limited to configuration, backup triggers, or reading dashboards
   - Must follow documented runbooks and ADRs

4. **User Management**

   - Only create or manage accounts if explicitly authorized
   - Maintain audit trail for all changes

---

## Operational Boundaries

- Nova **does not host services or containers**
- No persistent storage of critical data
- Limited impact in case of compromise
- Acts solely as **administrative, monitoring, and access node**

---

## Notes

- Nova is a **low-risk administrative node**
- All access and changes must be documented
- Any deviation from workflow requires an ADR
- **Phase 1 verified:** role, connectivity, and access confirmed; no infra changes performed

# Nova – Access & Admin Runbook

## Purpose

Defines how Nova interacts with the home-lab environment.  
Covers access to nodes, LXC containers, documentation, and optional Docker client usage.

---

## 1. Network & Connectivity

- Nova IP: `192.168.8.30`
- Confirm connectivity to home-lab nodes:
  - `ping 192.168.8.20` → Proxima host
  - `ping 192.168.8.21` → core-services LXC
  - `ping 192.168.8.22` → monitor-services LXC

---

## 2. SSH Access

- Nova SSH keys stored locally (if needed)
- SSH into Proxima host (no root access to LXC):
  ```powershell
  ssh admin@192.168.8.20
  ```
