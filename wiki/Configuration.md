Most settings are changed on the [Admin page](Admin-Page) and stored in `/app/data/config.json`. These environment variables are set in the Compose file.

| Variable | Default | What it does |
|---|---|---|
| `PORT` | `3000` | Port the server listens on inside the container. |
| `PUID` / `PGID` | `1000` / `1000` | User and group the app runs as, and the owner of the files it writes. They need write access to your libraries for uploads and notes. See [NAS setup](NAS-Setup#permissions). |
| `BROWSE_ROOTS` | `/volume1…4,/mnt,/media,/models,/data` (the ones that exist) | Folders the Admin page may browse when adding libraries. |
| `ADMIN_PASSWORD` | unset | Sets the admin password at start (also resets a forgotten one). |
| `ADMIN_RESET_2FA` | unset | `true` turns off the admin's two-factor sign-in at start, for a lost phone. Remove it again afterwards. |
| `SESSION_COOKIE_SECURE` | `false` | Set to `true` when serving over HTTPS. See [Reverse proxy and HTTPS](Reverse-Proxy-and-HTTPS). |
| `READ_ONLY` | `false` | `true` locks all changes (upload, delete, editing), even for the admin. |
| `MAX_UPLOAD_MB` | `1024` | Largest uploaded file in MB. See [Size limits](Size-Limits). |
| `MAX_UNZIP_MB` | `8192` | Largest unpacked archive in MB. |
| `MAX_RENDER_MB` | `1024` | Largest model in MB that gets a server thumbnail. |
| `RENDER_GPU` | `auto` | `auto`, `off` (CPU only) or `force`. See [GPU rendering](GPU-Rendering). |
| `DISABLE_SERVER_RENDER` | `false` | Turns off the server renderer completely; browsers render thumbnails instead. |
| `DISABLE_REMOTE_MOUNTS` | `false` | Turns off the root mount helper (no **Network shares** on the Admin page). |
| `AUTH_USER` / `AUTH_PASS` | unset | Optional HTTP basic authentication in front of the whole site. |
| `MODELS_DIR` | unset | A folder added as the first library on the first start. |
| `DATA_DIR` | `/app/data` | Settings (`config.json`), thumbnails and previews. |
| `CACHE_DIR` | `DATA_DIR` | Thumbnails and previews, to keep them on another disk. See [Thumbnails and previews](Thumbnails-and-Previews#keep-the-cache-on-another-disk). |

A limit set here wins over the Admin page and shows locked there.

## What is stored where

| Where | What |
| --- | --- |
| `/app/data/config.json` | Libraries, network shares, settings, accounts, the admin password (hashed), the supporter key |
| `/app/data/thumbs`, `/app/data/previews` | Thumbnails and compressed previews (or in `CACHE_DIR`) |
| `.3dviewer/` next to your models | Names, descriptions, series, licence and saved orientation of each model |
| `.3dviewer-trash/` in each library | Deleted files, until the trash is emptied |
| `cover.webp` in a folder | The folder's picture |

Example of a model's metadata:

```
Prints/
├── benchy.stl
└── .3dviewer/
    └── benchy.stl.json   { "title": "...", "description": "...", "group": "..." }
```
