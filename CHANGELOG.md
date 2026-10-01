# Changelog

All notable changes to 3D Viewer. Each version is also on the [Releases](https://github.com/VincentFlagg/3DViewer/releases) page and as a Docker tag: `ghcr.io/vincentflagg/3dviewer:<version>`.

## 1.3.0 (2026-10-01)

### New
- **Thumbnails and previews on another disk**: set `CACHE_DIR` and add a volume for it in `docker-compose.yml`. At the next start the existing thumbnails and previews are moved there, so nothing is rendered again. The Admin page shows where they are stored, and the start-up checklist warns when the folder is not on a volume.

### Fixed
- **Lychee scenes saved by older Lychee versions** (3.5.1 and before) no longer fail with "byte length of Uint32Array should be a multiple of 4". Their models open turned and placed as in Lychee, with their supports.

## 1.2.0 (2026-10-01)

### New
- **Size limits on the Admin page** (Admin → Limits): the largest file to upload, the largest unpacked .zip and the largest model to make a thumbnail for, in MB with the size in GB next to it. Changes apply at once, without a restart.
- `MAX_UPLOAD_MB`, `MAX_UNZIP_MB` and `MAX_RENDER_MB` in docker-compose still work and win over the Admin page, where they show locked.
- The startup log lists the limits in use; the README explains them under *Size limits*.

## 1.1.1 (2026-10-01)

### New
- **Lychee Slicer scenes (`.lys`)**: supported resin prints open with all their models placed as in Lychee, and their supports rebuilt as light-grey struts, pads and braces. A **Supports** button in the viewer hides them; thumbnails show the supported scene.
- Scenes whose models are not saved in the file (Lychee's own sample models) show Lychee's preview picture, as the thumbnail and in the viewer, with a note.
- The README shows a library overview with folder pictures.

## 1.1.0 (2026-09-30)

### New
- **Upload folders**: drag folders onto the page, or use **Upload → Upload a folder…**. The folder structure is kept. Big uploads are sent in parts with one progress bar.
- **Thumbnails rendered at the same time**: Admin → Thumbnails & previews, 1 to 4. More helps with a GPU, many CPU cores or libraries on network shares.
- **Folder pictures are resized** to the size a folder card uses: cropped to 4:3 and scaled down to 800 × 600 (saved as `cover.webp`).
- **App log**: a logo and a checklist of every service at each start, then one dated line per event (uploads, moves, deletes, library and settings changes, sign-ins, thumbnails, errors with their reason). See *Logs and troubleshooting* in the README.
- **Buy Me a Coffee**: a second way to donate, on the splash, next to the corner reminder and in Admin. Write "3D Viewer" in the coffee message to get a supporter key by email.
- **Textured OBJ models**: textures from the `.mtl` file now show in thumbnails, previews and the viewer.

### Changed
- The daily splash shows for 10 seconds, and a small supporter reminder stays in the bottom-right corner until a key is activated.
- Node 24 LTS base image, rebuilt every week with the latest security fixes.

### Fixed
- Dropping a folder failed with "Upload failed (network error)".
- Uploads that took longer than 5 minutes were cut off.
- A texture picture of an OBJ model was used as its cover, and textured models could show black.

## 1.0.0 (2026-09-28)

First public release.
