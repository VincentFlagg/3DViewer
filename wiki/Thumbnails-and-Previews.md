## Thumbnails

The server renders a thumbnail of every model in the background, with a headless browser: on the [GPU](GPU-Rendering) when the container has one, on the CPU otherwise. New models get theirs right after they are uploaded or imported. Models copied in some other way (over SMB, for example) are found when the libraries are looked through.

Settings in **Admin → Thumbnails → Thumbnails & previews**:

| Setting | |
| --- | --- |
| **Render on the server** | On by default. Off: browsers render thumbnails as people browse. |
| **Thumbnails rendered at the same time** | 1 by default, up to 4. More helps with a GPU, a CPU with many cores, or libraries on network shares. Without a GPU, 1 or 2 is usually best. Each one uses up to about 1 GB of memory while it works. |
| **Look through the libraries for new files** | Every 6 hours by default; also every 1, 3 or 12 hours, once a day at a set time (at night keeps the NAS quiet during the day), or only at start. |

The same card shows the queue and lists **Files that could not be rendered**. **Render missing now** looks for new files at once.

- Models bigger than the thumbnail limit (1 GB by default, [Size limits](Size-Limits)) get no server thumbnail, but still open in the viewer.
- G-code files use the preview picture the slicer saved in them; files without one get a render of the toolpaths.
- A model's picture can also come from an image next to it: `benchy.jpg` becomes the cover of `benchy.stl`. See [Gallery and browsing](Gallery-and-Browsing#pictures-and-covers).
- To render a thumbnail from another angle, see [Viewer → Thumbnail view](Viewer#thumbnail-view).

## Compressed previews

Large models also get a compressed preview: a welded and meshopt-compressed GLB, often 10–20× smaller, that the viewer loads instead of the original. It keeps colours and textures (up to 2048 px). **Build a compressed preview for models larger than** sets the size (5 MB by default). Downloads always give you the original file.

For 3MF projects, the viewer first shows the preview; **Show plates and colours** loads the full file.

## Clearing the cache

- **Clear thumbnails** or **Clear previews** deletes them; they are made again in the background.
- **Clear all & re-render** starts over for everything.

## Keep the cache on another disk

Thumbnails and previews are kept in the data folder (`/app/data/thumbs` and `/app/data/previews`). Previews of large libraries can take several GB. To keep them on another disk or share, add a volume and point `CACHE_DIR` to it:

```yaml
    environment:
      - CACHE_DIR=/cache
    volumes:
      - /volume2/docker/3dviewer/data:/app/data
      - /volume3/3dviewer-cache:/cache
```

- At the next start, the thumbnails and previews already made are moved there (the log shows how many), so nothing has to be rendered again. Settings stay in the data folder.
- **Admin → Thumbnails → Thumbnails & previews** shows the folder in use and its size.
- The start-up checklist shows the free space of the cache folder, and warns when `CACHE_DIR` is not on a volume: the cache would be lost when the container is recreated.

### When the cache folder is full

If the cache folder runs out of space or reaches its quota (the log says *Cache folder … is full*), 3D Viewer keeps working:

- The move stops at the first file that does not fit. What was not moved stays in the data folder and is still used from there.
- While the cache is full, new thumbnails are saved in the data folder and no new previews are made (the viewer opens the original file).
- **Admin → Thumbnails → Storage** shows what is where. Give the cache more room and restart, and the rest is moved.
