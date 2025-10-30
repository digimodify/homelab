# Homepage Dashboard

Short README for the homelab `homepage` project. This instance runs on Proxmox LXC containers and hosts a number of self-hosted services (see `config/services.yaml`). The media stack (Jellyfin + related apps) is run in Docker.

## Overview

- Host: Proxmox VE (LXC containers for services).
- Install helpers: community helper scripts are used to provision many services.
- Homepage: uses a configurable homepage/dashboard driven by the `config/*.yaml` files in this repo.
- Media stack: Docker containers for Jellyfin and related tooling (Radarr, Sonarr, Prowlarr, Bazarr, Jellyseerr, qBittorrent, etc.).

## What you'll find in this repo

- `config/services.yaml` — service entries and widget configuration for the homepage (contains template variables like `HOMEPAGE_VAR_*`).
- `config/bookmarks.yaml`, `config/settings.yaml`, `config/widgets.yaml` — other homepage configuration files.
- `config/example.env` — example environment file with the `HOMEPAGE_VAR_*` variables (safe to commit; contains placeholders only).

## How it was installed (notes)

- Proxmox: LXC containers were used for the homepage and many services.
- Many services were installed using community/helper scripts (see links below).
- The media stack (Jellyfin + automation apps) runs in Docker. Portainer is present (see `services.yaml`) and can be used to manage containers if needed.

## Quick management commands

Use these on the host/container where Docker is installed (adjust for your setup):

- List running containers:
  - `docker ps`
- Show all containers:
  - `docker ps -a`
- Start the Docker stack (if using compose):
  - `docker compose -f docker-compose.yml up -d`
  - or `docker-compose -f docker-compose.yml up -d` depending on how compose is installed.
- Stop the stack:
  - `docker compose -f docker-compose.yml down`
- View logs:
  - `docker compose -f docker-compose.yml logs -f <service>`

Proxmox/LXC tips:

- Use the Proxmox web UI for snapshots, container management, and backups.
- Use the Proxmox Backup Server (PBS) for backups if configured.

Homepage configuration notes

- `config/services.yaml` contains service entries with placeholders like `{{HOMEPAGE_VAR_JELLYFIN_URL}}` or `{{HOMEPAGE_VAR_PROXMOX_URL}}`. Those are substituted at runtime by your homepage app or via environment variables — keep secrets out of the repo.

## Troubleshooting quick wins

- If homepage widgets don't show data: verify the service URL, API key, and credentials referenced by the `HOMEPAGE_VAR_*` variables.
- If media services are unavailable: check Docker container status and logs with `docker ps` and `docker logs` (or Portainer).
- For LXC/container issues: check Proxmox tasks and container console from the Proxmox UI.

## Links & resources

- Proxmox community scripts (helper scripts used): https://community-scripts.github.io/ProxmoxVE/scripts
- Homepage project: https://gethomepage.dev/
- Example homelab repo used as reference: https://github.com/ChristianLempa/homelab/tree/main/homepage
- YouTube setup videos referenced by user:
  - https://youtu.be/mC3tjysJ01E?si=EUpCFYTTmRZdGgon
  - https://youtu.be/j9kbQucNwlc?si=5y5U1D-rzgfb0LaL

## Assumptions

- Docker (and optionally Docker Compose) is installed on the host/container running the media stack.
- Portainer is available for GUI-based container management (per `services.yaml`).
- Secrets and credentials (the `HOMEPAGE_VAR_*` values) are managed outside the repo (environment variables, vault, or a `.env` file excluded from git).

## Next steps / suggestions

- Add a `config/example.env` (without secrets) that documents required `HOMEPAGE_VAR_*` variables.
- A `config/example.env` has been added to this repo with the discovered variable names; fill values locally and DO NOT commit real secrets.
- Add a short `docker-compose.yml` or a note pointing to where the Docker stack is defined (if not already present).
- Consider documenting LXC templates or helper script commands used to build each container for reproducibility.
- Add backup/restore instructions (Proxmox LXC snapshots, PBS procedures).

---

- Add a `config/example.env` with the discovered variable names.
- Add a short `docker-compose.yml` template for the media stack.
- Expand troubleshooting with exact commands from your environment.
