## 👋 Welcome to arrstack 🚀

Complete *arr media automation stack (Sonarr, Radarr, Prowlarr, etc)

## 📋 Description

Complete *arr media automation stack (Sonarr, Radarr, Prowlarr, etc)

The stack bundles the whole download-and-import pipeline: indexers
(Prowlarr, Jackett), automation apps (Sonarr, Radarr, Lidarr, Readarr,
Whisparr), supporting services (Bazarr, Unpackerr, Overseerr), a BitTorrent
client (Transmission), a downloader (MeTube), a media server
(Audiobookshelf), and a dashboard (Homarr).

The default compose file runs an nginx `proxy` service that publishes the
whole stack on the single reserved external port `64113`. Each web UI is
served at `/{service}`: the proxy strips that prefix, so the service itself
only ever sees `/`. Homarr is the dashboard at `/`. Pages are rewritten so
their links stay under the prefix, and a `svc` cookie routes the requests a
page's JavaScript makes to the root.

Transmission's BitTorrent peer port `51413` (tcp and udp) is published on all
host interfaces, because peers cannot be proxied over HTTP.

## 🚀 Services

| Service | Image | Native port | Default URL |
|---------|-------|-------------|-------------|
| proxy | nginx:latest | 80 | `http://172.17.0.1:64113` |
| homarr | ghcr.io/homarr-labs/homarr:latest | 7575 | `/` |
| sonarr | ghcr.io/hotio/sonarr:latest | 8989 | `/sonarr/` |
| radarr | ghcr.io/hotio/radarr:latest | 7878 | `/radarr/` |
| lidarr | ghcr.io/hotio/lidarr:latest | 8686 | `/lidarr/` |
| readarr | linuxserver/readarr:0.4.19-nightly | 8787 | `/readarr/` |
| prowlarr | ghcr.io/hotio/prowlarr:latest | 9696 | `/prowlarr/` |
| whisparr | ghcr.io/hotio/whisparr:latest | 6969 | `/whisparr/` |
| bazarr | ghcr.io/hotio/bazarr:latest | 6767 | `/bazarr/` |
| jackett | ghcr.io/hotio/jackett:latest | 9117 | `/jackett/` |
| overseerr | linuxserver/overseerr:latest | 5055 | `/overseerr/` |
| transmission | linuxserver/transmission:latest | 9091 | `/transmission/` |
| metube | alexta69/metube:latest | 8081 | `/metube/` |
| audiobookshelf | ghcr.io/advplyr/audiobookshelf:latest | 80 | `/audiobookshelf/` |
| unpackerr | ghcr.io/hotio/unpackerr:latest | none | no web UI |

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/arrstack/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/arrstack" ~/.local/srv/docker/arrstack
cd ~/.local/srv/docker/arrstack
cp default.env .env
docker compose --env-file .env up -d
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
APP_ADMIN_USER=admin
APP_ADMIN_PASS=replace-with-a-random-password
APP_SECRET_TOKEN_64=replace-with-a-random-64-character-hex-string
```

Homarr refuses to start without a 64-character hex `SECRET_ENCRYPTION_KEY`.
The compose file maps it from `APP_SECRET_TOKEN_64`, which `default.env`
generates; set your own value before exposing the stack.

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

Transmission is the only service that reads credentials directly: its web UI
uses `USER` and `PASS`. Every other service authenticates on first run, so
change each default password before exposing it.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, nginx proxy published on `172.17.0.1:64113` |
| `docker-compose.traefik.yaml` | All services behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | All services behind an existing external `cloudflare` tunnel network |

The proxy variants publish no web ports and do not use the nginx proxy. Their
only published ports are Transmission's BitTorrent peer port `51413` (tcp and
udp) on all host interfaces, since peers cannot be proxied over HTTP. Each
service gets its own hostname, formed as `<service>.${BASE_DOMAIN_NAME}`, for
example `sonarr.example.com` and `radarr.example.com`. In every compose file
the container hostname is just the service name (`sonarr`, `radarr`,
`homarr`, `transmission`, and so on).

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Dashboard (Homarr)**: http://172.17.0.1:64113/
- **Sonarr**: http://172.17.0.1:64113/sonarr/
- **Other services**: `/{service}/` on the same address, see the table above
- **BitTorrent peers**: port `51413` (tcp and udp) on all host interfaces

Only the single port `64113` is published for the web UIs. Put your host
reverse proxy in front of it and forward every path unchanged.

The `svc` cookie is per browser. Opening two different services in two tabs
can send one tab's root-level requests to the other service; use one service
at a time per browser profile.

## 📂 Volumes

- `./volumes/config/sonarr` - Sonarr configuration
- `./volumes/config/radarr` - Radarr configuration
- `./volumes/config/lidarr` - Lidarr configuration
- `./volumes/config/readarr` - Readarr configuration
- `./volumes/config/prowlarr` - Prowlarr configuration
- `./volumes/config/whisparr` - Whisparr configuration
- `./volumes/config/bazarr` - Bazarr configuration
- `./volumes/config/jackett` - Jackett configuration
- `./volumes/config/unpackerr` - Unpackerr configuration
- `./volumes/config/overseerr` - Overseerr configuration
- `./volumes/config/transmission` - Transmission configuration
- `./volumes/config/metube` - MeTube configuration
- `./volumes/config/audiobookshelf` - Audiobookshelf configuration
- `./volumes/config/homarr` - Homarr configuration
- `./volumes/data/tv` - TV library
- `./volumes/data/movies` - Movie library
- `./volumes/data/music` - Music library
- `./volumes/data/books` - Book library
- `./volumes/data/usenet` - Usenet downloads
- `./volumes/data/subtitles` - Subtitles
- `./volumes/data/downloads` - Download client staging area
- `./volumes/data/audiobooks` - Audiobook library
- `./volumes/data/podcasts` - Podcast library

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f sonarr
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
