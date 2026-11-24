| Format | Extensions | Notes |
| --- | --- | --- |
| STL | `.stl` | ASCII and binary. |
| 3MF | `.3mf` | Colours and materials; plates and filament colours of Bambu Studio, OrcaSlicer and PrusaSlicer projects. |
| OBJ | `.obj` (+ `.mtl`) | With its materials and textures. See [Colours, materials and textures](Colours-Materials-and-Textures). |
| PLY | `.ply` | Meshes and point clouds, with vertex colours. |
| glTF | `.glb`, `.gltf` | Including Draco and Meshopt compression. |
| FBX | `.fbx` | |
| 3DS | `.3ds` | |
| COLLADA | `.dae` | |
| USD | `.usdz`, `.usd`, `.usda`, `.usdc` | |
| STEP, IGES | `.step`, `.stp`, `.iges`, `.igs` | CAD. |
| Blender | `.blend` | Meshes (Blender 2.8 to 4.x). |
| Lychee Slicer | `.lys` | Resin scenes with their supports. |
| G-code | `.gcode`, `.bgcode` | Toolpaths, layer by layer. |
| ZBrush, 123D Catch | `.ztl`, `.zpr`, `.3dp` | Listed and downloadable, not shown in 3D. |

Archives (`.zip`, `.rar`, `.7z`, `.tar`…) are unpacked on upload: see [Organising files](Organising-Files#archives).

## Which way is up

Every format opens Z-up by default, as it does in slicers. Change it per format in **Admin → Viewer → Viewer defaults**, per model with the Z-up toggle in the viewer toolbar, or save a model's orientation in the viewer. COLLADA and USD files say which way is up and are turned to match.

## CAD files (STEP, IGES)

Shown like any model, with a thumbnail and the colours stored in the file. OpenCascade (as WebAssembly, in the browser) turns their surfaces into a mesh. For big files the server keeps a compressed preview, so they open fast the next time. A file that is all black (the default of many CAD programs) is shown in the model colour.

## Blender (.blend)

3D Viewer reads the meshes stored in a `.blend` (Blender 2.8 to 4.x, also compressed files) and shows:

- the mesh objects of the scene, where they are placed, with their material colour, or the base colour texture when it is packed in the file (with its UV map);
- copies made by particle systems (trees, grass, rocks) and by instanced collections. Particles that Blender places when the file is opened are spread over the emitter in the same number and size, but not at the same spots; a colour ramp in the material (leaves by season) gives each copy its own colour.

Not shown: modifiers and geometry nodes (the mesh is shown as modelled), textures that are not packed, curves, text and metaballs. A file without any mesh shows the preview picture Blender saved in it.

Blender files are shown Z-up, with Blender units as millimetres.

## Lychee Slicer scenes (.lys)

Supported resin prints open with all their models placed as in Lychee, and their supports rebuilt as light-grey struts, pads and braces.

- The **Supports** button in the viewer hides them to see the model alone; thumbnails show the supported scene.
- The supports are rebuilt from the scene's settings, so they look close to Lychee's but are not an exact copy. To print, open the `.lys` in Lychee Slicer.
- A scene that uses one of Lychee's own sample models doesn't contain the model, so it shows Lychee's preview picture instead.
- Scenes from older Lychee versions (3.5.1 and before) open too.

## G-code (.gcode, .bgcode)

The toolpaths of a sliced print as solid, shaded strands (the width and height of each printed line), so the part looks like the print, coloured by feature: outer and inner walls, infill, top and bottom surfaces, bridges, supports, skirt…

- **Solid** or **Lines** (lines are lighter for very large files, which open as lines).
- **By feature** or **One colour** (the model colour), and a tick box per feature to hide it, for example infill and inner walls to see only the outside.
- A **Layer** slider shows the print up to any layer; **Travel** shows the moves where the printer does not print.
- The panel lists layers, layer height, print time, filament and the slicer.
- Thumbnails use the preview picture the slicer saves in the file (PrusaSlicer, OrcaSlicer, Bambu Studio, Cura with a thumbnail plugin); files without one get a render of the toolpaths.

Features are read from the slicer's comments (`;TYPE:` in PrusaSlicer, OrcaSlicer and Cura, `; FEATURE:` in Bambu Studio); G-code without them is drawn in one colour.

Sliced files can be [sent to a printer](Printing#send-to-printer).

## ZBrush and 123D Catch (.ztl, .zpr, .3dp)

These formats are not published (and Autodesk 123D Catch was shut down in 2017; its `.3dp` projects only point to photos and a mesh stored elsewhere), so they cannot be shown in 3D. They appear in the gallery with their own icon, so a model folder shows everything in it: click one to download it, or select, move and delete them like models.

For a preview, export the model as STL or OBJ and keep it next to the original. To hide them, untick **Admin → Viewer → Viewer defaults → Show ZBrush and 123D Catch files**.
