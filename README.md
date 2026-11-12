# BlockBuster Studio — Offline Skin & Addon Workbench

A **100% offline, single-file HTML tool** (`BlockBuster_Studio_Skin_Builder.html`) for customizing **BlockBuster Studio** Minecraft Bedrock `.mcaddon` packages directly in your browser — with zero servers, zero external dependencies, and zero internet required.

Upload your `.mcaddon`, replace or expand `bb:skin` entities (`bb:skin41+`), auto-register every skin into in-game suggestions and aliases, edit pack descriptions with Minecraft `§` color formatting, and export a ready-to-import `.mcaddon`.

---

## Key Features

### 1. 100% Offline & Self-Contained
- **Single `.html` file** — open directly via `file://` on Windows, macOS, Linux, Android, or iOS (or host statically on GitHub Pages).
- **Zero external links or CDNs** — no remote fonts, stylesheets, libraries, or network calls.
- **CSP & WebView safe** — pure-JavaScript ZIP/Inflate engine and JS literal parser with zero `eval()`, zero `new Function()`, and zero native `prompt()`/`alert()` popups.
- **Minecraft Night Edition UI** — starry pixel night sky, square Minecraft moon, torchlight & deepslate OreUI beveled panels, moonlit skin stage, plus a topbar theme switcher (**Minecraft Night**, **End Dimension**, and **Studio Slate**).

### 2. Custom Skins, HD Support & Live 3D/2D Preview
- **Batch PNG Drop Zone** — drop one or dozens of skin textures at once to auto-create new `bb:skinN` entities, clean filenames into display names, and register search keys.
- **Interactive Preview Stage** — drag-to-spin **3D** character preview alongside **Front**, **Back**, and **Raw UV Sheet** views.
- **Texture Resolution & Arm Detection** — supports `64×64`, `128×128` HD, and legacy `64×32` skins (with one-click **Upgrade 64×32 → 64×64** Bedrock conversion) plus automatic Classic (4px Steve) vs. Slim (3px Alex) arm detection.

### 3. Expand `bb:skin` Entities (`bb:skin41+`)
- Add `+1`, `+5`, or a custom `+N` (`1–200`) skin entity slots in one click (or trim newly added tail slots back to the original pack count).
- Automatically generates for every slot:
  - Behavior Pack entity JSON (`entities/bb_skinN.json`)
  - Resource Pack client entity JSON (`entity/bb_skinN.json`) with complete Molang initialization
  - Skin texture (`textures/entity/skins/skinN.png`)
  - Localization display name (`texts/en_US.lang` → `entity.bb:skinN.name=...`)
  - Slim arm geometry (`models/entity/humanoid.customSlim.geo.json`) automatically derived from `humanoid.custom.geo.json` whenever any skin uses the 3px Slim model.

### 4. Auto-Register in Suggestions & Aliases (`StudioUI.js`)
- Automatically updates:
  - `SKINS` — skin list UI entries
  - `MOB_CATALOG` — **Choose a Mob → Suggest Mob** (`_mobSuggestionPicker`) searchable entries
  - `MOB_ALIASES` — **Quick Morph** and **Playback Actor Select** (`resolveEntityId`) aliases
- **In-Game Suggestion Simulator** — test partial queries (like `filterMobCatalog` and `resolveEntityId`) right in the **Suggestions & Aliases** tab before exporting.
- **Script Text Sync & Molang Repair**:
  - Syncs hardcoded `bb:skin1...20` range hints in `StudioUI.js`, `CommandHandler.js`, and `AIAssistant.js` to match your expanded skin count.
  - Optionally repairs missing Molang initializers (`variable.item_use_normalized`, `is_paperdoll`, `map_face_icon`, `is_first_person`, `player_x_rotation`) on existing `bb:skin21..40` entities.

### 5. Addon Description, Manifest & Pack Health Audit
- Edit Behavior Pack (`BP/manifest.json`) and Resource Pack (`RP/manifest.json`) names and descriptions using an interactive Minecraft `§` color/formatting toolbar and live in-game preview box.
- Shared controls to copy BP description → RP, strip duplicate trailing RP lines, bump `[major, minor, patch]` versions across manifests and dependencies, or optionally regenerate UUIDs to install as a separate variant pack.
- Pre-export **Pack Health & Export** audit verifies manifests, dependencies, Molang setup, geometry references, and suggestion registration before packaging.

---

## Quick Start

### Option A: Run Completely Offline
1. Download [`BlockBuster_Studio_Skin_Builder.html`](./BlockBuster_Studio_Skin_Builder.html).
2. Double-click the file (or open it in Chrome, Edge, Firefox, Safari, or a mobile offline HTML viewer).
3. Drop or choose your `BlockBuster_Studio_*.mcaddon` file.

### Option B: Host on GitHub Pages
1. Copy or rename `BlockBuster_Studio_Skin_Builder.html` to `index.html` (or link directly to `BlockBuster_Studio_Skin_Builder.html`).
2. Enable **Settings → Pages** in your GitHub repository.

---

## Workflow Inside the Workbench

1. **Upload `.mcaddon`** — Supports both nested `.mcpack` bundles (e.g., `BlockBuster_Studio_v4.5.5_Directors_Cut_Fixed.mcaddon`) and folder-structured `.mcaddon` archives.
2. **Skins & Entities Tab** — Click any existing slot to replace its PNG, rename it with `§` codes, switch Classic/Slim geometry, or add custom search keywords; or batch-drop PNGs / use **+1**, **+5**, **Expand +N...** to add new slots.
3. **Suggestions & Aliases Tab** — Preview how players search your skins in `_mobSuggestionPicker` and toggle script hint syncing / Molang fixes.
4. **Addon Description & Manifest Tab** — Customize BP & RP names, descriptions, version numbers, and UUID regeneration mode.
5. **Pack Health & Export Tab** — Review integrity checks, set your output filename, and click **Build & Download .mcaddon** (a persistent **Save `.mcaddon`** link is also shown in case your viewer blocks automatic downloads).

---

## Files Modified Inside Exported `.mcaddon`

| Pack | File | Purpose |
| --- | --- | --- |
| Behavior Pack | `manifest.json` | Name, description, version, dependency links, optional new UUIDs |
| Behavior Pack | `entities/bb_skinN.json` | Entity definitions for expanded slots |
| Behavior Pack | `scripts/ui/StudioUI.js` | Updated `SKINS`, `MOB_CATALOG`, `MOB_ALIASES`, and skin range labels |
| Behavior Pack | `scripts/systems/CommandHandler.js` | Updated `/bb tutorial skins` range text (optional) |
| Behavior Pack | `scripts/systems/modules/AIAssistant.js` | Updated `/bb ai skins` range text (optional) |
| Resource Pack | `manifest.json` | Name, description, version, optional new UUIDs |
| Resource Pack | `entity/bb_skinN.json` | Client entities, textures, geometry (`custom` / `customSlim`), Molang variables |
| Resource Pack | `models/entity/humanoid.customSlim.geo.json` | Auto-generated 3px slim-arm geometry (when Slim skins exist) |
| Resource Pack | `textures/entity/skins/skinN.png` | Custom and converted `64×64` / HD skin PNGs |
| Resource Pack | `texts/en_US.lang` | Updated `entity.bb:skinN.name` localization entries |

---

## Browser Compatibility

Works in any modern desktop or mobile browser (Chrome, Edge, Firefox, Safari, Android Chrome/WebView, iOS Safari). Uses native `CompressionStream`/`DecompressionStream` (`deflate-raw`) when available, with a built-in pure-JS RFC-1951 Inflate + ZIP fallback when streams are unsupported.
