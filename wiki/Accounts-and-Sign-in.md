## The admin and accounts

- **The admin** has the password set on the Admin page (or with `ADMIN_PASSWORD`). The admin signs in on the main page as **admin** and can change the library: upload, move, rename, delete and edit.
- **Accounts** are added by the admin in **Admin → Accounts → Accounts**. People sign in with the person button at the top of the main page. Accounts can look at and download models, make [share links](Share-Links), [import from a link](Import-from-Link) and keep their own marks; everything else that changes the library is for the admin.

Each person can change their own password from the person menu. The admin gives an account a new password, or removes it, on the Admin page.

## Your own marks

Everyone signed in (the admin too) gets their own:

- **Favourites**: **☆ Favourite** in the viewer; a star on the card.
- **Tags**: type a tag under **Mine** in the viewer (Enter adds it; your earlier tags are suggested). Select several models and use **Edit…** to tag them at once.
- **Print log**: **+ Add a print** with the date, the filament or resin, notes and a photo (made small in your browser).

The sidebar lists **My favourites**, **My prints** and each tag across all libraries, and **Show** above the grid can narrow a folder to them. Marks follow a model when it is moved or its folder renamed in the app.

Accounts with **Can print** also see the [To print list](Printing).

## Private server

With **Admin → Accounts → Private** on, only signed-in accounts and the admin see the libraries. Everyone else gets the sign-in form, or only what a [share link](Share-Links) opens. Turn it on if 3D Viewer can be reached from the internet.

## Two-factor sign-in

Anyone can turn on two-factor sign-in for themselves in the person menu (the admin too):

1. Scan the code with an authenticator app (Google Authenticator, Microsoft Authenticator, Authy, 1Password…).
2. Signing in then also asks for its 6-digit code.
3. Keep the eight recovery codes: each works once, for a lost phone.

The admin can **Require two-factor sign-in** for every account (each sets it up the next time they sign in), and **Reset 2FA** for an account that lost its phone. A lost admin phone: set `ADMIN_RESET_2FA=true` in the container settings, restart, then remove it again.

## Single sign-on

People can sign in with your login provider (Authelia, Authentik, Keycloak, Zitadel, Pocket ID… anything with OpenID Connect), as well as with a user name and password.

1. In the provider, add an application (client) with the **redirect URI** shown in **Admin → Accounts → Single sign-on**. It is `https://<your 3D Viewer address>/api/auth/sso/callback`.
2. In 3D Viewer, enter the **Issuer URL**, **Client ID** and **Client secret**, and a **Button name**.
3. Tick **Show “Sign in with …” on the main page**.

Accounts are made the first time someone signs in. Untick **Make an account the first time someone signs in** to let in only people already linked.

Single sign-on needs 3D Viewer at a stable address, usually [behind a reverse proxy with HTTPS](Reverse-Proxy-and-HTTPS). If the redirect URI shows the wrong address, set **Admin → Notifications → Public address of 3D Viewer**.

## Extra basic authentication

`AUTH_USER` and `AUTH_PASS` put HTTP basic authentication in front of the whole site, as well as 3D Viewer's own sign-in. Most people use **Private** instead, which keeps share links working without a password.

## Forgot the admin password

Set `ADMIN_PASSWORD` in the Compose file and restart the container. That sets a new admin password.

While `ADMIN_PASSWORD` is set, it wins at every start: a password changed on the Admin page goes back to it at the next restart. Remove it once you are back in, and the password stays as it is.
