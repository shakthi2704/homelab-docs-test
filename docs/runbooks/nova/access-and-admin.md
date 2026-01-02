# Runbook – Nova Access and Administration

## Purpose

This runbook defines the **access, administration, and operational boundaries**
for Nova (Windows 11 workstation) within the homelab and development
infrastructure.

It ensures Nova is used safely for administrative tasks and monitoring without
impacting Lyra, Proxima, or Rhea.

---

## Scope

- Nova workstation operations
- Administrative access to Proxima and Lyra
- Access to monitoring dashboards
- Temporary local development tools

Out of scope:

- Core service deployment
- Persistent container or storage operations
- Direct changes on Rhea (OMV) beyond file access

---

## Access Principles

1. **Minimal Privilege**

   - Administrative access only where required
   - Standard user for daily tasks
   - Elevated privileges for maintenance or configuration

2. **Scoped Responsibilities**

   - Nova can manage, monitor, or access nodes, but not host containers
   - No persistent data storage on Nova affecting core infrastructure

3. **Isolation**

   - Tools and access from Nova must not interfere with Proxima LXC containers
   - Development workflows are strictly on Lyra

4. **Observability**
   - Nova may be used for monitoring dashboards or remote access
   - Read-only access preferred where possible

---

## Administrative Workflow

1. **Access Nodes**

   - Use secure, trusted methods to connect to Lyra, Proxima, or Rhea
   - Verify identity and connection before performing any action

2. **Monitoring & Troubleshooting**

   - Observe service status and logs
   - Use Nova as an administrative console only

3. **Maintenance Tasks**

   - Limited to node configuration, backup triggers, or orchestration
   - Must follow documented runbooks and ADRs

4. **User Management**
   - Only create or manage accounts if authorized
   - Maintain audit trail for any changes

---

## Operational Boundaries

- Nova does not host services or containers
- No persistent storage of critical data
- Limited impact in case of compromise
- Acts as administrative, monitoring, and access node only

---

## Notes

- Nova is a **low-risk administrative node**
- All access and changes must be documented
- Any deviation from workflow requires ADR
