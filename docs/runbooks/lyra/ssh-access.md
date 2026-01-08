# Lyra SSH Access – Baseline

## Purpose

Validate Lyra can access Proxima host for infrastructure operations.

## Steps

1. Check local user and SSH keys.
2. Generate key if missing.
3. Add Lyra public key to `/root/.ssh/authorized_keys` on Proxima host.
4. Test SSH connectivity: `ssh root@192.168.8.20`.

## Notes

- Root SSH access to LXC is intentionally disabled.
- Management of LXC is done via `pct enter <vmid>` or Proxmox Web UI.
