# Changelog

All notable changes to 3D Viewer. Each version is also on the [Releases](https://github.com/VincentFlagg/3DViewer/releases) page and as a Docker tag: `ghcr.io/vincentflagg/3dviewer:<version>`.

## 3.1.0 (2026-10-23)

### New
- **Export** (viewer → Tools): download the model as STL, 3MF or OBJ, standing on the bed as shown, scaled by % or to a height in mm. **Repair** closes holes, turns flipped faces and removes empty or doubled faces. Admins can save the result as a copy next to the original.
- **Lay flat on a face** and **Auto-orient for printing** (viewer → Orientation): click the face to print on, or let it find the position with the fewest supports.
- **View in AR** on phones and tablets: the model at its real size on your table (AR Quick Look on iPhone and iPad, Scene Viewer on Android).
- **Share links**: a link to a model or a folder for 1, 7 or 30 days or until removed. Anyone with it can view and download only that, also on a private server. Listed and removable in the dialog and in Admin → Share links.
- **Import from link**: paste a Printables, Thingiverse or MakerWorld page, or a link to a file, and it is downloaded into the open folder with its pictures and description. Thingiverse needs an app token (Admin → Import from link).
- **Compare**: **Compare with…** in the viewer picks the second model from the folder or by search, and **Overlay** shows the two models on top of each other in two colours.

## 3.0.2 (2026-10-18)

### Changed
- **Search:** a matching folder shows its folder picture, or without one a 2×2 collage of the models in it (its own models first, then those in its sub-folders), instead of a plain folder icon.

## 3.0.1 (2026-10-17)

### Changed
- **Search** looks through the open folder and all its sub-folders (the whole library at the top level), not only the folder you are in. It matches file names, folder names, display names, descriptions, series names and your own tags. Results show as one list with the folder each model is in, matching folders first; a click opens the model in its folder.

## 3.0.0 (2026-10-13)

### New
- **Wall thickness**: the whole model coloured by wall thickness (red below a thickness you choose, 0.8 mm by default, then orange, yellow, green and blue), with the thinnest spots labelled. Runs in the background with progress.
- **Overhangs**: faces that will need supports shown in red, with an adjustable overhang angle and how much of the surface needs supports.
- **Mesh check**: open edges, non-manifold edges and flipped faces, highlighted and counted, with the number of separate parts.
- **Weight & cost**: volume, plastic used, weight, filament length and cost for PLA, PETG, ABS, ASA, TPU, Nylon, PC, PLA-CF and resin, with infill, wall count and 1.75 / 2.85 mm filament. Prices per kg and the currency are set in **Admin → Print cost**; each person can override a price.
- **Measure**: **Circle** through three points (radius, diameter, centre) and **Angle** (three points), next to **Distance**, which now shows ΔX, ΔY and ΔZ.
- **Cross-section**: type the exact cut height (or distance from the left side or front); the cut face is hatched.

### Fixed
- The cross-section's red cut face was hidden behind the model's own inside faces; it shows again.

## 2.1.7 (2026-10-12)

### New
- **Folder picture: Fill or Fit whole picture.** Fill (the default) crops the picture to the 4:3 card with the frame, as before. **Fit whole picture** keeps the whole picture, shrunk to fit the card, and fills the empty sides with **Black** or **White** borders. The switch is in the dialog and in the full-size preview, and the previews show the card exactly as it will be saved. GIFs keep Fill, as they are saved as they are.

## 2.1.6 (2026-10-12)

### New
- **Folder picture** full-size preview: **Fit to screen** and **Actual size**. Fit to screen (the default) enlarges small pictures and model thumbnails and shrinks big ones so the whole picture fills the screen. Actual size shows it at 100 %, starting at the frame; scroll, or drag beside the frame, to look around. The choice stays while you step through the pictures.

## 2.1.5 (2026-10-12)

### New
- **Folder picture** full-size preview: **arrows** (and the ← → keys, or a swipe on phones) step through the folder's pictures and model thumbnails.
- The **4:3 frame** can be edited: drag it to choose the part that is saved, drag its corners to make it bigger or smaller (it stays 4:3). **Reset frame** centres it again. Each picture keeps its frame while you step through them, and the small preview shows it. GIFs keep a fixed frame, as they are saved as they are.

## 2.1.4 (2026-10-12)

### New
- **Folder picture** full-size preview: **View full size**, or a click on the preview, shows the whole picture with a frame on the 4:3 part the folder card keeps. **X**, Esc or a click beside the picture closes it; **Use this picture** saves it from there.

## 2.1.3 (2026-10-12)

### Changed
- **Folder picture** previews your choice before saving it. Clicking a picture or model thumbnail, or uploading a picture, shows it in the dialog cropped to 4:3 as the folder card will show it; **Use this picture** saves it, **Cancel** (or Esc) goes back.

## 2.1.2 (2026-10-12)

### Fixed
- Dockhand's release-notes icon opened the releases of a private repository. The image now carries Dockhand's `dockhand.changelog.url` label, so the icon opens the [3D Viewer releases](https://github.com/VincentFlagg/3DViewer/releases).

## 2.1.1 (2026-10-12)

### Fixed
- Unpacking an archive whose name ends in a dot before the extension (for example `Iron Giant..7z`) failed on network shares with "ENOTDIR: not a directory". Names of new folders and files no longer end in a dot or a space, which Windows and SMB shares cannot store: the folder is now called `Iron Giant`.

## 2.1.0 (2026-10-12)

### New
- **RAR, 7z, TAR and compressed files** are unpacked like zips: on upload, with **Unpack** on their card, from the selection bar and with **Admin → Libraries → Unpack archives**. RAR4/RAR5, split RAR and 7z archives, `.tar`, `.tar.gz`, `.tar.xz`, `.tar.bz2`, and single files like `model.stl.gz`.
- **Archives with a password** (RAR, 7z and zip): **Unpack** asks for the password. It is not kept.

### Changed
- Admin → Limits: **Largest unpacked archive** (was "Largest unpacked .zip"), for every kind of archive.

## 2.0.1 (2026-10-11)

### New
- **Snapping for Measure**: points snap to corners, borders, the middle of a border, the centre of a flat face, the centre of the model or of its base, or nowhere. **Auto** (the default) picks a corner, the middle of a border or a border, whichever is close. A ring shows where a click will land.
- **Open in Creality Print** (version 6 or later).

## 2.0.0 (2026-10-11)

### New
- **Accounts**: the admin adds accounts on the Admin page; people sign in on the main page (person button at the top). Accounts can look and download; only the admin changes the library. Each account can change its own password.
- **Private server**: Admin → Accounts → Private shows the libraries only to signed-in accounts and the admin.
- **Favourites, tags and a print log** for each account (and the admin): ☆ Favourite and tags under **Mine** in the viewer, and **+ Add a print** with date, filament, notes and a photo. The sidebar lists My favourites, My prints and each tag across all libraries; **Show** filters a folder by them.
- **Recently added**: the newest models of all libraries, in the sidebar.
- **Compare**: select two models and click **Compare** to see them side by side at the same scale.
- **Print bed**: a printer's build volume around the model (many Bambu Lab, Prusa, Creality, Elegoo, Anycubic, Voron and resin printers, or a custom size), and whether the model fits.
- **New formats**: STEP and IGES (CAD, with their colours), 3DS, COLLADA (.dae) and USD (.usdz, .usd, .usda, .usdc). STEP files can also be opened in the slicer.
- **Scan schedule** (Admin → Thumbnails): look through the libraries for new files every 1, 3, 6 or 12 hours, or once a day at a set time.
- **Duplicates** (Admin): finds models stored more than once, in any folder or library, and sends the extra copies to the trash.
- **Backup** (Admin): one file with all settings, accounts and their marks, and restore from it.

## 1.8.6 (2026-10-11)

### New
- **Measure** in the viewer: click two points on the model for the distance between them (and its width, depth and height parts).
- **Cross-section** in the viewer: cut through the model across its height, width or depth with a slider; the cut face shows in red.
- **Screenshot** of the viewer: WebP (smallest file, the default), JPG or PNG.
- **Open in slicer**: opens STL, 3MF, OBJ and PLY files in Bambu Studio, OrcaSlicer, PrusaSlicer or UltiMaker Cura.
- **Sort by** name, date, size or type, and **Show** folders only, models only, models without a thumbnail or one file type.
- **Admin → Storage**: space used by thumbnails, previews and the trash, and the free space of the cache, the data folder and each library, with a warning when one is almost full.

### Fixed
- A cache folder (`CACHE_DIR`) that runs out of space or quota ("Unknown system error -122") no longer fills the log with one line per file or stops thumbnails. Moving stops at the first file that does not fit, and the files left behind are still used from the data folder. While the cache is full, new thumbnails go to the data folder and previews are skipped, and a thumbnail is saved even when its preview cannot be. The start-up checklist shows the cache's free space.

## 1.8.5 (2026-10-07)

### New
- **Blender files in 3D**: `.blend` files are now shown as models, with a thumbnail. 3D Viewer reads the meshes stored in the file (Blender 2.8 to 4.x, also compressed): the objects of the scene with their material colours or packed base colour textures, copies made by particle systems (trees, grass) and instanced collections. A colour ramp in a material (leaves by season) gives each copy its own colour. Modifiers, geometry nodes, curves and text are not shown; a file without a mesh shows the preview picture Blender saved in it.

### Changed
- Blender files are no longer listed with ZBrush and 123D Catch files: the Admin switch is back to **Show ZBrush and 123D Catch files**.

## 1.8.0 (2026-10-07)

### New
- **Blender files (.blend)** are listed in the gallery with the preview picture Blender saves inside them (also from compressed files), or a Blender icon when there is none. Download, select, move and delete them like models; there is no 3D view. The Admin switch is now **Show ZBrush, 123D Catch and Blender files**.

## 1.7.2 (2026-10-06)

### Changed
- The folder title, its tools (Select, Picture, Rename, Add info, card size, Grid/List) and the upload/unzip progress bar stay pinned under the top bar while you scroll.

## 1.7.1 (2026-10-06)

### New
- **Thumbnails with the sun**: **Use this view** with the sun lamp on saves its direction and shadows too, and the thumbnail is rendered with them. **Front view** goes back to the front with even light.

### Fixed
- A thumbnail that was being rendered while its orientation or view was saved could be kept with the old setting. It is now rendered again.

## 1.7.0 (2026-10-06)

### New
- **Sun lamp** in the viewer (**Light → Sun lamp**): one strong light with shadows on the model and the floor. **Front**, **Left**, **Right**, **Back**, **Top**, or any direction with **Around** and **Height**. Remembered in your browser.
- **Use this view** (admin): turn the view to any angle and use it for the model's thumbnail; the model also opens from it. **Front view** goes back.
- **Unpack several zips**: select zips and click **Unpack** in the selection bar; they are unpacked one after another.

### Fixed
- **One zip at a time**: clicking **Unpack** twice (or two admins at once) could unpack the same zip twice. Now only one zip is unpacked at a time; the others wait.
- The tick box of a selected card was hidden behind its picture.

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
