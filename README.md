# KORU: The Fight for Eden
### A Primal ONE Franchise Title — Build 4.0

---

## 1. Overview

**Koru: The Fight for Eden** is a browser-based, single-file WebGL arena
shooter built on Three.js. It is the founding title of the **Primal ONE**
franchise — a multi-title universe centered on neural-linked bio-mechanical
reclamation units fighting to reverse the Zytheron Hive-Mind's occupation of
Earth's remaining wild biomes.

This package contains the complete client-side build. No backend, database,
or build step is required — it runs directly from a static file server.

---

## 2. Package Contents

| File | Required | Description |
|---|---|---|
| `koru_the_fight_for_eden_AAA-4.html` | Yes | The complete game client (HTML/CSS/JS, single file). |
| `ZYTHERON_CRAFT.glb` | Yes | Enemy fighter-class fleet craft 3D asset. Must sit in the same folder as the HTML file. |
| `koru.glb` | Optional | Playable Koru character model (Loadout Option 2). Supply your own; the game falls back to a procedural bio-mech frame if absent. |
| `splashscreen.jpg` | Optional | Title splash background image. Supply your own; the game falls back to a solid background if absent. |
| `README.md` | — | This file. |
| `LICENSE.md` | — | Proprietary license governing use of this software. |
| `TECHNICAL_WHITEPAPER.md` | — | Engineering and design documentation. |

---



The client loads the following at runtime — an internet connection is
required for first load unless these are vendored locally:

- Three.js r128 core + GLTFLoader, OrbitControls, and the EffectComposer /
  RenderPass / SSAOPass post-processing chain (`cdn.jsdelivr.net`)
- Tailwind CDN build (`cdn.tailwindcss.com`)
- Google Fonts: Orbitron, Rajdhani, JetBrains Mono (`fonts.googleapis.com`)


---

## 5. Ownership & License

This software is proprietary and confidential. See `LICENSE.md` for the
full terms. No portion of this codebase, its assets, or its associated
documentation may be copied, redistributed, reverse engineered, or used to
train machine learning models without prior written authorization from the
rights holder.

© Primal ONE. All rights reserved.
