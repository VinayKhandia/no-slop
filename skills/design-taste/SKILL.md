---
name: design-taste
description: Establishes a cohesive visual, typographic, motion, and optional 3D design direction before any UI code is written.
---

# Design Taste

Avoid generic, boilerplate interfaces. For any task involving user interfaces, establish a deliberate design direction before writing any frontend code.

## Core Principle

Never jump straight into writing HTML/CSS or React components without a documented design system. Create a concise `DESIGN.md` in the project root that guides all frontend development.

## Design Decisions Checklist

1. **Concept**: The personality and visual metaphor of the application (e.g., "editorial darkroom", "tactile utilitarian instrument", "warm minimalist archive"). Avoid "generic SaaS card layout".
2. **Color Palette**: Specify primary, secondary, surface, background, text, and accent colors with explicit hex codes and distinct functional roles. Ensure accessible contrast ratios.
3. **Typography Pairing**: Select deliberate font pairings (one expressive heading face, one legible body face). Define size, weight, and line-height scale.
4. **Spacing System**: Enforce a strict spatial grid (typically 4px or 8px base units) for margins, padding, and layout gutters.
5. **Motion Principles**: Define transition curves, durations (e.g., 150ms for micro-interactions, 300ms for layout transitions), and easing functions. Motion must inform context, not distract.
6. **Optional 3D / Creative Tech Direction**: Where appropriate to the product concept, evaluate lightweight 3D or dynamic interactive effects (three.js, React Three Fiber, WebGL shaders, GSAP scroll-triggered animations). Specify whether 3D enhances the narrative or should be omitted to maintain lightweight performance.

## Output Structure: DESIGN.md

Generate a concise `DESIGN.md` following this structure:

```markdown
# Design Direction

## Concept
[1-2 sentences on visual identity and user feeling]

## Palette
- Background: #XXXXXX (purpose)
- Surface: #XXXXXX (purpose)
- Text Primary: #XXXXXX (purpose)
- Text Secondary: #XXXXXX (purpose)
- Accent: #XXXXXX (purpose)
- Border / Muted: #XXXXXX (purpose)

## Typography
- Headings: [Font family, weights, scale]
- Body / Mono: [Font family, weights, scale]

## Spacing & Layout
- Grid unit: [e.g., 4px / 8px]
- Layout max-width and container padding

## Motion & Interaction
- Hover / Focus transitions: [duration + ease]
- Page / Modal entrance: [duration + ease]

## 3D & Advanced Effects
- Direction: [None | Three.js | GSAP | Canvas]
- Purpose: [How it serves the product concept without bloating bundle size]
```

The frontend role must adhere strictly to `DESIGN.md`.
