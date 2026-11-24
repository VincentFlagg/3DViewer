The server renders every thumbnail in the background with a headless browser. With a GPU it is much faster than on the CPU.

## Turn it on

Pass the GPU device to the container (it is in the [Compose file](Installation) already):

```yaml
    devices:
      - /dev/dri:/dev/dri
```

The renderer tries the GPU first (Vulkan, then OpenGL ES through Mesa). If neither works, it falls back to the CPU (SwiftShader). **Admin → Thumbnails** shows which one is in use and the GPU's name, and so does the container log at start.

## Which NAS have one

UGREEN DXP, Synology and QNAP models with an Intel CPU (for example N100, Celeron J4125, i3 or i5) have `/dev/dri`. Other models render on the CPU.

## Settings

| `RENDER_GPU` | |
| --- | --- |
| `auto` (default) | GPU when one works, else the CPU |
| `off` | Always the CPU |
| `force` | Also accepts a software GPU |

`DISABLE_SERVER_RENDER=true` turns the server renderer off completely; browsers render the thumbnails instead.

## Problems

- **The container won't start, with an error about `/dev/dri`**: the NAS has no GPU device. Remove the `devices` lines.
- **Admin shows the CPU although there is a GPU**: check that `/dev/dri` exists on the NAS (`ls /dev/dri` over SSH) and that the `devices` lines are there. The start-up checklist in the container log shows the renderer in use.
- Thumbnails still appear without a GPU, only more slowly. See [Thumbnails and previews](Thumbnails-and-Previews).
