Signed-in accounts and the admin click **Import** at the top and paste a link. It goes into the folder that is open.

## Model pages

A model page on **Printables**, **Thingiverse** or **MakerWorld** becomes a new folder named after the model, with:

- its files (archives unpacked);
- its first picture as the folder picture, and the other pictures in `images/`;
- a `README.md` with the description and the link it came from.

| Site | Notes |
| --- | --- |
| Printables | Works as it is. |
| Thingiverse | Needs an app token (free): paste it in **Admin → Library → Import from link**. |
| MakerWorld | Only signed-in members can download files, so usually only the pictures and description come in, with a note to download the 3MF there and upload it. |

## Direct file links

A link straight to a file (`.stl`, `.3mf`, `.zip`…) is saved in the folder; archives are unpacked like an upload.

## How it works

- The server downloads it in the background; the dialog shows the progress.
- Each file can be as large as the [upload limit](Size-Limits).
- Accounts cannot import from addresses on the local network; the admin can.
- [Notifications](Notifications) can tell you when an import finishes.
- Sites change how they answer from time to time. When one does, the error says to download the files there and upload them instead.
