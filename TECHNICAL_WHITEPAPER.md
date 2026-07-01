# Technical White Paper
## KORU: The Fight for Eden — Build 4.0
### First Title of the Primal ONE Franchise

**Classification:** Proprietary — Internal & Authorized Licensee Distribution Only
**Document Owner:** Primal ONE
**Status:** Current Build

---

## 1. Franchise Positioning

**Primal ONE** is a proprietary interactive entertainment franchise built
around a single founding premise: primal instinct, fused with synthetic
technology, is Earth's last defense against an invading machine
intelligence. **Koru: The Fight for Eden** is the flagship title and
canonical entry point into the Primal ONE universe, establishing its core
cast, antagonist faction, and visual identity for all future titles,
spin-offs, and licensed media under the Primal ONE name.

All character IP, faction lore, and world-building introduced in this
build (Koru, the Zytheron Hive-Mind, the Zytheron Craft fleet class, the
Eden Reclamation Project, and the Hive Sovereign "Zyxar") are canon assets
of the Primal ONE franchise and are governed by the accompanying
`LICENSE.md`.

---

## 2. Product Summary

| | |
|---|---|
| Title | Koru: The Fight for Eden |
| Franchise | Primal ONE |
| Build | 4.0 |
| Genre | Top-down / third-person arena shooter |
| Platform | WebGL (browser client), single static HTML deployment |
| Engine | Three.js r128 |
| Session Structure | 3-sector campaign with escalating AI difficulty and a franchise boss encounter |

---

## 3. Engineering Architecture

### 3.1 Rendering Pipeline
- **Renderer:** `THREE.WebGLRenderer`, ACES Filmic tone mapping, sRGB output
  encoding, PCF soft shadow mapping.
- **Post-processing:** `EffectComposer` → `RenderPass` → `SSAOPass`
  (screen-space ambient occlusion), with automatic graceful fallback to
  direct rendering if the post-processing chain fails to initialize on a
  given client (older GPUs / restricted WebGL contexts).
- **PBR Environment Reflections:** A procedurally generated equirectangular
  gradient is converted via `THREE.PMREMGenerator` into `scene.environment`,
  giving all PBR-material surfaces (metallic hull plating, chrome trim on
  both playable and enemy assets) physically plausible ambient reflections
  without the cost of real-time screen-space reflection tracing.
- **Material Model:** All craft and character surfaces use
  `MeshStandardMaterial` / native glTF PBR material definitions
  (`baseColorTexture`, `metallicFactor`, `roughnessFactor`, emissive
  channels), read directly from the source `.glb` files' PBR
  specification.

### 3.2 Asset Pipeline
- **Player Character:** Procedural fallback bio-mech frame (always
  available, zero external dependency) with an optional high-fidelity
  `koru.glb` model swap-in (Loadout Option 2), including animation-clip
  blending (`idle` ↔ `sneak walk`) via `THREE.AnimationMixer`.
- **Enemy Fleet Craft:** `ZYTHERON_CRAFT.glb` — the canonical Zytheron
  fighter-class fleet craft asset. Loaded once, bounding-box normalized at
  runtime, and instanced (cloned) across the enemy object pool. Falls back
  to a procedural placeholder shape if the asset is unavailable, ensuring
  the game remains playable in incomplete deployments.
- **Scale Normalization:** Enemy craft height is programmatically resolved
  against a fixed player reference height and scaled to a 1.5× multiplier,
  guaranteeing consistent in-game proportion regardless of the source
  model's native export scale.

### 3.3 Enemy AI & Combat Systems
- **State Machine:** IDLE → SEEK → ATTACK, driven by proximity thresholds
  against the player position, evaluated on a staggered per-frame offset
  for performance at scale (up to 50 pooled enemy instances).
- **Detection Array:** Each fighter-class craft carries two offset
  circular radar rings that continuously rotate, increasing sweep speed
  and emissive intensity once the player enters engagement range —
  visualizing the "scouting" phase of the AI state machine prior to
  weapons release.
- **Weapons Array:** A triangular three-point emitter mount fires
  simultaneous converging beam effects at the moment of proximity-
  triggered attack, layered on top of the existing pooled-projectile
  damage system for gameplay-balance consistency with prior builds.
- **Object Pooling:** Enemies, projectiles, particles, and laser-beam FX
  are all managed through a shared `Pool` utility to avoid per-frame
  garbage collection overhead during sustained combat.

### 3.4 Environment System
- Procedurally generated jungle biome: layered canopy trees with buttress
  root geometry, undergrowth shrubs, cross-plane fern clutter, drifting
  low ground mist sprites, and a canvas-generated noise texture applied to
  the ground plane for a naturalistic forest-floor read under ambient
  occlusion.
- Obstacle system distinguishes between projectile-blocking cover (trees)
  and movement-only collision (shrubs), preserved unchanged from prior
  builds for gameplay-balance continuity.

### 3.5 Mission / Level Structure
| Sector | Name | Objective | Timer | Notes |
|---|---|---|---|---|
| I | Canopy Breach | Scout & Destroy | 180s | Extended pacing window for player onboarding |
| II | Hive Infiltration | Extract Nodes | 60s | Escalated AI aggression scaling |
| III | Zyxar's Core | Boss Defeat | 90s | Hive Sovereign flagship encounter |

---

## 4. Front-End Player Experience

1. **Splash Screen** — Branded title art (`splashscreen.jpg`) with a
   single "Enter" call to action.
2. **Mission Dossier Screen** — Presents both franchise-canon combat
   assets: Koru (playable, selectable loadout) and the Zytheron Craft
   (hostile intelligence entry, non-playable), each rendered in a live,
   auto-orbiting 3D preview viewer with accompanying franchise lore text.
3. **Gameplay HUD** — Real-time armor integrity, neural overclock
   (dash resource), kill counter, sector timer, and score tracking,
   unchanged in logic from prior builds to preserve player familiarity
   across franchise updates.

---

## 5. Franchise Extension Notes

This build establishes the following canon assets as reusable Primal ONE
franchise IP for future titles, updates, or licensed spin-off media:

- **Koru** — bio-mechanical reclamation unit, franchise protagonist.
- **Zytheron Hive-Mind** — primary antagonist faction.
- **Zytheron Craft** — fighter-class fleet vehicle, antagonist faction
  signature unit.
- **Zyxar** — Hive Sovereign, franchise boss-tier antagonist.
- **Eden Reclamation Project** — in-universe player faction / mission
  framework.

Any future Primal ONE title reusing these assets or names must comply
with the ownership terms defined in `LICENSE.md`.

---

© Primal ONE. All rights reserved. This document contains proprietary and
confidential technical information and is provided to authorized
licensees for deployment purposes only.
