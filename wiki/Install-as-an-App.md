**Install app** (the phone icon at the top) installs 3D Viewer on a computer, phone or tablet. It gets its own icon on the desktop, dock or home screen and opens in its own window, without the browser's bars.

## How to install

| Device | How |
| --- | --- |
| **iPhone, iPad** | Share → **Add to Home Screen**. Works over `http://` too. |
| **Android** | **Install app**, or the browser menu → **Install app**. Needs an `https://` address. |
| **Chrome or Edge on a computer** | **Install app**, or the install icon in the address bar. Needs an `https://` address. Over `http://`, Chrome's **Create shortcut… → Open as window** works too. |

Where the browser can't install it from the page, the button explains how.

## Getting an https:// address

Open 3D Viewer through your NAS's reverse proxy with a certificate, Tailscale, or a tunnel. See [Reverse proxy and HTTPS](Reverse-Proxy-and-HTTPS).

## The icon

The icon is a shaded 3D cube or a flat 2D one, set in **Admin → Viewer → Install as an app**. The browser tab and the logo use it too.

When the server can't be reached, the app shows a short message instead of an error page.
