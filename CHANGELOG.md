# Changelog

All notable changes to 3D Viewer. Each version is also on the [Releases](https://github.com/VincentFlagg/3DViewer/releases) page and as a Docker tag: `ghcr.io/vincentflagg/3dviewer:<version>`.

## 1.6.0 (2026-10-03)

### New
- **Rename folders** (admin): the pencil button on a folder card, or **Rename** above the grid for the current folder. Models inside keep their notes, orientation, thumbnails and previews.
- **New folder in Move to…**: create a folder where you are in the picker (in any library) and move into it in one go.
- **Folder cards show what they hold**, sub-folders included: for example **12 folders · 10 models · 35 files**. The counts are worked out in the background and remembered, so big libraries still open fast.

## 1.5.0 (2026-10-01)

### New
- **Unpack zips already in a library**: a zip with 3D models inside shows as a card with **Unpack** (admin). It is unpacked like an uploaded zip, into a new folder named after it, and the zip goes to the trash. **Admin → Libraries → Unpack zips** unpacks every zip with models in a library, sub-folders included. Zips without models are left alone and not shown.
- **123D Catch projects (.3dp)** are listed like ZBrush files, with a 123D Catch icon (download, move, delete; no 3D preview). The Admin switch is now **Show ZBrush and 123D Catch files**.
- **Folders can be selected**: folder cards have a tick box in select mode, and **Select all** includes them. **Download** zips a whole folder with everything in it (no size limit); **Move to…** and **Delete** (to the trash) work on folders too.

## 1.4.4 (2026-10-01)

### New
- **Admin → Viewer defaults → Show ZBrush files (.ztl, .zpr) in the gallery**: on by default; untick it to hide them.

## 1.4.3 (2026-10-01)

### New
- **ZBrush files (.ztl, .zpr)** are listed in the gallery with a ZBrush icon (no 3D preview: the format is not published). Click to download; select, move and delete them like models.

## 1.4.2 (2026-10-01)

### Changed
- **Labelled dimensions** in the viewer panel: W (width, left to right) × D (depth, front to back) × H (height, bottom to top), as the model stands in the viewer. The height is always the last number, also with Z-up turned off.

## 1.4.1 (2026-10-01)

### Changed
- **G-code looks like the print**: toolpaths are drawn as solid, shaded strands with the width and height of each printed line, instead of thin lines whose colours blended together. Thumbnails of G-code without a saved picture use the same look.
- New in the viewer panel for G-code: **Solid** / **Lines** (very large files open as lines), **By feature** / **One colour**, and a tick box per feature to hide it (all shown when a file opens). Solid/Lines and the colour choice are remembered in the browser.

## 1.4.0 (2026-10-01)

### New
- **Select several models**: **Select** above the grid (or Ctrl/Cmd+click a card), click to pick, Shift+click for a range, **Select all**. A bar at the bottom shows the count and size.
- **Download several files as one .zip** (for everyone). OBJ and GLTF models bring their `.mtl`, textures and `.bin` files. The zip is streamed, so big selections work. One plain file downloads as it is.
- **Move between libraries**: drag onto another library in the sidebar (listed while dragging), or use **Move to…** (folder cards, viewer, selection bar) with a library and folder picker. Moves to another disk or share are copied, then deleted, with a progress bar. Notes, orientation and thumbnails go along. You are asked before replacing a file with the same name.
- **Trash**: deleted files and folders (folders with everything in them, too) go to a hidden `.3dviewer-trash` folder in their library. **Admin → Trash** restores them where they were or deletes them for good. Items are kept 30 days by default (Admin setting; 0 = until emptied).
- **G-code (.gcode) and Prusa binary G-code (.bgcode)**: toolpaths coloured by feature with a legend, a layer slider, travel moves on request, and print time, filament, layer height and slicer in the panel. Thumbnails use the preview picture saved by the slicer.

### Changed
- Deleting a non-empty folder is now possible (it goes to the trash). Deleting asks for confirmation and says how long the item can be restored.

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
