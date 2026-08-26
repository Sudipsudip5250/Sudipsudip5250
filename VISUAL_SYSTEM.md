# Cyber-Research Visual System

This visual system turns Sudip Bhattarai’s portfolio and GitHub profile into a coherent research laboratory: precise, curious, slightly mysterious, and still welcoming. It is designed around a deep-space canvas, thin geometric scaffolding, true isometric depth, and small moments of human-readable status copy.

## Design tokens

| Token | Value | Use |
|---|---|---|
| Deep space | `#070B17` | Global page background and negative space |
| Research navy | `#111332` | Raised surfaces, cards, and stage interiors |
| Electric cyan | `#66E3FF` | Primary signal, links, active status, data streams |
| Soft violet | `#8B7CFF` | Secondary signal, research states, orbital paths |
| Warm amber | `#FFB86B` | Human warmth, build states, highlights, warning-free emphasis |
| Off-white | `#F4F6FF` | Primary copy and high-contrast labels |
| Muted blue-gray | `#9BA9C9` | Secondary copy, metadata, supporting descriptions |

The lighting direction is consistent: cyan and violet are rim lights from the upper-left and right edges, while amber is the warm under-light. Surfaces stay translucent enough to suggest glass, but backgrounds remain opaque enough for readable text in both GitHub themes and the portfolio theme toggle.

## Asset inventory

| Asset | Format | Size | Intended use |
|---|---|---:|---|
| `hero-banner.svg` | SVG | 1200 × 360 | Profile README hero and portfolio shareable social/OG visual |
| `mission-control.svg` | SVG | 1200 × 440 | README mission-control block and portfolio console section |
| `toolkit-constellation.svg` | SVG | 1200 × 480 | README toolkit visualization and portfolio toolkit route |
| `particle-field.svg` | SVG | 1200 × 720 | Atmosphere layer for future portfolio backgrounds |
| `glyph-ai.svg` | SVG | 160 × 160 | AI/model project card icon |
| `glyph-data.svg` | SVG | 160 × 160 | Data/visualization project card icon |
| `glyph-app.svg` | SVG | 160 × 160 | Mobile/interface project card icon |
| `glyph-rust.svg` | SVG | 160 × 160 | Systems/Rust project card icon |
| `project-card-template.svg` | SVG | 640 × 420 | README-facing glass project-card template |
| `project-card-template.png` | PNG | 640 × 420 | Static fallback for README previews |

All SVGs are authored as source-controlled assets rather than rasterized artwork. This keeps the exact copy legible, preserves 2× sharpness, and allows CSS/SMIL motion to be disabled for reduced-motion users where the renderer honors the media query.

## Motion rules

Motion communicates state instead of decoration. Orbital paths rotate slowly, data streams use long dash patterns, and node pulses breathe rather than pop. Interactive portfolio cards use a short hover lift and cursor-aware glow; README images remain useful as static fallbacks. The implementation must always respect `prefers-reduced-motion: reduce`, and no information is conveyed only through motion.

## Portfolio integration

The portfolio uses the same tokens in `src/styles.css`, applies the particle field as an ambient layer, adds the mission-control console to the home route, adds the toolkit constellation to `/toolkit`, and gives project cards a small floating glyph. The current route map, verified URLs, Cloudflare contact function, and project evidence remain unchanged.

## GitHub README integration

The profile README uses relative paths such as `./assets/hero-banner.svg`, `./assets/mission-control.svg`, and `./assets/toolkit-constellation.svg`. The banner contains the exact hierarchy **RESEARCH · BUILD · SHARE**, **SUDIP BHATTARAI**, **Generative AI · Full-stack · Open Source**, and **> turning curiosity into code_** so the identity remains visible even when external badge services are unavailable.

## Depth pass

The second pass adds more depth without increasing noise. Toolkit nodes now use three material treatments with brighter cores, outer rings, and longer connecting streams. Mission-control pathways gain inset plates, floating offsets, a scan line, and a subtle telemetry header. Portfolio cards use a pointer-positioned sheen, layered grid texture, a soft glass highlight, and a restrained 3D lift; status dots breathe slowly to distinguish `LIVE` from `EXPERIMENT` without relying on color alone.

## Living motion contract

The motion layer is deliberately slow and stateful. Toolkit rings rotate over 72–96 seconds, connection dashes travel over 14 seconds, node cores breathe over 8 seconds, and mission-control panels float by only a few pixels over 14 seconds. The particle field drifts at a very low opacity over 72–96 seconds so it can sit behind content without competing with it. The hero keeps all typography static while only the orbital and glow layers move. Every SVG includes a `prefers-reduced-motion: reduce` rule that freezes or disables nonessential motion, and the portfolio scroll reveals become immediately visible in reduced-motion mode.

The reusable `project-card-template.svg` and `.png` provide the README-facing card language: a glass surface, neon edge, status pill, floating glyph, readable metadata, and a clear details action. The live portfolio applies the same material language through CSS and uses the existing glyph mapping for verified projects.

## Advanced atmosphere and scroll rules

The portfolio atmosphere is a four-layer system: a drifting deep-space grid, low-opacity particle wash, thin neural-signal threads, and blurred cyan/violet volumetric glows. Mobile reduces the atmospheric intensity, while reduced-motion users receive a frozen field and an immediately readable interface.

The signal stage responds to three restrained inputs: time supplies the existing idle life, the pointer supplies a small cursor-following tilt, and scroll supplies a capped reactor rotation plus a small halo shift. The sticky signal indicator reports the section currently crossing the reading zone. These effects use passive listeners and `requestAnimationFrame` scheduling; no additional rendering library is needed.

