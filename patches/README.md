# Camera KF Menu Fix — Bedrock Filmmaking Studio v4.5.5

The camera entity (`bbs:cam`) keyframe menus had drifted into their own orange
"camera" variants. They now use the same chrome and interaction pattern as the
normal actor keyframe menus, while keeping every camera-only tool.

## What changed

| Screen | Before | After |
| --- | --- | --- |
| Keyframe List | `§6 CAMERA KEYFRAME LIST`, `Camera Keyframe List` section, no tip footer | `§3 KEYFRAME LIST`, `Keyframe List` section, `keyframeList` tip footer, `Track/Total` body, active-only list, same **Add Keyframe Category…** + **Back** index maths |
| Add Category | Modal with frame slider + dropdown | Icon `btn()` picker (10 camera types + Back), then the same **CHOOSE FRAME** slider step as actors |
| Edit Content | `§6 CAMERA TOOLS — fN`, 11 hard-coded buttons | `§a EDIT CONTENT - FRAME N`, `Edit Content` section, hint block, config-driven order (`keyframeScrubber.cameraContentMenuOrder`), keyed Back |
| Category sub-lists | Orange titles, custom options form | Category-coloured titles, `N keyframe(s) on <track>.` body, shared `_keyframeEntryActions` Edit/Delete flow |
| Frame panel | Actor status rows only | Camera status rows (easing, preset, shake, FOV, dolly speed, look-at, cut, visibility, sound, command) in the same `Status` layout |
| Clear Keyframes | Reported "nothing to clear" on camera tracks | Detects and clears all camera keyframe arrays at the frame |

Also fixes the easing editor dispatch (`keyType.includes("eas")`), which
previously never matched the list name `Easing Curves`, so the easing dropdown
was missing from **Edit Keyframe**.

Camera-only behaviours (ease/preset/shake/FOV/dolly speed/look-at/cut/
visibility/sound/command) are unchanged.

## Applying

From the pack root (the folder containing `BP/` and `RP/`):

```bash
patch -p1 < patches/bedrock-filmmaking-studio-v4.5.5-camera-kf-menu.patch
```

Then repackage the behaviour and resource packs.

## Verified

- 36/36 focused UI-harness checks pass (form titles, sections, tip footer,
  button order/counts, add-picker routing, sub-list edit/delete, camera frame
  status, clear behaviour, actor-list regression parity).
- Built `.mcaddon`: `google_drive/Bedrock_Filmmaking_Studio_v4.5.5_Cam_KF_Menu_Fix.mcaddon`
  (3,485,535 bytes; BP 186 files, RP 313 files; manifests unchanged).
- Google Drive copy: <https://drive.google.com/file/d/1fz5MZyl125P56B3spzezdy4x4T9W9k_8/view>
