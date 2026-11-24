A library can be any folder the container can see: a share on another NAS or computer, or a USB drive. There are two ways to use a network share.

## Shares connected on the NAS (UGREEN)

1. Connect the share in UGOS first: add it as a remote folder in the **Files** app (SMB, NFS or WebDAV). UGOS mounts remote folders under `/mnt/@remote/…`.
2. The `/mnt/@remote:/mnt/@remote:rslave` volume passes every remote folder into the container, including ones connected later.
3. On the Admin page, click **Add library** and search or browse for it. Remote folders show with a readable name such as **SMB · 192.168.0.74**.

If the other NAS is offline, its library shows **Folder not found** until it is back.

## Connect shares in 3D Viewer

**Admin → Network shares → Add share**:

- Enter the SMB (Windows or NAS share) or NFS details: host or IP, share name or export path, and a user name and password (SMB). You can also choose a protocol version and read-only.
- The app mounts the share and can add it as a library in one step.
- Shares reconnect when the container starts and are retried every 5 minutes, for example if the other NAS was still booting.
- The Admin page shows the status (**Connected**, or **Not connected** with the reason), with **Connect**, **Disconnect**, **Edit** and **Remove**.

### What it needs

The container starts a small root helper that only mounts and unmounts shares; the web app itself runs as `PUID:PGID`. This needs, in the Compose file:

```yaml
    cap_add:
      - SYS_ADMIN
      - DAC_READ_SEARCH
    security_opt:
      - apparmor:unconfined
```

`SYS_ADMIN` is a broad privilege. If you only use shares connected on the NAS, remove the `cap_add` and `security_opt` lines, or set `DISABLE_REMOTE_MOUNTS=true`.

Passwords are stored in `/app/data/config.json`, readable only by the app user. When a share is mounted they go through a temporary credentials file, never on the command line.

## USB and external drives

| NAS | Where drives appear | Volume to add |
| --- | --- | --- |
| UGREEN | `/mnt/@usb/<device>` (for example `/mnt/@usb/sdc1`) | `- /mnt/@usb:/mnt/@usb:rslave` (already in the Compose file) |
| Synology | `/volumeUSB1/usbshare` | `- /volumeUSB1:/volumeUSB1:rslave`, and add `/volumeUSB1` to `BROWSE_ROOTS` |
| QNAP | `/share/USBDisk1` … | covered by `- /share:/share:rslave` |

- To check the path, SSH into the NAS and run `ls /mnt/@usb` (UGREEN).
- Thanks to `rslave`, drives plugged in later show up without restarting the container. Add the drive's folder as a library on the Admin page.
- A library on an unplugged drive shows **Folder not found** until the drive is back.

## Any other folder

Add a volume with the same path on both sides, for example `- /volume3:/volume3`, and make sure the path is in `BROWSE_ROOTS`. `/volume1`–`/volume4` are already listed, and volumes that aren't mounted are ignored.
