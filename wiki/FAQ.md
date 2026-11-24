### Is 3D Viewer free?

Yes. Every feature works without paying. A donation of any amount gets a [supporter key](Supporter-Key) that turns off the short daily splash screen and the small reminder in the corner.

### Do my models leave my network?

No. 3D Viewer runs on your own NAS or server, and your models stay there; nothing is uploaded anywhere. It only connects out for what you set up yourself: [importing from a link](Import-from-Link), [notifications](Notifications), [single sign-on](Accounts-and-Sign-in#single-sign-on) and [printers](Printing).

### Does it change my model files?

No. Orientation, names, descriptions and series are stored next to the model in a `.3dviewer/` folder. [Prepare for print](Prepare-for-Print) and [Export](Check-Tools#export) give you a new file, or a copy next to the original.

### Which formats does it show?

STL, 3MF, OBJ, PLY, GLB/GLTF, FBX, 3DS, COLLADA, USD/USDZ, STEP/IGES, Blender, Lychee and G-code. See [Supported formats](Supported-Formats).

### Can it show colours and textures?

Yes, as they are stored in the file. GLB is the best format for that. See [Colours, materials and textures](Colours-Materials-and-Textures).

### Does it work on my phone?

Yes, in any modern browser. You can also [install it as an app](Install-as-an-App), and view models in AR at their real size.

### Which NAS does it run on?

UGREEN, Synology and QNAP are tested; any Linux server or PC with Docker works, on amd64 or arm64. See [NAS setup](NAS-Setup).

### Do I need a GPU?

No. With an Intel GPU, thumbnails render faster. See [GPU rendering](GPU-Rendering).

### Can other people use it?

Yes. Add [accounts](Accounts-and-Sign-in), or send a [share link](Share-Links) to one model or folder. Viewing and downloading are open to everyone on your network unless you make the server **Private**.

### Can I keep people from downloading a shared model?

You can leave the download buttons out of a [share link](Share-Links#what-visitors-see). The model still has to reach the visitor's browser to be shown in 3D, so that can't stop someone determined from saving it.

### Can I use it from outside my home?

Yes: put it [behind a reverse proxy with HTTPS](Reverse-Proxy-and-HTTPS), or use Tailscale or a VPN. Turn on **Private** first.

### Can I open models in my slicer?

Yes: **Open in slicer** in the viewer opens Bambu Studio, OrcaSlicer, PrusaSlicer, Creality Print or Cura. Sliced files can also be [sent to a printer](Printing#send-to-printer).

### Where are my settings kept?

In the data folder (`/app/data/config.json`). Back them up in **Admin → Backup**. See [Backups](Backups).

### How do I update?

Pull the new image and redeploy, then hard-refresh the browser. See [Updating](Updating).

### It's in the wrong language

The app follows your browser's language; the globe button at the top changes it. See [Languages and translations](Languages-and-Translations).

### I have an idea or found a bug

Post ideas in [Discussions → Ideas](https://github.com/VincentFlagg/3DViewer/discussions/categories/ideas) (👍 the ones you want, the most wanted are built first), and bugs as an [issue](https://github.com/VincentFlagg/3DViewer/issues/new?template=bug_report.yml).
