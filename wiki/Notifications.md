**Admin → Notifications** sends a short message when something happens. Messages that come at the same time are sent together.

## What to send a message about

- new models turn up (uploaded, imported or copied in);
- an [import from a link](Import-from-Link) finishes;
- someone opens a [share link](Share-Links);
- a scheduled [backup](Backups) fails.

**Public address of 3D Viewer** (optional, for example `https://3d.example.com`) is used for the links in messages, so they open 3D Viewer from wherever you read them.

## Where to send them

Turn on one or more, and use **Send a test** to check each.

| Service | What to enter |
| --- | --- |
| **Telegram** | A bot token (from @BotFather) and the chat ID. |
| **Discord** | A webhook URL (channel settings → Integrations → Webhooks). |
| **E-mail** | Any SMTP server: host, port, user, password, from and to. |
| **ntfy** | The topic URL (for example `https://ntfy.sh/my-3dviewer-x7k2`), and an access token if the topic is protected. |
| **Gotify** | The server URL and an app token. |

With ntfy.sh, anyone who knows the topic name can read it, so use a name that is hard to guess.
