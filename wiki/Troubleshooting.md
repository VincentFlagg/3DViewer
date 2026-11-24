## Read the log first

Open the container's log: **Logs** in Dockhand, Container Manager or Container Station, or `docker logs 3DViewer`.

Each start (and automatic restart) prints the 3D Viewer logo and a checklist:

- web server;
- data folder, and cache folder when `CACHE_DIR` is set;
- each library;
- network shares;
- thumbnail renderer (GPU or CPU);
- upload limits;
- admin password and supporter license.

After that, there is one dated line per event: uploads (files, size, folder), unpacked archives, moves, deletes, new folders, library and settings changes, sign-ins, thumbnails made or failed, and every error with its reason.

When you [report a bug](https://github.com/VincentFlagg/3DViewer/issues/new?template=bug_report.yml), include the lines around the error, your 3D Viewer version and your NAS.

## The page is blank or broken after an update

The browser is mixing old and new files. Hard-refresh: **Ctrl+Shift+R**, or **Cmd+Shift+R** on a Mac. If you installed it as an app, close and reopen it. A private window shows whether the cache is the cause.

## The container won't start

- **An error about `/dev/dri`**: the NAS has no GPU device. Remove the `devices` lines from the Compose file.
- **An error about a volume path**: a folder on the left side of a volume doesn't exist on the NAS. Create it, or fix the path. The `/app/data` folder must exist.
- **It restarts over and over**: read the log for the reason. The health check marks the container unhealthy when the web server doesn't answer.

## "Upload failed: the connection … was lost"

The log says how far the upload got. Common causes:

- a reverse proxy with an upload size limit: in Nginx or Nginx Proxy Manager, set `client_max_body_size 0;`. See [Reverse proxy and HTTPS](Reverse-Proxy-and-HTTPS);
- the network dropping.

Files larger than the upload limit (**Admin → Thumbnails → Limits**) are skipped before uploading, with a message.

## Uploads, moves or deletes fail with a permission error

`PUID` and `PGID` don't own your model folders. Set them to the user that does: see [NAS setup → Permissions](NAS-Setup#permissions). Also check that editing isn't turned off (**Admin → Accounts → Access & editing**, or `READ_ONLY=true`).

## A library shows "Folder not found"

- A USB drive was unplugged, or a network share is offline: it comes back when the drive or share does.
- The folder isn't passed into the container: add a volume with the same path on both sides, and add it to `BROWSE_ROOTS`. See [Network shares and USB drives](Network-Shares-and-USB-Drives).

## The folder I want isn't in "Add library"

Its path isn't in `BROWSE_ROOTS`, or there is no volume for it. Add both, and redeploy.

## A network share says "Not connected"

The reason is shown next to it in **Admin → Library → Network shares**. Check the host, share name, user and password, and the protocol version. Shares are retried every 5 minutes. Connecting shares from 3D Viewer needs the `cap_add` and `security_opt` lines: see [Network shares and USB drives](Network-Shares-and-USB-Drives#what-it-needs).

## Thumbnails are missing or slow

- **Admin → Thumbnails** shows the queue and **Files that could not be rendered**.
- Models above the thumbnail limit (1 GB by default) get no thumbnail but still open. See [Size limits](Size-Limits).
- Files copied over SMB are found at the next look through the libraries (every 6 hours by default). **Render missing now** does it at once.
- On the CPU, rendering is slower: see [GPU rendering](GPU-Rendering).

## A model shows in the plain model colour

See [Colours, materials and textures](Colours-Materials-and-Textures#when-a-model-shows-up-in-the-plain-model-colour).

## A model lies on its side

Turn it in the viewer and **Save orientation**, or change which formats open Z-up in **Admin → Viewer → Viewer defaults**. See [Viewer → Orientation](Viewer#orientation).

## Signed out right after signing in

`SESSION_COOKIE_SECURE=true` while opening 3D Viewer over plain `http://`. Use the `https://` address, or set it to `false`.

## Forgot the admin password, or lost the phone for two-factor sign-in

- Password: set `ADMIN_PASSWORD` and restart. See [Accounts and sign-in](Accounts-and-Sign-in#forgot-the-admin-password).
- Admin two-factor: set `ADMIN_RESET_2FA=true`, restart, sign in, then remove it again. For an account: **Reset 2FA** in **Admin → Accounts**.

## "Open in slicer" or AR on Android doesn't work

The slicer and Google's Scene Viewer download the model from 3D Viewer themselves, so they must reach the server at the address in your browser. Scene Viewer may also need HTTPS.

## "Install app" is missing on Android or in Chrome

Chrome, Edge and Android only install apps from an `https://` address. See [Install as an app](Install-as-an-App).

## Still stuck?

Ask in [Discussions](https://github.com/VincentFlagg/3DViewer/discussions), or [report a bug](https://github.com/VincentFlagg/3DViewer/issues/new?template=bug_report.yml) with your version, your NAS and the log lines.
