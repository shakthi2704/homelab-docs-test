# Lyra Docker Client – Baseline

## Purpose

Allow Lyra to inspect or manage Docker stacks remotely.

## Steps

1. Install Docker client.
2. Test connection to Proxima host using `docker -H ssh://root@192.168.8.20`.
3. Confirm container visibility: `docker ps`.

## Notes

- Lyra is not intended to run production containers.
- Any destructive operations must be coordinated with Proxima host.
