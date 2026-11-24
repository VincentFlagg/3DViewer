3D Viewer shows models with the colours, materials and textures stored in them. This page lists what each format keeps, how to lay out the files so nothing goes missing, and what to check when a model shows up in the plain model colour.

## Which format to use

For a model with materials or textures, use **GLB**. It is one file with the mesh, materials and textures inside, so nothing can get lost when you copy, move or download it.

From Blender: **File → Export → glTF 2.0**, then set **Format** to **glTF Binary (.glb)**.

## What each format shows

| Format | What is shown | Files it needs |
| --- | --- | --- |
| **GLB** | Full materials and textures | None, everything is inside |
| **GLTF** | Full materials and textures | Its `.bin` and texture files, where the `.gltf` says they are |
| **OBJ** | Materials from its `.mtl` file and their textures | The `.mtl` named on the OBJ's `mtllib` line, and the textures the `.mtl` names |
| **FBX** | Materials and textures | Textures packed in the file, or next to it |
| **3DS, COLLADA (.dae)** | Materials and textures | Textures next to the file |
| **USDZ / USD** | Materials and textures | USDZ packs them in the file |
| **3MF** | Colours and materials. For Bambu Studio, OrcaSlicer and PrusaSlicer projects, also the filament colours and plates | None |
| **PLY** | Vertex colours | None |
| **STEP / IGES** | The colours saved in the file | None |
| **Blender (.blend)** | Material colours, and base colour textures packed in the file | Textures must be packed (**File → External Data → Pack Resources**) |
| **STL** | No materials. The few exporters that write colours into a binary STL are shown in colour | None |
| **G-code** | Coloured by feature (walls, infill, supports…) or in one colour. See [Supported formats](Supported-Formats#g-code-gcode-bgcode) | None |

## Laying out OBJ and GLTF files

Keep the extra files next to the model, under the exact names the files use:

```
Dragon/
├── dragon.obj        ← "mtllib dragon.mtl"
├── dragon.mtl        ← "map_Kd textures/dragon_diffuse.png"
└── textures/
    └── dragon_diffuse.png
```

- Paths in the `.mtl` or `.gltf` are relative to the model's folder. A sub-folder like `textures/` works.
- Absolute paths from the computer that made the file (`C:\Users\...\dragon.png`) cannot be found on the server. Open the `.mtl` in a text editor and change them to a relative path.
- Names are case-sensitive on a NAS: `Dragon.PNG` and `dragon.png` are different files.
- **Download** of an OBJ or GLTF gives a `.zip` with the `.mtl`, `.bin` and textures it needs.

## When a model shows up in the plain model colour

A model without a material of its own, or with only plain white or grey materials, is shown in the **Default model color** (**Admin → Viewer → Viewer defaults**), like an STL. If a model you expected in colour shows up that way, check that:

1. the `.mtl` or texture files are next to the model, under the names the model uses (see above);
2. the file has materials at all: many STL, OBJ and 3MF exports have none;
3. for STEP files, the file isn't all black, the default of many CAD programs. Those are shown in the model colour on purpose.

A texture that can't be found is left out, so the model isn't drawn black. The rest of its materials are still shown.

## Large models

Large models get a compressed preview that the viewer loads first. The preview keeps the textures, at up to 2048 px. For 3MF projects, **Show plates and colours** loads the full file with the slicer's plates and filament colours. Downloads always give you the original file.

## Export

**Tools → Export** (STL, 3MF, OBJ) writes the shape only, without the file's own materials and textures. Colours you paint with [Paint](Prepare-for-Print#paint) are exported in 3MF for Bambu Studio / OrcaSlicer, PrusaSlicer and other slicers.
