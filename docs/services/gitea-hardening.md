# Gitea Hardening Checklist

**Context:** Core-services LXC, Docker container, Phase 4  
**Goal:** Secure and stabilize Gitea as the central source control system

---

## 1. Access & Authentication

- [ ] Disable public user registration (`Settings → Configuration → Registration`)
- [ ] Set default repository visibility to **private**
- [ ] Disable anonymous access (read-only/public)
- [ ] Enforce SSH key–based Git access for all users
- [ ] Review admin accounts; remove any unnecessary users
- [ ] Configure strong password policy (if local accounts enabled)

---

## 2. Configuration & Persistence

- [ ] Confirm Docker volume mapping for Gitea data (`/data`)
- [ ] Ensure repository and config persistence across container restarts
- [ ] Verify timezone and base URL configuration
- [ ] Enable logging and confirm log rotation settings
- [ ] Record container environment variables (PUID, PGID, TZ, ports)

---

## 3. Repository & Organization Structure

- [ ] Create infrastructure organization/group
- [ ] Create baseline repositories:
  - [ ] `infra-docs`
  - [ ] `docker-stacks`
  - [ ] `home-lab-config`
- [ ] Initialize README.md in each repo
- [ ] Configure branch protection rules for critical repos

---

## 4. Network & Security

- [ ] Route Gitea through reverse proxy (Traefik / Nginx Proxy Manager)
- [ ] Enable HTTPS / TLS certificates
- [ ] Limit external access if not required (firewall / port exposure)
- [ ] Optionally enable fail2ban / brute-force protection

---

## 5. Backup & Recovery

- [ ] Create backup routine for `/data` volume
- [ ] Schedule LXC snapshots of core-services container
- [ ] Test restore procedure for at least one repository
- [ ] Document backup location, frequency, and retention policy

---

## 6. Monitoring & Maintenance

- [ ] Integrate Gitea container into Prometheus / Grafana monitoring
- [ ] Enable container auto-update policy (manual for now)
- [ ] Document version and update procedure
- [ ] Schedule regular configuration reviews
