# RackWeave — DC Rack Connection Builder

<img width="1869" height="913" alt="image" src="https://github.com/user-attachments/assets/7ef67155-3dba-4a12-92e5-232b6d7b1d88" />

A static, single-file site that turns a YAML datacenter fiber design into an
interactive, draggable rack/connection diagram — and exports it as PNG, PDF,
HTML or SVG. Runs entirely in your browser.

🌐 **Live demo:** <https://melihteke.github.io/RackWeave.io/>

> Inspired by [netweave.io](https://melihteke.github.io/netweave.io/) — but
> rack & fiber focused.

## ✨ Features

- 📥 **YAML in, diagram out** — paste YAML, drop a `.yaml` file, or pick one
  of the bundled examples; the diagram renders automatically (live, debounced).
- 🧲 **Drag & drop nodes** — fine-tune cabinet positions; links re-route live.
- 🎛️ **Switch link styles** on the fly:
  Curved · Straight · Orthogonal · Rounded Orthogonal · Step
- ✨ Animated dashed fiber links (toggleable).
- 🌗 **Dark / Light theme** toggle.
- 📤 **Export** to **PNG**, **PDF** (A3 landscape), **HTML** (self-contained
  snapshot incl. source YAML), and **SVG**.
- 🖱️ Hover tooltips for racks (devices, power feeds) and links
  (strands, type, group).
- ℹ️ **About** modal & **GitHub** link in the navbar.
- 🪶 No build, no backend, no tracking — static site, ready for GitHub Pages.

## 🚀 Use

- **Hosted:** open <https://melihteke.github.io/RackWeave.io/>
- **Local:** open `index.html` in a browser, **or**
- **Self-host:** push to GitHub → enable Pages on the `main` branch root → done.

Bundled examples live in [`examples/`](examples/). Use the **Example** dropdown
in the toolbar to load one instantly.

## 📐 YAML schema

```yaml
dc_fiber_design:
  site: SITE-A
  site_metadata:
    region: Region-1
    location: Example City

  default_power_feeds: [pdu-a, pdu-b]

  colocations:
    - id: 1
      name: ZONE-A
      racks:
        - name: SITE-A.ZONE-A.RACK-01
          power_feeds: [pdu-a, pdu-b]
          devices:
            - SITE-A-ZA-SW-01
            - SITE-A-ZA-SW-02

  admin_zone:
    name: CORE
    racks:
      - name: SITE-A.CORE.FCR-01
        role: Fiber-Cross-Connect-Room
        power_feeds: [pdu-a, pdu-b]

  fiber_connections_between_racks:
    zone_a_connections:
      - { from: SITE-A.ZONE-A.RACK-01, to: SITE-A.CORE.FCR-01, strands: 24, type: SMF }
```

### Layout rules

- **Colocations** are placed in vertical columns: the **first colocation** is
  rendered on the **left**, the **second** on the **right**, alternating for
  any additional zones.
- **`admin_zone.racks`** are placed in the **center** as FCR cabinets
  (highlighted in amber).
- Connections from `fiber_connections_between_racks` (any keyed groups, or a
  flat list) are drawn between the corresponding rack nodes.

After auto-layout, you can **drag any node** to reposition it — your manual
positions are preserved across re-renders until you press **Auto-Layout**.

## 🔒 Privacy

Topology data is sensitive. RackWeave **never sends your YAML anywhere** — all
parsing, layout and exporting happens entirely client-side. No accounts, no
analytics, no backend.

## 🧪 Stack

- [`js-yaml`](https://github.com/nodeca/js-yaml) — YAML parsing
- [`jsPDF`](https://github.com/parallax/jsPDF) — PDF export
- Vanilla JS + SVG — no framework, no bundler

## 👤 Author

**Melih Teke** — Network Engineer ·
[LinkedIn](https://www.linkedin.com/in/melih-teke/)

## 📄 License

MIT
