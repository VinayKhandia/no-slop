---
name: motion-craft
description: Use for any website with animation or scroll effects. Rules for smooth 60fps motion, scroll choreography, and cursor effects. Prevents laggy or generic animation.
---

# Motion Craft

Load after design-taste. Smooth beats flashy: a laggy effect is worse than no effect.

## 1. Performance rules (hard)
- Animate only transform and opacity (plus clip-path and CSS variables read by shaders). Never animate width, height, top, left, margin, box-shadow, filter blur on large areas.
- ONE animation loop: Lenis drives scroll, gsap.ticker calls lenis.raf(time*1000), gsap.ticker.lagSmoothing(0), and lenis.on("scroll", ScrollTrigger.update). Three.js renders inside the same ticker. Never run a second requestAnimationFrame loop.
- Use scrub: 1 (or 0.6 to 1.2) on scrubbed triggers for built-in smoothing.
- Add will-change: transform only on elements animating continuously. Remove it after.
- Avoid backdrop-filter on large or many elements. Max 1 to 2 small glass panels. Safari struggles.
- No layout reads (getBoundingClientRect, offsetHeight) inside per-frame code. Cache values on resize.
- Split text into lines/words once at load. Never re-split during scroll.
- Images: set width and height, use loading="lazy" below the fold. Compress.
- Do not create more than about 30 ScrollTriggers. Use timelines with one trigger each.
- Call ScrollTrigger.refresh() after fonts and images load.

## 2. Easing and rhythm
- Entrances: power3.out or expo.out, 0.8 to 1.2s. Stagger 0.05 to 0.12s.
- Scrubbed motion: ease "none" with scrub smoothing, never bouncy.
- Vary effects per section. Same fade-up everywhere reads as a template.
- Hold moments: pin a section so the user can absorb one big idea.

## 3. Scroll choreography (use at least 5, including 1 and 2)
1. Pinned storyline: a pinned section where scroll drives a multi-step timeline (object transforms, copy swaps, numbers change).
2. Scene-linked scroll: scroll progress drives the 3D camera and objects (see scene-3d).
3. Line/word mask reveals for headlines (overflow hidden, y from 110%).
4. Clip-path image wipes and scale-down reveals (inset() to 0).
5. Horizontal scroll gallery inside a pinned section.
6. Velocity skew: skewY or scale of marquee text based on scroll velocity, clamped.
7. Multi-layer parallax (3 depths minimum).
8. Section background color shifts through a CSS variable tied to scroll.
9. Number counters and SVG path drawing on scroll.
10. Sticky stacking cards that scale back as the next arrives.
Plan one or two per section in DESIGN.md. Do not use all in one section.

## 4. Cursor effects (desktop only, skip on touch via matchMedia("(pointer: fine)"))
Pick at least 2:
- Custom cursor dot plus ring that follows with lerp (ring lags behind).
- Cursor grows or changes label on hover ("View", "Drag", "Play").
- Magnetic buttons: element moves slightly toward cursor, springs back.
- Spotlight or glow following the cursor via CSS variables (--x, --y).
- Tilt cards in 3D on hover (rotateX/Y from pointer, perspective).
- Light trail on a small canvas, max 20 points, auto-fades.
Hide the native cursor only if the custom one works. Keep it under 1ms per frame.

## Element-by-element motion (every element gets a decision)
- Headlines: line-mask reveal on enter. Optionally scrub word opacity from 20% to 100% across scroll.
- Paragraphs: fade-up by line, y 16 to 24px, stagger 0.03s.
- Eyebrow labels and numbers: slide in from the side while a hairline draws (scaleX 0 to 1).
- Cards: staggered entrance from varied directions. Hover: lift y -6px, tilt up to 6 degrees following the pointer, inner image scale 1.06, accent shift. Press state.
- Images: clip-path inset wipe, inner scale 1.2 to 1, and 8 to 12% parallax inside the frame.
- Buttons: magnetic pull, fill sweep via a translated pseudo-element, arrow nudge, visible focus ring.
- Nav: hides on scroll down, returns on scroll up, active indicator slides between links, compacts after the hero.
- Lists and menus: row hover draws an underline or shows a preview image that follows the cursor.
- Numbers: count up with tabular-nums. SVG strokes draw on scroll.
- Marquees: speed tied to scroll velocity, clamped.
- Section transitions: background color shift or a wipe. No hard cuts. No two adjacent sections reuse the same entrance.
- Footer: giant wordmark reveal.
- Page load: preloader of 1.2s maximum with progress, then the hero sequence.
- Cursor: starts hidden (opacity 0), appears on the first pointermove at the real pointer position. Never render it at 0,0.

## Pinned and stepped sequences: completeness (hard rules)
- Every step has real content in the DOM: a title, one or two sentences, and a visual or number. No empty steps, no placeholder or lorem text, no empty containers.
- Stack all steps in one grid cell. Without JS they read as normal blocks. JS hides non-active steps after init.
- Build the step timeline with explicit fromTo tweens for every step in and out, never .from() that depends on the previous state. Use labels. Make step 1 enter and exit like the others.
- Pin length is steps x 100vh at most. No dead scroll: no stretch longer than 1 viewport where nothing visible changes.
- Progress indicators show the active step and total (for example 02 / 04).
- After building, call ScrollTrigger.refresh() and verify by scrolling to the center of each step.

## 5. Accessibility and fallback
- prefers-reduced-motion: disable pinning, parallax, scrubbing and cursor effects. Keep simple fades.
- Content must be readable with JS animation failing (elements visible by default, hidden only after JS adds a class).

## 6. Final check
- [ ] Only transform/opacity animated in scroll code.
- [ ] One shared ticker for Lenis, GSAP and Three.js.
- [ ] No large backdrop-filter.
- [ ] 5+ distinct scroll effects, including one pinned storyline.
- [ ] 2+ cursor effects, off on touch.
- [ ] Reduced-motion path works.
- [ ] Opened in a browser: scrolling feels smooth, no frame hitching. If it hitches, remove the heaviest effect first.