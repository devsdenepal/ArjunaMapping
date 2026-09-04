# ArjunaMapping

Advanced, open-source OSINT research-mapping tool. Organize identifiers, build connections, and pin locations for any research target — entirely **local-first**, so your data stays on your device.

Inspired by how investigators wire together discrete clues, ArjunaMapping gives you a node-based workspace (React Flow) plus a full map view (Google Maps **or** OpenStreetMap) so you can see both the *who/what* and the *where* of an investigation side by side.

## Features

- **Projects** — create named workspaces per research target; open/save projects as `.osint.json` files.
- **Identifier nodes** — a rich library of built-in identifier types: social media (Instagram, Facebook, X/Twitter, YouTube, TikTok, LinkedIn, Snapchat, Reddit, Discord, Telegram), contact (email, phone), personal (name, address, family), vehicle (vehicle, VIN, license plate), plus a **custom** catch-all type.
- **Connections** — link identifiers together (e.g. "this email belongs to this person") and browse the graph.
- **Map pinning** — pin visited/relevant locations with notes, dates, context, and people present. Optional Google Maps (API key) with a full **OpenStreetMap fallback** so the app works with zero setup.
- **Themes** — light/dark toggle with persistent preference.
- **Import/export** — projects, recents, custom icons, all data are local and portable.
- **No backend** — everything persists in `localStorage` and optional JSON files. API keys never leave the device.

## Getting Started

### Prerequisites

- Node.js 18+
- npm

### Install & run

```bash
npm install
npm run dev
```

Open [http://localhost:5173](http://localhost:5173).

### Build for production

```bash
npm run build
npm run preview
```

## Map Setup (optional)

ArjunaMapping works out of the box with **OpenStreetMap**. To use Google Maps instead:

1. Create a project in [Google Cloud Console](https://console.cloud.google.com/), enable **Maps JavaScript API** (+ **Geocoding API** for search), and create an API key.
2. Drop the key into `public/app.config.json` (copy from `app.config.example.json`), **or** paste it in-app via the **Settings → Maps** panel.
3. Optionally add a Map ID for styled maps (see `app.config.example.json`).

```
# public/app.config.json  (gitignored — keys never get committed)
{
  "googleMaps": {
    "apiKey": "AIza...",
    "mapId": ""
  }
}
```

Switch map providers anytime from the map tab's settings (Google ↔ OSM).

> Your API key stays on-device: either in `localStorage` or in the gitignored `public/app.config.json`. It is never embedded in project files.

## Project Files

- `public/app.config.json` — optional app config (maps API key / Map ID). Gitignored.
- `*.osint.json` — exported/saved project snapshots. Gitignored.

## Tech Stack

| Layer     | Tech                                                  |
| --------- | ----------------------------------------------------- |
| UI        | React 18, Vite 6                                      |
| Maps      | Leaflet + react-leaflet (OSM), @vis.gl/react-google-maps (Google) |
| Graph     | @xyflow/react (React Flow)                            |
| Storage   | localStorage, JSON file import/export                 |

## Directory Structure

```
src/
├── App.jsx                    # App shell, first-run / landing routing
├── main.jsx                   # Entry point (providers)
├── identifierTypes.js         # Built-in identifier type definitions
├── components/                # Landing, project view, map tabs, modals, pickers
├── context/                   # Theme, Project, AppConfig, CustomIcons, Navigation, NodeHistory, ProjectContext
├── images/icons/              # Badge/user icons
├── styles/                    # global.css, themes.css
└── utils/                     # appConfig, projectIO, clearAllData, createProject, recentProjects, customIcons
```

## Privacy & Security

- **100% local** — no accounts, no cloud sync, no telemetry.
- Project data and API keys never leave your browser/device.
- Do **not** commit `public/app.config.json` or `.osint.json` files (already gitignored).
- Review and comply with applicable laws and platform terms when conducting research; only collect information you are authorized to handle.

## License

MIT License. See [LICENSE](LICENSE) for details.

---

**Built for ethical investigators, researchers, and analysts. Use responsibly.**