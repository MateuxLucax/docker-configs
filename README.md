# Docker Utils 🐳

A collection of Docker Compose configurations for self-hosted services. Each service is organized in its own directory with proper environment variable management.

## 🏗️ Services

### 🎬 Media & Entertainment
- **[Jellyfin](./media/)** - Media server for movies, TV shows, and music with hardware acceleration
- **[Radarr](./media/)** - Movie collection manager 
- **[Sonarr](./media/)** - TV series collection manager
- **[Prowlarr](./media/)** - Indexer manager for *arr stack
- **[Transmission](./media/)** - BitTorrent client with Flood UI
- **[YouTube-DL Material](./youtubedl-material/)** - Web UI for youtube-dl

### 🔐 Security & Productivity  
- **[Vaultwarden](./vaultwarden/)** - Bitwarden-compatible password manager
- **[n8n](./n8n/)** - Workflow automation platform
- **[Stirling PDF](./stirling-pdf/)** - PDF manipulation tools

### 🎮 Gaming
- **[Minecraft](./minecraft/)** - Minecraft server with RCON management

### 🌐 Infrastructure
- **[Cloudflared](./cloudflared/)** - Cloudflare Tunnel for secure remote access
- **[Watchtower](./watchtower/)** - Automatic Docker container updates
- **[Monitoring](./monitoring/)** - Prometheus + Grafana monitoring stack

### 🌍 Personal
- **[mateux.dev](./mateux-dot-dev/)** - Personal website
- **[RSLP Checker](./rslp-checker/)** - Custom Portuguese stemming tool

## 🚀 Quick Start

1. Clone this repository:
   ```bash
   git clone https://github.com/MateuxLucax/docker-utils.git
   cd docker-utils
   ```

2. Navigate to the service you want to deploy:
   ```bash
   cd media  # or any other service directory
   ```

3. Copy the example environment file:
   ```bash
   cp .env.example .env
   ```

4. Edit the `.env` file with your specific configuration:
   ```bash
   nano .env
   ```

5. Start the services:
   ```bash
   docker compose up -d
   ```

## 📁 Project Structure

```
docker-utils/
├── service-name/
│   ├── docker-compose.yml    # Service configuration
│   ├── .env.example         # Environment template  
│   ├── .env                 # Your local config (git-ignored)
│   └── additional-configs/  # Service-specific files
```

## 🔧 Environment Variables

Each service uses environment variables for configuration. Key patterns:

- `DOCKER_VOLUME_PATH` - Base path for Docker volumes (usually `./data`)
- `PUID`/`PGID` - User/group IDs for file permissions (usually `1000`)
- `TZ` - Timezone (e.g., `America/Sao_Paulo`)

## 🌐 Network Architecture

Services use Docker networks for isolation:
- `tunnel` - Services exposed via Cloudflare Tunnel
- `services` - Internal service communication  
- `torrent` - Torrent-related services

## 🔒 Security Notes

- All `.env` files are git-ignored to prevent credential leaks
- Example files use placeholder values
- Services run with resource limits
- Non-root user configuration where applicable

## 📋 Prerequisites

- Docker & Docker Compose
- Sufficient disk space for media storage
- Domain name (for tunnel services)

## 📄 License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.
