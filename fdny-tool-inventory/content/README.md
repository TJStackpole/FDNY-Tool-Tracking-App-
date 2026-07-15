# Content folder — your official references

The app seeds engine/ladder tool lists from **public** descriptions of FDNY riding
positions. They're a starting point, not an official inventory. Put your real material here.

> ⚠️ FDNY operational manuals and tool-assignment tables are internal/intranet and
> copyrighted. Only add copies you're authorized to use, and **do not commit them to a
> public repository** — keep the repo private, or link to an access-controlled location.

## Add a reference (shows up in the Reference view)

Put a PDF here (or host it) and add an entry to `manifest.json`:

```json
{
  "references": [
    { "title": "Ladder Company Operations — tool tables", "file": "content/ladder-ops.pdf", "note": "Ch. 3" },
    { "title": "Engine Company Operations — equipment", "url": "https://your-access-controlled-host/engine-ops.pdf" }
  ]
}
```

## Load your real rig loadouts

The fastest way to replace the sample tools with your official lists:

1. Open the app → **Rigs & Setup** and edit each rig's tool rows (name, location/position,
   category, qty). This is fully customizable per firehouse.
2. Or build the lists once, then use **Sync & Export → Export all data (JSON)** to save them,
   and **Import JSON** to load the same setup on every firehouse's device.
