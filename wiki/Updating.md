Every version is listed on the [Releases](https://github.com/VincentFlagg/3DViewer/releases) page with what changed, and in the [CHANGELOG](https://github.com/VincentFlagg/3DViewer/blob/main/CHANGELOG.md).

## Update

- **Dockhand, Container Manager or Container Station**: pull the new image and redeploy the project.
- **Command line**: `docker compose pull && docker compose up -d`.

Then hard-refresh the browser: **Ctrl+Shift+R**, or **Cmd+Shift+R** on a Mac.

Your libraries, settings, accounts, notes and thumbnails are kept: they are in the data folder and next to your models.

## Stay on one version

`:latest` always has the newest version. To stay on one version, use its number instead:

```yaml
    image: ghcr.io/vincentflagg/3dviewer:1.0.0
```

## Security updates

The image is rebuilt every week, so security fixes for the operating system, Node and Chromium reach `:latest` even when 3D Viewer itself doesn't change. Pull it now and then even when there is no new release.

## Before a big update

Download a settings backup (**Admin → Backup**) first. See [Backups](Backups).
