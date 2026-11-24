3D Viewer is tested on these NAS systems, and runs on any Linux server or PC with Docker (amd64 or arm64).

| NAS | Operating system | Install with | Where your files are |
|---|---|---|---|
| **UGREEN** (DXP series) | UGOS Pro | Docker app or Dockhand (Compose project) | `/volume1`, `/volume2`, …; USB drives in `/mnt/@usb`; remote folders in `/mnt/@remote` |
| **Synology** | DSM 7.2 or later | Container Manager → **Project** | `/volume1`, `/volume2`, …; USB drives in `/volumeUSB1/usbshare` |
| **QNAP** | QTS 5 / QuTS hero | Container Station → **Applications** | `/share/<shared folder>` |

GPU thumbnail rendering works on models with an Intel CPU (they provide `/dev/dri`). Other models render on the CPU. See [GPU rendering](GPU-Rendering).

## UGREEN

The [Compose file on the Installation page](Installation) is written for UGREEN: use it as it is.

- Keep the `/volume1`, `/volume2` lines that match your volumes.
- USB drives appear under `/mnt/@usb/<device>`, remote folders connected in the **Files** app under `/mnt/@remote/…`. The `rslave` volumes make drives and folders connected later show up without a restart.
- DXP models with an Intel CPU have `/dev/dri`: keep the `devices` lines for GPU rendering.

## Synology

- Keep the `/volume1`, `/volume2` lines that match your volumes.
- Remove the `/mnt/@usb` and `/mnt/@remote` lines (they are UGREEN paths), and take them out of `BROWSE_ROOTS`.
- For USB drives, add `- /volumeUSB1:/volumeUSB1:rslave` and add `/volumeUSB1` to `BROWSE_ROOTS`.
- If the container won't start because of `/dev/dri`, remove the `devices` lines: that model has no GPU device.

## QNAP

- Shared folders live under `/share`. Replace the volume lines with `- /share:/share:rslave` and set `BROWSE_ROOTS=/share`.
- Remove the `/mnt/@usb` and `/mnt/@remote` lines.
- USB drives also appear under `/share` (for example `/share/USBDisk1`).
- Put the data folder somewhere like `/share/Container/3dviewer/data`.

## Other Linux servers and PCs

- Mount each folder of models with the same path on both sides, for example `- /srv/models:/srv/models`, and add it to `BROWSE_ROOTS`.
- Without `BROWSE_ROOTS`, the Admin page may browse `/volume1`–`/volume4`, `/mnt`, `/media`, `/models` and `/data`, the ones that exist.
- `MODELS_DIR=/srv/models` adds that folder as the first library on the first start.

## Permissions

Set `PUID` and `PGID` to the user that owns your model folders. Over SSH, run `id <username>`:

```
uid=1026(myuser) gid=100(users) …   →   PUID=1026, PGID=100
```

- On Synology the first user is usually `1026:100`.
- On QNAP the admin user is `0:0`, and regular users start at `500:100`.

With the wrong user, browsing works but uploads, notes, moves and deletes fail with a permission error in the log.

To keep everyone from changing anything, even the admin, set `READ_ONLY=true`.
