# Proxmox Homelab

 ![homepage-dashboard](assets/dash-screenshot.png)

This repository contains configuration and docker-compose stacks used to run a compact home lab for media and other services.


Navigation
- [homepage](./homepage/) — the main homepage/dashboard and its configuration (bookmarks, widgets, settings).
- [servarr](./servarr/) — media/App stacks: Gluetun (VPN), qBittorrent, Radarr, Sonarr, Jellyfin, and helpers. See `servarr/README.md` for details.

Hardware
- I will describe infra here (fill in CPU, RAM, storage, hypervisor/LXC/Docker host, network layout, VLANs, and IP addresses). Example fields you might include:
  - Host machine: model, CPU, RAM, OS
  - Storage layout: disks, RAID, mount points
  - Network: bridge names, VLANs, subnet ranges
  - Backup targets: NAS or cloud

Quick deploy guidance
- Per-project READMEs contain project-specific deployment steps. Typical workflow:

  1. Review the project's README. Example: `cd servarr && less README.md`.
  2. Copy the example environment file and edit local values (do NOT commit secrets):

     cp example.env .env
     # edit .env with your private keys and host paths

  3. Create any required host directories and set permissions (update UID/GID as needed):

     mkdir -p /opt/servarr/configs
     mkdir -p /data
     chown -R 1000:1000 /opt/servarr /data

  4. Start the service:

     docker-compose up -d

Security & secrets
- This repo should NOT contain secrets. Use `example.env` or `.env.example` files with placeholders and keep the real `.env` local. Add `.env` to your `.gitignore`.
- Services that route traffic through a VPN (for example `qBittorrent` using `gluetun`) are configured intentionally for privacy — do not change network settings without understanding the implications.

Suggested additional sections to add to this README
- Inventory: list hardware, model numbers, serials, and firmware versions.
- Network diagram: ASCII or an image showing subnet ranges, VLANs and device roles.
- Backups: what to back up, where, frequency, restore steps.
- Monitoring & alerts: metrics, dashboards, and alert rules (Prometheus, Grafana, UptimeRobot, etc.).
- Secrets & Vault: how you store secrets (passphrases, Ansible Vault, Bitwarden, etc.).
- Automation: scripts, cron jobs, or Ansible playbooks used to provision and maintain the lab.
- Change log / Runbook: notable changes, maintenance windows, and runbook for common failures.

Contributing
- Prefer creating a branch and a pull request. Do not add real credentials or private keys to commits — use placeholders in committed example files.

License
- Add a LICENSE file at the repo root if you want to publish this publicly.

Need help?
- If you want, I can:
  - generate a polished `.env.example` for each project (placeholders only),
  - add a root-level `.gitignore` (ignoring `.env`, logs),
  - create a network diagram stub or sample hardware inventory template.

Fill in the hardware section and any project-specific notes and I'll update the README accordingly.
# homelab
