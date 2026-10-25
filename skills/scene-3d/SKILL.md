---
name: scene-3d
description: Use for landing pages, portfolios, product and brand sites that benefit from 3D. Builds an immersive scroll-driven three.js world with a relevant hero object. Skip if the user says no 3D.
---

# Scene 3D

Load after design-taste and motion-craft. Default ON for landing pages and brand sites. Skip for dashboards and form-heavy tools.

## 1. Architecture
- One fixed full-screen canvas behind the page (position fixed, inset 0, pointer-events none; use a separate hit area for drag if needed). HTML content scrolls over it.
- three.js from CDN through an import map. All geometry and textures are made in code. No downloaded models.
- Scroll progress p (0 to 1) from Lenis/ScrollTrigger. Smooth it: s += (p - s) * (1 - Math.exp(-dt * 5)). Drive everything from s.
- Each page section maps to a range of s with its own camera position and object state.

## 2. Immersive environment (required)
Required. Read skills/scene-3d/enclosures.md and build a closed enclosure the camera sits inside.

## 3. Hero object (required, must match the product)
Build it procedurally and make it interactive. Examples:
- Cafe: cup and saucer using LatheGeometry (profile points), handle with TorusGeometry arc, coffee surface disc, steam as soft particles or noise sprites, floating beans.
- Sneakers/products: simplified shapes plus shader color changes.
- Music: reactive bars/rings or vinyl.
- Tech/SaaS: floating UI planes, glass cubes, data nodes.
- Real estate/architecture: rotating building blocks, light sweeps.
Interactions (at least 3):
- Drag to rotate with inertia (damped velocity).
- Hover: object tilts toward the pointer, glow or scale up slightly.
- Scroll: object moves between sections, explodes into parts, or changes variant (cup lifts, coffee swirls, beans orbit).
- Click: trigger a short animation (steam burst, color swap).
Add smaller satellite objects (beans, bubbles, shards) with varied depth for parallax.

## 4. Materials and light
Read skills/scene-3d/realism.md before building the hero object.

## 5. Performance budget
- renderer.setPixelRatio(Math.min(devicePixelRatio, 1.5)). antialias true.
- Under 60k triangles total. Under 2000 particles (use Points or InstancedMesh).
- No object creation inside the render loop. Reuse vectors and quaternions.
- Pause rendering when the tab is hidden or canvas is not visible.
- Dispose geometries, materials and textures when removed.
- On low power (navigator.hardwareConcurrency <= 4) reduce particles and pixel ratio further.

## 6. Fallbacks
- No WebGL or reduced motion: show a static gradient or CSS-drawn illustration of the object, keep all content usable.
- Loading: show a simple progress state, then fade the canvas in.

## 7. Composition (3D vs text)
- DESIGN.md states, per section, where the focal object sits (left, right, center-bottom, full-bleed) and where the text sits. They never share the same region.
- Hero default: text in one half of the viewport, object in the other. On mobile: object on top, text below. Keep this true at any width by shifting the object or camera with the aspect ratio (camera.setViewOffset or object x based on aspect).
- Body copy, buttons and labels never overlay the object. A single display headline may overlap the object only as a deliberate editorial move, with the object in front.
- Decorative orbits, rings and beans must not cross text blocks. Keep them in the object zone or at screen edges.

## 8. Geometry quality
Read skills/scene-3d/realism.md before building geometry.

## 9. Environment visibility
Read skills/scene-3d/enclosures.md for environment structure and lighting.

## 10. Style link
The chosen style recipe decides the environment type (tinted room, white cyclorama, patterned maximal room, void with floating shapes, and so on). Follow it.

## 11. Final check
- [ ] Camera is inside an environment that moves/rotates with scroll.
- [ ] Hero object matches the product and is built in code.
- [ ] 3+ interactions (drag, hover, scroll, click).
- [ ] Single shared render ticker, no allocations per frame.
- [ ] Under budget, fallback tested.
- [ ] Sections change camera position/mood as you scroll.
- [ ] Text and 3D object occupy different zones in every section.
- [ ] Curved surfaces are smooth, solid and closed.
- [ ] Environment is clearly visible and palette-based.
- [ ] visual-qa screenshots were reviewed.
- [ ] Enclosure shape is recognizable and textured, with props and changing sections.
- [ ] Realism self-check passed on a 2x zoom screenshot.