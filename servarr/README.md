# Self-Hosted Media Server

## Servarr Stack

### Services included

- `gluetun` — VPN client (WireGuard/OpenVPN) that routes container traffic through your VPN provider; provides a local HTTP proxy and port‑forwarding support.
- `qbittorrent` — Torrent client (linuxserver/qbittorrent) configured to use gluetun's network (`network_mode: "service:gluetun"`).
- `sabnzbd` — Usenet download client with a web UI (LinuxServer image).
- `bazarr` — Subtitle downloader that integrates with Radarr/Sonarr.
- `jellyfin` — Media server for serving video and audio to clients.
- `jellyseerr` — Request manager for Jellyfin (request/approval workflow).
- `prowlarr` — Indexer manager (search index orchestration for *Arr apps).
- `radarr` — Movie library manager and automated movie downloader.
- `sonarr` — TV series library manager and automated episode downloader.
- `flaresolverr` — Cloudflare‑bypass proxy used by some indexers and scrapers.
- `unpackerr` — Monitors download clients, extracts archives, and hands completed items to *Arr apps.

This folder contains a docker-compose stack for a small media setup using Jellyfin and the "Arr" Stack

## Quick steps to deploy

1. Create a local environment file from the example (do NOT commit the real `.env`):

   cp example.env .env

2. Edit `.env` and fill in your values (WireGuard/OpenVPN keys, `FORWARDED_PORT`, `FOLDER_FOR_CONFIGS`, `FOLDER_FOR_MEDIA`, `PUID`, `PGID`, timezone, API keys, etc.).

3. Ensure host folders exist and have the correct permissions:

   mkdir -p /opt/servarr/configs
   mkdir -p /data
   chown -R 1000:1000 /opt/servarr /data

4. Start the stack from this directory:

   docker-compose up -d

## Notes
- qBittorrent is configured to run inside the `gluetun` service network (`network_mode: "service:gluetun"`) so traffic is routed through the VPN — do not change this unless you understand the privacy implications.
- Keep your real `.env` out of the repository; commit only `example.env` or `.env.example` with placeholders.
- If the compose file uses `${VAR:?err}` and a variable is missing, Docker Compose will error; ensure required variables are set in `.env`.

## References
- TechHutTV Jellyfin repo: https://github.com/TechHutTV/homelab/tree/main/media/jellyfin
- TechHutTV Jellyfin setup: https://www.youtube.com/watch?v=eJvQKLVrmU8
- BlueMonkey 4n6: https://youtu.be/uu9PvIBYrWk?si=YawIY_ATB1vvGiEK
