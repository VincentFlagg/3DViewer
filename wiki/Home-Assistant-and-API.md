## API tokens

Signed-in accounts and the admin make tokens in the person menu → **API tokens**:

- **Read-only**: can only read.
- **Full access**: can also change things, as its owner could.

A token acts as the person who made it. The admin sees and can remove every token in **Admin → Accounts → API tokens**.

Send the token in a header:

```
Authorization: Bearer 3dv_...
```

## Library numbers

`GET /api/stats/summary` returns:

```json
{ "models": 1234, "size_bytes": 52428800000, "size_gb": 52.43, "libraries": 3,
  "added_7d": 12, "added_30d": 40, "views_30d": 310, "prints_30d": 9, "prints_total": 152, "version": "4.0.0" }
```

Try it:

```bash
curl -H "Authorization: Bearer 3dv_..." http://192.168.1.10:8733/api/stats/summary
```

## Home Assistant sensor

In `configuration.yaml`, with the token in `secrets.yaml`:

```yaml
rest:
  - resource: http://192.168.1.10:8733/api/stats/summary
    headers:
      Authorization: !secret threedviewer_token   # "Bearer 3dv_..."
    scan_interval: 900
    sensor:
      - name: "3D Viewer models"
        value_template: "{{ value_json.models }}"
        unit_of_measurement: "models"
      - name: "3D Viewer added this week"
        value_template: "{{ value_json.added_7d }}"
      - name: "3D Viewer library size"
        value_template: "{{ value_json.size_gb }}"
        unit_of_measurement: "GB"
```

`secrets.yaml`:

```yaml
threedviewer_token: "Bearer 3dv_..."
```

Use the port you mapped in the Compose file (`8733` by default), or `3000` if Home Assistant reaches the container directly on a Docker network.

## Other calls

The same token works for the other `/api/...` calls the app makes, for example `/api/stats`, `/api/queue` (the To print list) and `/api/printers`. Open the browser's developer tools on the 3D Viewer page to see the calls it makes.
