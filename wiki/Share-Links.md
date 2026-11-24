A share link opens one model, or one folder with everything in it, for anyone who has the link: no account needed, also on a [private server](Accounts-and-Sign-in#private-server).

## Make a link

Signed-in accounts and the admin click **Share link** in the viewer, or **Share** above a folder, and pick how long the link works: **1 day**, **7 days**, **30 days** or **until removed**. Then **Make link** and **Copy**.

The dialog lists the links already made for that model or folder, with **Copy** and **Remove**.

## What visitors see

- **A model**: that model in the viewer.
- **A folder**: that folder and its sub-folders, without the sidebar or the rest of the library. Visitors can open models and search inside it.

By default visitors can also use the tools and download. To keep the page simple, tick what to **Leave out of the page** when you make the link:

| Option | What it hides |
| --- | --- |
| **Tools and Prepare** | Measure, cut, export… |
| **Model info** | Size, dimensions, pictures, similar models |
| **View controls** | Light, orientation, wireframe, grid |
| **Download buttons** | The download buttons and the zip download |

The dialog starts from the defaults the admin sets in **Admin → Accounts → Share links**. Links made before this option existed follow those defaults too.

The model is still sent to the visitor's browser to show it in 3D. Leaving out the download buttons keeps the page simple, but cannot stop someone determined from saving the file.

## Manage links

- **Admin → Accounts → Share links** lists every link that works, who made it and until when, with **Remove**.
- Links keep working when the model or folder is moved or renamed in the app.
- A removed or expired link stops working at once.
- [Notifications](Notifications) can tell you when someone opens a share link.

## Sharing outside your home

The person you share with has to reach 3D Viewer: put it [behind a reverse proxy with HTTPS](Reverse-Proxy-and-HTTPS), and turn on **Private** so the link is the only thing they can see.
