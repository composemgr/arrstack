## 👋 Welcome to arrstack 🚀

Complete *arr media automation stack (Sonarr, Radarr, Prowlarr, etc)

## 📋 Description

Complete *arr media automation stack (Sonarr, Radarr, Prowlarr, etc)

## 🚀 Services

- **sonarr**: ghcr.io/hotio/sonarr:latest
- **radarr**: ghcr.io/hotio/radarr:latest
- **lidarr**: ghcr.io/hotio/lidarr:latest
- **readarr**: ghcr.io/hotio/readarr:latest
- **prowlarr**: ghcr.io/hotio/prowlarr:latest
- **whisparr**: ghcr.io/hotio/whisparr:latest
- **bazarr**: ghcr.io/hotio/bazarr:latest
- **jackett**: ghcr.io/hotio/jackett:latest
- **unpackerr**: ghcr.io/hotio/unpackerr:latest
- **overseerr**: ghcr.io/hotio/overseerr:latest
- **transmission**: linuxserver/transmission:latest
- **metube**: alexta69/metube:latest
- **audiobookshelf**: ghcr.io/advplyr/audiobookshelf:latest
- **homarr**: ghcr.io/homarr-labs/homarr:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/arrstack/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/arrstack" ~/.local/srv/docker/arrstack
cd ~/.local/srv/docker/arrstack
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install arrstack
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
SERVICE_USER=1000
SERVICE_GROUP=1000
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:8989

## 📂 Volumes

- `./rootfs/config/sonarr` - Data storage
- `./rootfs/data/media/tv` - Data storage
- `./rootfs/data/downloads` - Data storage
- `./rootfs/config/radarr` - Data storage
- `./rootfs/data/media/movies` - Data storage
- `./rootfs/config/lidarr` - Data storage
- `./rootfs/data/media/music` - Data storage
- `./rootfs/config/readarr` - Data storage

## 🔍 Logging

```shell
docker compose logs -f sonarr
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
