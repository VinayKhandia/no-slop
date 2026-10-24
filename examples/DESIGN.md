# Design Direction: Systems Engineer Portfolio

## Concept
Tactile Instrument & Monastic Monospace. Inspired by UNIX workstations, clean telemetry dashboards, and precision aerospace hardware. Avoids generic SaaS rounded cards and gradient fluff in favor of high-contrast typographic hierarchy and crisp rectangular panels.

## Palette
- Background: `#0B0D0F` (deep obsidian void, reduces eye strain)
- Surface: `#14181D` (dark slate panel background)
- Surface Elevated: `#1C222A` (elevated cards, terminal header, active states)
- Text Primary: `#E6EDF3` (crisp white with slight warm tint, high contrast)
- Text Secondary: `#8B949E` (cool muted grey for timestamps, metadata, and labels)
- Accent: `#2EA043` (terminal phosphor green for active statuses, commands, and CTA)
- Accent Warm: `#D29922` (amber warning/build indicator for active experiments)
- Border / Muted: `#30363D` (subtle 1px boundary lines for structure)

## Typography
- Headings: `JetBrains Mono`, 700 weight, uppercase tracking +0.05em.
- Body: `Inter`, 400/500 weight, line-height 1.6 for comfortable reading.
- Code / Telemetry: `JetBrains Mono`, 400 weight, monospace precision.

## Spacing & Layout
- Grid unit: 4px base (4px, 8px, 12px, 16px, 24px, 32px, 48px).
- Container max-width: 1040px with 24px horizontal gutters.
- Borders: 1px solid `#30363D` throughout; border-radius strictly 4px (no pill shapes).

## Motion & Interaction
- Micro-interactions: 120ms `cubic-bezier(0.16, 1, 0.3, 1)` for button states and keyboard focus rings.
- Terminal typing effect: Discrete 25ms per-character cadence with a blinking block cursor (800ms period).
- Page transitions: Zero layout shift; simple opacity fade (150ms) on tab change.

## 3D & Advanced Effects
- Direction: Lightweight ASCII Canvas Shader / Three.js Orthographic Wireframe.
- Purpose: Renders a low-overhead wireframe polyhedron that slowly orbits in the hero backdrop, reacting subtly to mouse cursor movement without stalling the main thread. Fallback to CSS grid if WebGL is disabled.
