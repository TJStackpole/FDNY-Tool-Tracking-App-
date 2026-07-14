# FDNY Apparatus Tool Inventory & Rig Check

A single-file, zero-install dashboard for fire company officers to verify apparatus tools at
the start of a tour, document discrepancies with comments and photos, and manage the
firehouse tool room. Built to host for free on GitHub Pages and to connect later to an
inventory / gear-management system and photo cloud.

> **Not affiliated with, or endorsed by, the FDNY.** The seeded engine/ladder tool lists are
> **supplemental** — compiled from *public* descriptions of FDNY riding positions
> (Fire Engineering, Firehouse, etc.), not an official FDNY tool-assignment table. Replace
> them with your department's official lists (in-app **Rigs & Setup**, or `content/`).

## What it does

- **Dashboard** — per-apparatus readiness (present / missing / damaged from the last check),
  open-discrepancy count, and pending upload/sync count for the selected firehouse.
- **Rig Check** — pick a rig and walk its tools grouped **by riding position and compartment**
  so the officer knows exactly where each item should be. Tap Present / Missing / Damaged,
  add a comment, and attach a photo to any line. Progress bar + submit.
- **Discrepancies & Chain of Custody** — missing/damaged items auto-log here with who flagged
  them, when, the tour, comments, and photos; resolving records who/when/how.
- **Tool Room** — a fully editable inventory of what each firehouse keeps in stock, with
  bins/locations, quantities, min-stock **low-stock flags**, and CSV export.
- **Rigs & Setup** — customize firehouses, apparatus, and each rig's expected tool loadout
  (the "what should be on the truck" master list every check runs against).
- **Photos & Uploads** — gallery of all captured photos with upload status.
- **Sync & Export** — configure your inventory-system and photo-cloud endpoints, push the
  queue, and export/import everything as JSON.
- **Reference** — the public sources behind the seed lists, plus a slot for your official
  tables.

## How the integrations work (honestly)

FDNY's inventory/gear systems and photo cloud are internal — a public static page can't reach
them directly, and it shouldn't hold secret API keys. So this app uses an **adapter** model:

- Everything you do is captured locally first (works fully offline).
- In **Sync & Export** you set a **POST endpoint** for your inventory system and one for your
  photo cloud. When set, the queue POSTs each item as `{ kind, data }` (rig checks,
  discrepancies, inventory changes, and photos).
- Point those endpoints at your agency's real API/bucket — or a small proxy that adds
  authentication — and the paperwork flows automatically. Until then, use **Export** (CSV/JSON).

This keeps it GitHub-friendly today and "speaks back to the FDNY system" the moment IT wires
up the endpoints.

## Run it

- **Locally:** open `index.html` (double-click). Photos use your device camera on mobile.
  The reference manifest auto-loader needs http(s), so to add references either host it or run
  `python3 -m http.server` and visit `http://localhost:8000`.
- **GitHub Pages:** push the repo → Settings → Pages → deploy from `main` / root.

## Data & privacy

Settings, rigs, inventory, checks, and discrepancies are stored in your browser
(`localStorage`); photos are stored locally in **IndexedDB**. Nothing leaves the device until
you configure an endpoint and push. Guarded fallbacks keep it working if storage is
unavailable. Because data is per-device, use **Export/Import JSON** (Sync view) to move a
firehouse's setup between devices, or configure a shared backend endpoint.

## Customize

- **Rigs & Setup** — add/rename firehouses and apparatus; edit every tool's name, location,
  category, and quantity.
- Seed values, categories, and location ordering live near the top of the `<script>` in
  `index.html` (`engineTools()`, `ladderTools()`, `CAT`, `ENGINE_ORDER`, `LADDER_ORDER`).

## Notes

- The header emblem is a **generic placeholder** (the FDNY logo is a City of New York
  trademark) — swap the inline `<svg>` in the top bar with authorized artwork.
- Tool lists are illustrative until you load your official tables; treat readiness numbers as
  reflecting the sample loadout until then.

## License

MIT — see [LICENSE](LICENSE). Covers the application code only, not any FDNY publications,
trademarks, or data you add.
