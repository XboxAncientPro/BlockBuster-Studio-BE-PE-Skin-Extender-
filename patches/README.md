# Bedrock Filmmaking Studio — pack patches

These patches are maintained for **PrimeGamingBoyzzYT's Bedrock Filmmaking Studio**
(`bbs:cam`, `bb:skinN`, `scripts/ui/StudioUI.js`). They are not for third-party
clones or rebrands.

All paths are relative to the extracted pack root (the folder containing `BP/`
and `RP/`).

## v4.5.6 — vanilla HUD, camera-safe takes, transition menu, 60 tracks

**File:** [`bedrock-filmmaking-studio-v4.5.6-camera-hud-tracks.patch`](./bedrock-filmmaking-studio-v4.5.6-camera-hud-tracks.patch)

**Base:** `Bedrock_Filmmaking_Studio_v4.5.5` build that already contains the
camera keyframe-menu parity fix (the build distributed as
`Bedrock_Filmmaking_Studio_v4.5.5_Cam_KF_Menu_Fix.mcaddon`).

### What it changes

| Area | Change |
| --- | --- |
| Camera recording | `bbs:cam` sessions no longer capture block place/break/explode, block interactions, liquid placement/pickup, item use/drop, eating, fishing, or `entityHit` attacks. |
| Camera playback | Camera tracks filter those event types in `_processEvents`, skip block pre-clear and hit-target pre-spawn, and never generate swing/place/break auto-animation keyframes. |
| Legacy camera takes | Old camera block snapshots are ignored by `TrackStore` snapshot rebuild and `restoreAllBlocks`, so they cannot edit the world. |
| HUD | Removes the `SKIN_MARKER` actionbar prefix, the `HUD Frame Skin` setting, `RP/ui/hud_screen.json`, and `RP/textures/ui/bb_actionbar_bg.png`. The Personal Director HUD uses the normal vanilla actionbar with no custom frame or right-edge docking. |
| Cut transition menu | Rebuilt `_scrubberCameraCutTransition` as the same icon-button `ActionFormData` style as the other camera tools. Effect and ease open their own icon lists; duration uses a normal slider. Effects are stored with canonical playback keys (`instant_cut`, `fade_black_short`, `fade_black_long`, `flash_white`, `whip_pan`, `shake`). |
| Track limit | `recording.maxTracks` 50 → **60**; `MAX_TRACKS` fallback and the AI Assistant fallback follow. |
| Packaging | BP/RP manifests bumped to `4.5.6`, names/blurbs updated, changelog entry added. |

### Apply

The patch contains one binary deletion (`bb_actionbar_bg.png`), so use `git apply`
rather than plain `patch`:

```bash
cd /path/to/extracted-pack-root
git apply --check --binary bedrock-filmmaking-studio-v4.5.6-camera-hud-tracks.patch
git apply --binary bedrock-filmmaking-studio-v4.5.6-camera-hud-tracks.patch
```

If you only have `patch`, apply the text hunks and then manually delete:

```text
RP/textures/ui/bb_actionbar_bg.png
```

### Verification

- 22/22 functional checks passed in a Node ESM harness with stubbed
  `@minecraft/server` and `@minecraft/server-ui` (camera capture/playback gates,
  legacy snapshot isolation, vanilla HUD text, transition menu flow, track limit).
- Rebuilt addon re-extracted: **186 BP files / 311 RP files**, `58` scripts pass
  `node --check`, no `hud_screen.json` or `bb_actionbar_bg.png`, both manifests
  valid at `4.5.6`.
- Final addon:
  `Bedrock_Filmmaking_Studio_v4.5.6_Vanilla_HUD_Camera_Safe.mcaddon`
  (3,930,765 bytes, SHA-256
  `33f32014d4f31e7106bc87d7a6d0e8b616c9c15792979057a0ec3cd3073a9297`).

### Existing builds

- `Bedrock_Filmmaking_Studio_v4.5.5_Cam_KF_Menu_Fix.mcaddon` — camera keyframe
  menu parity fix, previously delivered.
