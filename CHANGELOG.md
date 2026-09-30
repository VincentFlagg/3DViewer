# Changelog

All notable changes to 3D Viewer. Each version is also on the [Releases](https://github.com/VincentFlagg/3DViewer/releases) page and as a Docker tag: `ghcr.io/vincentflagg/3dviewer:<version>`.

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
