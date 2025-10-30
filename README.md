# Proxmox Homelab

 ![homepage-dashboard](assets/dash-screenshot.png)

This repository contains configuration and docker-compose stacks used to run a compact home lab for media and other services.


Navigation
- [homepage](./homepage/) — the main homepage/dashboard and its configuration (bookmarks, widgets, settings).
- [servarr](./servarr/) — media/App stacks: Gluetun (VPN), qBittorrent, Radarr, Sonarr, Jellyfin, and helpers. See `servarr/README.md` for details.

Hardware
- Lenovo ThinkCentre M720q (primary) — 16GB RAM, 500GB
- Intel NUC NUC8i5BEK ×2 (secondaries) — 16GB RAM, 500GB each
- Intel NUC (NFS storage) — 500GB
- TP-Link TL-SG108E (managed switch)
- Ubiquiti UAP-AC-Pro (access point)
- Backup target: external HDD + SSD

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



