# Bedrock Filmmaking Studio — Skin & Addon Workbench

A **100% offline, single-file HTML workbench** for customizing Minecraft Bedrock `.mcaddon` filmmaking packs directly in your browser — with **zero servers, zero CDNs, zero installs and zero internet required**.

Open [`index.html`](./index.html), drop your pack, reskin it, expand `bb:skin` entities, regenerate suggestions, audit the manifests and export a ready-to-import `.mcaddon`.

> **Renamed:** this project was previously published as *BlockBuster Studio — Skin & Addon Builder*. It is now **Bedrock Filmmaking Studio**. The `bb:` entity namespace is deliberately preserved so every existing BlockBuster Studio / Bedrock Filmmaking Studio pack still loads, edits and exports correctly.

---

## Highlights in the v5 Workbench

### 1. 100% Offline & Self-Contained
- **One `.html` file** — works from `file://` on Windows, macOS, Linux, Android, iOS, or hosted statically on GitHub Pages.
- **No external requests at all** — no fonts, stylesheets, images, libraries or analytics. Even the icon, logo and all FX are generated locally.
- **CSP / WebView safe** — a pure-JavaScript ZIP + Inflate engine and a JS-literal parser with zero `eval()`, zero `new Function()` and no native `alert()` / `prompt()` popups.
- **No telemetry** — the pack never leaves the browser tab.

### 2. Cinematic Studio UI
- Refreshed **clapperboard branding** for Bedrock Filmmaking Studio.
- Four switchable themes: **Studio Night**, **Cinema Gold** (warm spotlight premiere), **End Dimension** and **Studio Slate**.
- The chosen theme, sound setting and FX setting persist in `localStorage`.

### 3. Tactile Touch, Mouse & Sound Design (No Asset Files)
- **Pointer trails** on touch screens and mouse — lightweight, pixel-style sparkles on a full-screen canvas.
- **Click ripples, press pulses and particle bursts** on buttons, cards and tabs.
- **Generated SFX** with the Web Audio API — soft click ticks, add/remove cues, success and error chimes, undo/redo sweeps, and an export fanfare. No audio files, no CDN.
- **Haptic pulse** on supported mobile browsers.
- `prefers-reduced-motion` is respected automatically, and **SFX: On/Off** + **FX: On/Off** toggles live in the topbar.

### 4. Custom Skins, HD Support & Live 3D/2D Preview
- **Batch PNG drop zone** — drop one or dozens of textures to auto-create new `bb:skinN` entities, clean filenames into display names and register search keys.
- **Interactive preview stage** — drag/spin the **3D** character, or switch to **Front**, **Back** and **Raw UV Sheet** views.
- **Texture resolution & arm detection** — supports `64×64`, `128×128` HD and legacy `64×32` skins, with one-click **64×32 → 64×64** Bedrock conversion and automatic Classic (4px) vs. Slim (3px) detection.
- **Duplicate** the selected skin into a new slot in one click.

### 5. Expand `bb:skin` Entities (`bb:skin41+`)
- Add `+1`, `+5`, or a custom `+N` (`1–200`) slots in one click, and trim new tail slots back to the original count.
- Generates every required file automatically:
  - Behavior Pack entity JSON (`entities/bb_skinN.json`)
  - Resource Pack client entity JSON (`entity/bb_skinN.json`) with complete Molang initialization
  - Skin texture (`textures/entity/skins/skinN.png`)
  - Localization entry (`texts/en_US.lang` → `entity.bb:skinN.name=...`)
  - Slim arm geometry (`models/entity/humanoid.customSlim.geo.json`) derived from `humanoid.custom.geo.json` whenever a 3px skin exists.

### 6. Auto-Registration in Suggestions & Aliases (`StudioUI.js`)
- Automatically updates `SKINS`, `MOB_CATALOG` and `MOB_ALIASES` for **Suggest Mob**, **Quick Morph** and **Playback**.
- **Bulk Register All / Unregister All**, plus a **live suggestion simulator** for partial queries before exporting.
- **Auto-Detect Arms** re-checks every texture and syncs Classic/Slim geometry.
- Syncs hardcoded `bb:skin1...N` hints in `StudioUI.js`, `CommandHandler.js` and `AIAssistant.js`, and can repair missing Molang initializers on older slots.

### 7. Manifests, Pack Health & Export
- Edit BP/RP names and descriptions with the Minecraft `§` colour toolbar and a live in-game preview.
- Copy BP → RP, strip duplicate trailing RP lines, bump `[major, minor, patch]`, or regenerate UUIDs for a separate variant pack.
- **Pack Health audit** checks manifests, dependencies, textures, Molang, geometry, duplicate names and suggestion registration before packaging.
- **Undo / Redo** every skin edit, **Reset Edits** to the uploaded pack, and export the roster as `.csv`.

