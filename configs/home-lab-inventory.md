# Home Lab Inventory & Config Reference

## Nodes

| Node    | Hostname | OS         | IP Address    | Role/Notes                    |
| ------- | -------- | ---------- | ------------- | ----------------------------- |
| Dev PC  | Lyra     | Fedora     | 192.168.8.101 | Development workstation       |
| Proxmox | Proxima  | Proxmox    | 192.168.8.102 | Container host (LXC + Docker) |
| Laptop  | Nova     | Windows 11 | 192.168.8.103 | Admin / remote work           |
| OMV     | Rhea     | OMV        | 192.168.8.104 | Media server / file sharing   |

---

## LXC Containers on Proxima

| Container Name    | Class   | Service / Role          | Docker Inside? | Persistent Volume          | Notes                   |
| ----------------- | ------- | ----------------------- | -------------- | -------------------------- | ----------------------- |
| core-git-01       | Core    | Gitea / Forgejo         | Yes            | proxima-core-git-vol       | Main local Git server   |
| monitor-uptime-01 | Monitor | Uptime Kuma             | Yes            | proxima-monitor-uptime-vol | Monitoring dashboard    |
| monitor-pulse-01  | Monitor | Pulse                   | Yes            | proxima-monitor-pulse-vol  | Observability           |
| sandbox-test-01   | Sandbox | Experimental containers | Yes            | ephemeral                  | Temporary / dev testing |

---

## Docker Ports & Mapping

| Container         | Service | Host Port | Container Port | Notes        |
| ----------------- | ------- | --------- | -------------- | ------------ |
| core-git-01       | Gitea   | 3000      | 3000           | Web UI       |
| core-git-01       | SSH     | 2222      | 22             | Git over SSH |
| monitor-uptime-01 | Web UI  | 8081      | 3001           | Dashboard    |
| monitor-pulse-01  | Web UI  | 8082      | 3000           | Dashboard    |

---

## Volumes

| Volume Name                | Host Path                       | Usage                 |
| -------------------------- | ------------------------------- | --------------------- |
| proxima-core-git-vol       | /mnt/pve/toshiba/core-git       | Persistent Git data   |
| proxima-monitor-uptime-vol | /mnt/pve/toshiba/monitor-uptime | Monitoring data       |
| proxima-monitor-pulse-vol  | /mnt/pve/toshiba/monitor-pulse  | Observability metrics |

---

## Notes

- IPs are **local LAN addresses**; update if network changes
- Ports are **mapped from container → host**; can be adjusted in runbooks
- Volumes should follow **naming-conventions** and backup rules
- This file is **for internal reference only**; do not commit sensitive credentials
- Update whenever a new container, service, or host is added
