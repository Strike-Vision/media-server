# 🎬 Media Server Stack

This repository contains a **Docker Compose** setup for a complete self-hosted media server.  
It includes everything you need to automate, organize, and stream your movies and TV shows — all in one stack.

---

## 📦 Services

| Service | Description |
|----------|-------------|
| **Sonarr** | Automates TV show downloads and management. |
| **Radarr** | Automates movie downloads and management. |
| **Prowlarr** | Indexer manager for Sonarr, Radarr, and other *arr apps. |
| **Jellyseerr** | Request management tool that integrates with Sonarr and Radarr. |
| **FlareSolverr** | Proxy server to bypass Cloudflare protection for indexers. |
| **Jellyfin** | Media server for streaming your movies and TV shows. |

---

## 🧱 Stack Overview

This project uses **Docker Compose** to orchestrate containers.  
Each service runs independently, connected through a shared Docker network.

### Example Directory Structure

```
/media-server/
│
├── docker-compose.yml
├── .env
├── config/
│   ├── sonarr/
│   ├── radarr/
│   ├── prowlarr/
│   ├── jellyseerr/
│   └── flaresolverr/
└── media/
    ├── movies/
    └── tv/
```

---

## 🚀 Getting Started

### Prerequisites
- [Docker](https://docs.docker.com/engine/install)
- Optional: [Tailscale](https://tailscale.com) or a reverse proxy for remote access.

### 1️⃣ Clone the repository
```bash
git clone https://github.com/<your-username>/media-server.git
cd media-server
```

### 2️⃣ Start the stack
```bash
docker compose up -d
```

### 3️⃣ Access your services

| Service | Port | URL |
|----------|------|-----|
| Sonarr | 8989 | http://localhost:8989 |
| Radarr | 7878 | http://localhost:7878 |
| Prowlarr | 9696 | http://localhost:9696 |
| Jellyseerr | 5055 | http://localhost:5055 |
| FlareSolverr | 8191 | http://localhost:8191 |
| Jellyfin | 8096 | http://localhost:8096 |

---

## 🎥 Jellyfin Setup Options

### 🐳 Option 1: Run Jellyfin in Docker (Recommended)
```yaml
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    ports:
      - "8096:8096"
    volumes:
      - ./config/jellyfin:/config
      - ./media:/media
    restart: unless-stopped
```
Warning: Hardware Transcoding does not work on windows with docker, Please install natively for Hardware Transcoding.

Start Jellyfin:
```bash
docker compose up -d jellyfin
```

---

### 💻 Option 2: Run Jellyfin Natively on Windows
1. Download the Windows version from [Jellyfin Downloads](https://jellyfin.org/downloads/).
2. Install and open Jellyfin.
3. Point your media libraries to your shared `/media` directory.
4. Allow port **8096** through Windows Firewall.

---

### 🐧 Option 3: Run Jellyfin Natively on Linux
```bash
# Debian / Ubuntu
curl -s https://repo.jellyfin.org/install-debuntu.sh | sudo bash

# Fedora / RHEL
sudo dnf install jellyfin

# Enable and start the service
sudo systemctl enable --now jellyfin
```

Access Jellyfin at [http://localhost:8096](http://localhost:8096)

---

## 🧩 Optional Add-ons

| Tool | Purpose |
|------|----------|
| **Bazarr** | Subtitle management for Sonarr/Radarr |
| **qBittorrent / NZBGet / SABnzbd** | Download clients |
| **Grafana + Prometheus** | Monitoring and container metrics |
| **Watchtower** | Automatic container updates |

---

## 🧠 Tips

- Use **Tailscale** or **Cloudflare Tunnel** for remote access.
- Backup `/config` folders regularly.
- Monitor disk usage — transcoding can consume a lot of temporary storage.

---

## 🧾 License

This project is licensed under the [MIT License](LICENSE).

---

## ❤️ Credits

- [Sonarr](https://sonarr.tv)
- [Radarr](https://radarr.video)
- [Prowlarr](https://prowlarr.com)
- [Jellyseerr](https://jellyseerr.dev)
- [FlareSolverr](https://github.com/FlareSolverr/FlareSolverr)
- [Jellyfin](https://jellyfin.org)
