## 👋 Welcome to nexterm 🚀

Self-hosted server management and terminal access

## 📋 Description

Nexterm is a self-hosted server management platform. It keeps an inventory of
your machines, stores their connection credentials encrypted at rest, and gives
you a browser-based terminal and file browser for each one.

## 🚀 Services

- **app**: germannewsmaker/nexterm:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/nexterm/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/nexterm" ~/.local/srv/docker/nexterm
cd ~/.local/srv/docker/nexterm
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install nexterm
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
APP_ORG_NAME=Nexterm
APP_ADMIN_USER=administrator
APP_ADMIN_PASS=replace-with-a-random-password
ENCRYPTION_KEY=replace-with-a-random-encryption-key
```

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

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64270` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64270

Create the first admin account on first visit.

## 📂 Volumes

- `./volumes/data/nexterm` - Nexterm database and application data

## 🔐 Security

- Change all default passwords before deploying to production
- `ENCRYPTION_KEY` protects the stored server credentials. Set it before first
  start and keep it backed up; changing it later makes existing credentials
  unreadable.
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy) so the terminal
  and credentials are not sent in the clear
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
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