## Runtime motion architecture

The portfolio uses a real `RuntimeParticles` canvas rather than relying on the SVG atmosphere for motion. It adapts particle count to coarse pointers, hardware concurrency, and reduced-motion preference; uses a capped device pixel ratio; draws only low-alpha dots and sparse local links; and applies subtle cursor influence through a global passive pointer listener without intercepting page input. The SVG particle field remains as a quiet visual fallback texture.

The signal stage is a raw WebGL runtime object with a CSS reactor fallback. `HeroLabScene` renders the luminous core, three separated orbital rails, four satellite nodes, and sparse telemetry links; the wrapper adds a grid, floor reflection, labels, and low-cost DOM hierarchy when WebGL is unavailable. The scene receives capped scroll-linked angle and desktop-only pointer tilt. Scroll work is scheduled through `requestAnimationFrame`, reveals use Intersection Observer, and all nonessential animation is disabled or frozen under `prefers-reduced-motion`.

## Runtime particle performance budget

The particle runtime uses device capability signals rather than a fixed desktop density. Desktop uses up to 62 particles at approximately 60 fps with sparse local links; coarse-pointer devices use 34 particles at approximately 30 fps with links disabled; constrained devices or `saveData` connections use 24–34 particles at approximately 25 fps with links disabled; and reduced-motion mode uses 18 static particles with no animation loop. The canvas is capped at a 2× device pixel ratio, uses a desynchronized 2D context when available, and keeps pointer influence local and passive. This keeps the moving field visible while protecting mobile battery and lower-end frame time.

## Complete runtime 3D redesign

The portfolio’s primary visual language is now generated at runtime rather than delivered as project-preview artwork. `HeroShaderBackground` provides the low-frequency volumetric atmosphere; `HeroLabScene` renders the interactive 3D Signal Reactor with its luminous core, orbital rails, and signal nodes; and `ProjectField` generates project-specific grid, orbit, core, and telemetry geometry from each project slug. Pointer and scroll state are passed into these layers as small transform inputs, while `prefers-reduced-motion`, coarse-pointer, low-power, and no-WebGL conditions reduce or freeze the scene without hiding content. SVG assets remain available for GitHub README compatibility, but the portfolio’s hero and workbench surfaces are live code-driven experiences.

## San-inspired chapter motion and repair pass

The portfolio now borrows the strongest interaction pattern from the `San` project without copying its application shell: a fixed section-aware WebGL scene changes geometry by route, follows scroll progress, responds to pointer position on capable devices, and throttles or freezes under reduced-motion and low-power conditions. The active chapter modes are hero Signal Reactor, work constellation, toolkit network, and contact beacon.

The workbench also has a dedicated WebGL renderer per project card. The previous empty-card defect came from an absolute-only `.project-field` whose computed width collapsed to zero inside the grid; the repair explicitly sets width, height, and minimum width to 100 percent. Each card now renders a visible wireframe object, orbital ring, node points, telemetry bars, live-code readout, pointer lighting, and project-specific color treatment. The CSS layer remains a readable label and fallback, while the geometry is generated in code.

## Always-on Signal Reactor

The home signal stage is a control-free, continuously rotating Signal Reactor / Orbital Data Core. The WebGL layer is intentionally hierarchical: a compact multi-point core with three short containment axes sits inside three widely spaced elliptical orbital rails; four separated satellite nodes and a small set of radial telemetry rays communicate active data flow without recreating a chemistry diagram. The CSS reactor shell is a low-cost fallback, not the primary rendering surface, and mirrors the same core/rail/satellite hierarchy with emissive depth, a soft floor reflection, and restrained telemetry labels. The scene begins in motion on page load, keeps the ASK / TEST / SHARE research framing, and uses CORE / LAB labels without a rotate or reset button. Pointer tilt remains desktop-only; coarse-pointer devices receive automatic motion without touch event work.

## Git history convention

Human-authored commits in the August 24–25 portfolio/profile work use the established identity **Sudip Bhattarai <sudipsudip5250@gmail.com>**. Automated contribution refresh commits remain attributed to `github-actions[bot]` so automation provenance is not rewritten as a human author.

## Premium editorial instrument pass

The 2026 refinement moves the portfolio from a collection of neon surfaces toward a chapter-based editorial instrument. The shell gives typography, spacing, dividers, and actions more authority while the runtime visuals carry one dominant metaphor per route. Home uses the Signal Reactor; Work uses three project-specific instruments; Toolkit uses a live eight-node capability graph; and the home mission-control surface uses a live three-path WebGL console. The static mission-control and toolkit SVGs remain preserved for GitHub README compatibility and fallback use, while the portfolio route uses live code-driven canvases.

The Work cards layer the shared code-generated WebGL field with distinct lightweight instruments: a rotor for Fan, clock hands and ticks for Hybrid Clock, and a connected temporary-room mesh for Ephemeral Chat. The generative AI showcase has three different runtime renderers within one accessible canvas: a prompt-to-path field, separated embedding neighborhoods, and a trace-oriented inference display. Tabs and pause/re-sample controls remain explicit.

The route-aware `ScrollScene3D` now uses chapter geometry instead of a shared cube preset: a reactor halo on Home, three instrument bays on Work, an eight-node graph on Toolkit, and an open beacon on Contact. Runtime scenes use bounded geometry, capped pixel ratios, hidden-tab pause, low-power heuristics, coarse-pointer safeguards, and reduced-motion fallbacks. SVG assets remain the README-facing visual layer and are not removed by this runtime upgrade.

### References

[1]: https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_best_practices "MDN — WebGL best practices"
