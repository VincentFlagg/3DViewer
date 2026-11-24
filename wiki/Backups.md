## What a backup holds

**Admin → Backup → Download backup** gives one file with the settings of this 3D Viewer:

- libraries and network shares (with their passwords);
- all settings;
- the admin password;
- the accounts with their favourites, tags and print logs;
- the supporter key.

Your models, their notes and the thumbnails are **not** in it: back up your model folders with your NAS's own backup. Keep the backup file somewhere safe, since it contains passwords.

## Restore

**Admin → Backup → Restore from a backup…** and pick the file.

## Automatic backups

**Admin → Backup → Automatic backups**:

- **Save a backup automatically into a folder**, every **day** or every **week** (on Sunday), at the time you choose.
- **Keep the newest** 14 by default. Older backups in that folder are deleted; other files are left alone.
- **Choose folder…**: pick a folder on another disk or a network share, so a backup survives if the disk with 3D Viewer's data fails.
- **Back up now** makes one at once.

[Notifications](Notifications) can tell you when a scheduled backup fails.

## Moving to a new NAS

1. On the old NAS: **Admin → Backup → Download backup**.
2. Copy your model folders to the new NAS, keeping the same paths if you can (for example `/volume1/3D`).
3. [Install 3D Viewer](Installation) on the new NAS, with the same volumes.
4. Open `/admin`, set a password, and **Restore from a backup…**.
5. If a library's path changed, change its folder in **Admin → Library → Libraries**.

Thumbnails are made again in the background.

Names, descriptions, series and saved orientations travel with your models, in the `.3dviewer/` folders next to them.
