3D Viewer runs as one Docker container. The image `ghcr.io/vincentflagg/3dviewer:latest` runs on **amd64** and **arm64**: UGREEN, Synology and QNAP NAS, and any Linux server or PC with Docker.

## 1. The Compose file

Download [docker-compose.yml](https://github.com/VincentFlagg/3DViewer/blob/main/docker-compose.yml), or copy it from here:

```yaml
services:
  3dviewer:
    image: ghcr.io/vincentflagg/3dviewer:latest
    container_name: 3DViewer
    ports:
      - "8733:3000"
    environment:
      - PORT=3000
      - PUID=${PUID:-1000}
      - PGID=${PGID:-1000}
      - BROWSE_ROOTS=${BROWSE_ROOTS:-/volume1,/volume2,/volume3,/volume4,/mnt/@usb,/mnt/@remote}
      - ADMIN_PASSWORD=${ADMIN_PASSWORD:-}
      - SESSION_COOKIE_SECURE=${SESSION_COOKIE_SECURE:-false}
      - READ_ONLY=${READ_ONLY:-false}
    cap_add:
      - SYS_ADMIN
      - DAC_READ_SEARCH
    security_opt:
      - apparmor:unconfined
    devices:
      - /dev/dri:/dev/dri
    volumes:
      - /volume2/docker/3dviewer/data:/app/data
      - /volume1:/volume1
      - /volume2:/volume2
      - /mnt/@usb:/mnt/@usb:rslave
      - /mnt/@remote:/mnt/@remote:rslave
    healthcheck:
      test: ["CMD", "node", "/app/healthcheck.js"]
      interval: 30s
      timeout: 10s
      start_period: 60s
      retries: 3
    restart: unless-stopped
```

What each part does:

| Part | Why |
| --- | --- |
| `ports: 8733:3000` | 3D Viewer opens at `http://<nas-ip>:8733`. Change `8733` if that port is taken. |
| `PUID` / `PGID` | The user the app runs as. It needs write access to your model folders for uploads, notes and moves. See [NAS setup](NAS-Setup#permissions). |
| `BROWSE_ROOTS` | The folders the Admin page may browse when you add a library. |
| `/app/data` volume | Settings, accounts, thumbnails and previews. **Must be a folder on your NAS**, or everything is lost when the container is recreated. |
| `/volume1`, `/volume2` … | Your model folders, with the same path inside and outside the container. |
| `cap_add`, `security_opt` | Only needed to [connect network shares from inside 3D Viewer](Network-Shares-and-USB-Drives#connect-shares-in-3d-viewer). Remove them if you don't. |
| `devices: /dev/dri` | The Intel GPU, for [faster thumbnails](GPU-Rendering). Remove it if your NAS has none. |
| `/mnt/@usb`, `/mnt/@remote` | UGREEN's USB drives and remote folders. Remove them on other NAS. |

## 2. Deploy

Create a new Compose project and paste the file:

- **UGREEN**: Dockhand, or the **Docker** app → Project.
- **Synology**: **Container Manager → Project**.
- **QNAP**: **Container Station → Applications**.
- **Any Linux**: save it as `docker-compose.yml` and run `docker compose up -d`.

Change the `/app/data` volume to a folder that exists on your NAS (for example `/volume1/docker/3dviewer/data`, or `/share/Container/3dviewer/data` on QNAP), and follow the [notes for your NAS](NAS-Setup) before you deploy.

## 3. First start

1. Open `http://<nas-ip>:8733/admin` and create the admin password. (Or set `ADMIN_PASSWORD` in the environment; that also resets a forgotten password.)
2. Click **Add library**, browse or search for the folder that holds your models, and click **Use this folder**. Repeat for each share or drive.
3. Open `http://<nas-ip>:8733` to browse. Thumbnails appear as the server renders them; the Admin page shows the progress.

The container log shows a start-up checklist (web server, data folder, libraries, renderer, limits…). If something is wrong, it is usually named there: see [Troubleshooting](Troubleshooting).

## Next steps

- [Add accounts](Accounts-and-Sign-in) or make the server private.
- [Put it behind a reverse proxy with HTTPS](Reverse-Proxy-and-HTTPS) to open it from outside your home.
- [Install it as an app](Install-as-an-App) on your phone or computer.
- Turn on [automatic backups](Backups) of the settings.
