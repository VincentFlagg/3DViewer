To open 3D Viewer from outside your home, with a name like `https://3d.example.com`, put it behind a reverse proxy with a certificate. HTTPS is also needed to [install it as an app](Install-as-an-App) on Android and in Chrome or Edge, and for AR on Android.

## Before you start

- **Give it its own (sub)domain**, for example `3d.example.com`. 3D Viewer has to be served at the root of the address; a sub-path such as `example.com/3d/` does not work.
- **Set `SESSION_COOKIE_SECURE=true`** in the Compose file once you open it over HTTPS, so the sign-in cookie is only sent over HTTPS.
- **Remove the upload size limit** in the proxy, or uploads of large models fail (see below).
- **Make the server private** (**Admin → Accounts → Private**) if it is reachable from the internet, so only signed-in people see your libraries. [Share links](Share-Links) keep working.
- To have links in [notifications](Notifications) use the public address, set it in **Admin → Notifications → Public address of 3D Viewer**.

3D Viewer trusts the `X-Forwarded-*` headers of a proxy on the same machine or on your local network, so it knows the visitor's address and that the connection is HTTPS.

## Caddy

```
3d.example.com {
    reverse_proxy 192.168.1.10:8733
}
```

Caddy gets the certificate by itself and has no upload limit by default.

## Nginx

```nginx
server {
    listen 443 ssl;
    server_name 3d.example.com;
    # ssl_certificate / ssl_certificate_key …

    client_max_body_size 0;          # no upload limit
    proxy_request_buffering off;     # send large uploads straight through

    location / {
        proxy_pass http://192.168.1.10:8733;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 600s;     # long imports and big downloads
    }
}
```

## Nginx Proxy Manager

1. **Add Proxy Host**: domain `3d.example.com`, scheme `http`, forward to the NAS IP and port `8733`.
2. **SSL** tab: request a certificate and turn on **Force SSL**.
3. **Advanced** tab, custom Nginx configuration:

   ```nginx
   client_max_body_size 0;
   proxy_request_buffering off;
   ```

## Traefik

```yaml
    labels:
      - traefik.enable=true
      - traefik.http.routers.3dviewer.rule=Host(`3d.example.com`)
      - traefik.http.routers.3dviewer.entrypoints=websecure
      - traefik.http.routers.3dviewer.tls.certresolver=letsencrypt
      - traefik.http.services.3dviewer.loadbalancer.server.port=3000
```

Traefik has no upload limit by default.

## UGREEN, Synology and QNAP built-in proxies

The NAS's own reverse proxy (Synology: **Control Panel → Login Portal → Advanced → Reverse Proxy**) works too: forward `https://3d.example.com` to `http://localhost:8733`. If large uploads fail, the proxy's body size limit is the usual cause.

## Without opening a port

Tailscale, a Cloudflare Tunnel or a VPN to your home also work, and keep 3D Viewer off the open internet. On its free plan, a Cloudflare Tunnel refuses requests over 100 MB. 3D Viewer sends uploads in batches of up to 256 MB, so big uploads can fail that way. Upload large files, or many files at once, on your home network.

## Extra protection

`AUTH_USER` and `AUTH_PASS` put HTTP basic authentication in front of the whole site, as well as 3D Viewer's own sign-in. Share links then also need that password, so most people use **Private** instead. For single sign-on (Authelia, Authentik, Keycloak…), see [Accounts and sign-in](Accounts-and-Sign-in#single-sign-on).

## When something doesn't work

- **"Upload failed: the connection … was lost"**: the proxy's body size limit. The container log says how far the upload got.
- **Signed out right after signing in**: `SESSION_COOKIE_SECURE=true` while opening it over plain `http://`. Use the `https://` address, or set it back to `false`.