### 8. Quality-of-Life
- **Keyboard shortcuts** + built-in help dialog (`?`).
- **Full-window drag & drop** — drop a `.mcaddon` anywhere to open it, or PNGs to add skins.
- Two-step confirmation for destructive actions (trim, delete, reset) instead of native popups.
- Unsaved-changes guard when closing the tab.
- Accessible tabs, keyboard-selectable skin cards, visible focus rings and a polite live region for toasts.

---

## Quick Start

### Option A — Run Completely Offline
1. Download [`index.html`](./index.html).
2. Double-click it (or open it in Chrome, Edge, Firefox, Safari, or a mobile offline HTML viewer).
3. Drop your `.mcaddon` (for example `Bedrock_Filmmaking_Studio_v4.5.5_Directors_Cut.mcaddon`).

### Option B — Host on GitHub Pages
1. Keep the file named `index.html` at the repository root.
2. Enable **Settings → Pages** (deploy from the root of your default branch).
3. Open the Pages URL — everything still runs client-side.

---

## Workflow

1. **Open** your `.mcaddon` — supports nested `.mcpack` bundles and folder-structured archives.
2. **Skins & Entities** — select any slot to replace its PNG, rename it with `§` codes, switch Classic/Slim geometry, add search keywords or duplicate it. Use **+1 / +5 / +N** to expand, or drop PNGs in bulk.
3. **Suggestions & Aliases** — test partial searches and toggle script-hint syncing / Molang repair.
4. **Addon Description & Manifest** — customise BP/RP names, descriptions, versions and UUID regeneration.
5. **Pack Health & Export** — review the audit, choose a filename, then **Build & Download .mcaddon**.

---

## Keyboard Shortcuts

| Action | Shortcut |
| --- | --- |
| Open `.mcaddon` | `Ctrl` + `O` |
| Build & download | `Ctrl` + `E` |
| Undo / redo skin edit | `Ctrl` + `Z` / `Ctrl` + `Shift` + `Z` |
| Previous / next skin | `[` / `]` |
| Toggle SFX / FX | `M` / `V` |
| Cycle theme | `T` |
| Open help | `?` |
| Close dialogs | `Esc` |

---

## Files Modified Inside an Exported `.mcaddon`

| Pack | File | Purpose |
| --- | --- | --- |
| Behavior Pack | `manifest.json` | Name, description, version, dependencies, optional new UUIDs |
| Behavior Pack | `entities/bb_skinN.json` | Entity definitions for expanded slots |
| Behavior Pack | `scripts/ui/StudioUI.js` | Updated `SKINS`, `MOB_CATALOG`, `MOB_ALIASES`, skin range labels |
| Behavior Pack | `scripts/systems/CommandHandler.js` | Updated `/bb tutorial skins` range text (optional) |
| Behavior Pack | `scripts/systems/modules/AIAssistant.js` | Updated `/bb ai skins` range text (optional) |
| Resource Pack | `manifest.json` | Name, description, version, optional new UUIDs |
| Resource Pack | `entity/bb_skinN.json` | Client entities, textures, geometry, Molang variables |
| Resource Pack | `models/entity/humanoid.customSlim.geo.json` | Auto-generated 3px slim-arm geometry |
| Resource Pack | `textures/entity/skins/skinN.png` | Custom and converted PNG textures |
| Resource Pack | `texts/en_US.lang` | Updated `entity.bb:skinN.name` entries |

---

## Project Structure

```
.
├── index.html   # the entire workbench (UI, ZIP engine, patchers, SFX/FX)
├── README.md
└── LICENSE
```

---

## Browser Compatibility

Works in modern desktop and mobile browsers: Chrome, Edge, Firefox, Safari, Android Chrome/WebView and iOS Safari. Uses native `CompressionStream` / `DecompressionStream` (`deflate-raw`) when available, with a built-in RFC-1951 Inflate fallback and stored-ZIP fallback for older engines. Sound effects need Web Audio (widely supported); if unavailable, the workbench simply runs silently.

## Compatibility Notes

- Entity IDs stay in the `bb:skinN` namespace and file paths stay `bb_skinN.json` / `skinN.png`, so exported packs remain drop-in compatible with existing worlds and StudioUI scripts.
- The workbench identifies a pack by `scripts/ui/StudioUI.js`; both older **BlockBuster Studio** and current **Bedrock Filmmaking Studio** packs are accepted.
- Verified end-to-end against **Bedrock Filmmaking Studio v4.5.5 (The Director's Cut)** — 40 `bb:skin` entities, nested `.mcpack` bundles — loading, expanding to 41 slots, rewriting `StudioUI.js`, `en_US.lang`, both manifests and re-exporting a valid `.mcaddon`.
- Always test an exported pack in a copied world first. UUID regeneration creates a separate variant pack; leave it off to update in place.

---

## License

MIT — see [LICENSE](./LICENSE). Copyright (c) 2026 PrimeGamingBoyzzYT.
