Three limits protect a small NAS from files that are too big to handle. Change them in **Admin → Thumbnails → Limits** (no restart needed), or set them in the Compose file. A value set in the Compose file wins and shows locked on the Admin page. Sizes are in MB: 1024 MB = 1 GB.

| Admin page | Variable | Default | What it limits |
|---|---|---|---|
| Largest file to upload | `MAX_UPLOAD_MB` | `1024` (1 GB) | One uploaded file. Folders are sent in parts, so their total size has no limit. |
| Largest unpacked archive | `MAX_UNZIP_MB` | `8192` (8 GB) | Everything inside one archive (.zip, .rar, .7z, .tar.gz…) together. A bigger archive is kept as it is, not unpacked. |
| Largest model to make a thumbnail for | `MAX_RENDER_MB` | `1024` (1 GB) | Bigger models still open in the viewer, but get no server thumbnail. |

The defaults fit almost every model: a 120 MB model uploads and gets a thumbnail without changing anything.

**Memory**: making a thumbnail needs roughly 3 to 5 times the file size in memory. On a NAS with 4 GB of RAM, keep the thumbnail limit at 1024 MB or less.

The container log lists the limits in use at every start.

- **Downloads** have no size limit: selections are streamed as one .zip, so multi-GB downloads work without filling the server's memory.
- **Imports from a link** use the upload limit for each file.
- A **reverse proxy** can have its own upload limit. See [Reverse proxy and HTTPS](Reverse-Proxy-and-HTTPS).
