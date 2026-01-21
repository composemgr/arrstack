## 👋 Welcome to arrstack 🚀

Arrstack - Complete media automation stack (Sonarr, Radarr, Prowlarr, etc.)

## 📋 Description

Complete media automation stack including Sonarr (TV), Radarr (Movies), Prowlarr (indexer manager), Lidarr (music), Readarr (books), Bazarr (subtitles), qBittorrent, SABnzbd, and Jellyfin for playback.

## 🚀 Services

- **sonarr**: TV show PVR
- **radarr**: Movie PVR
- **prowlarr**: Indexer manager
- **lidarr**: Music PVR
- **readarr**: Book/ebook PVR
- **bazarr**: Subtitle manager
- **qbittorrent**: Torrent client
- **sabnzbd**: Usenet client
- **jellyfin**: Media server

## 📦 Installation

### Using curl
```shell
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/arrstack/main/docker-compose.yaml" | docker compose -f - up -d
```

### Using git
```shell
git clone "https://github.com/composemgr/arrstack" ~/.local/srv/docker/arrstack
cd ~/.local/srv/docker/arrstack
docker compose up -d
```

### Using composemgr
```shell
composemgr install arrstack
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
SERVICE_USER=1000
SERVICE_GROUP=1000
```

## 🌐 Access

- **Sonarr**: http://172.17.0.1:8989
- **Radarr**: http://172.17.0.1:7878
- **Prowlarr**: http://172.17.0.1:9696
- **Lidarr**: http://172.17.0.1:8686
- **Readarr**: http://172.17.0.1:8787
- **Bazarr**: http://172.17.0.1:6767
- **qBittorrent**: http://172.17.0.1:8080
- **SABnzbd**: http://172.17.0.1:8081
- **Jellyfin**: http://172.17.0.1:8096

## 📂 Volumes

- `./rootfs/config/*` - Each service's configuration
- `./rootfs/data/downloads` - Download directory
- `./rootfs/data/media/tv` - TV shows
- `./rootfs/data/media/movies` - Movies
- `./rootfs/data/media/music` - Music
- `./rootfs/data/media/books` - Books

## 🔐 Security

- Configure authentication in each service
- Use VPN for torrent traffic (not included)
- Set appropriate file permissions

## 🔍 Logging

```shell
docker compose logs -f
```

## 🛠️ Management

```shell
docker compose up -d
docker compose down
docker compose pull && docker compose up -d
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+
- Significant disk space for media

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
