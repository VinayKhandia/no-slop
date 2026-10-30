# Cursor Library

A collection of 12 distinct cursor behaviors. Choose a cursor that reinforces the concept and matches the design style.

## 1. Magnetic dot with trailing ring
- Behavior: A solid core dot locks onto pointer and interactive elements while an outer ring follows smoothly with lag.
- How to build: Fixed container with pointer-events none; inner dot translates directly to pointer coords; outer ring lerps position (factor 0.15); over buttons, the dot springs toward the element center with damped velocity.
- Best-fit styles: Swiss / International, Minimalism, Editorial.

## 2. Blend-mode invert circle
- Behavior: A high-contrast circle that inverts background and text colors underneath, scaling up over links and interactive elements.
- How to build: Fixed circular div with mix-blend-mode difference and background #ffffff; centered via transform translate(-50%, -50%); scale tweens from 1 to 2.5 on pointerenter of interactive tags.
- Best-fit styles: Editorial, Neo-brutalism, Dark luxe.

## 3. Text label follower ("View", "Drag")
- Behavior: A pill badge showing contextual action text ("View", "Drag", "Explore") that hovers beside the pointer over interactive zones.
- How to build: Position fixed pill with palette accent background; opacity 0 by default; on hovering cards or media containers, update textContent, scale from 0 to 1, and offset x/y by 16px from pointer.
- Best-fit styles: Editorial, Dark luxe, Surreal.

## 4. Spotlight/flashlight reveal
- Behavior: A radial gradient mask centered on the pointer revealing an illuminated layer or texture beneath a darker foreground.
- How to build: Track pointer coordinates in CSS custom properties (--cursor-x, --cursor-y); foreground layer uses background radial-gradient(circle 180px at var(--cursor-x) var(--cursor-y), transparent 0%, rgba(0,0,0,0.85) 100%) or mask-image.
- Best-fit styles: Dark luxe, Surreal, Y2K / Retro-future.

## 5. Liquid blob (SVG goo filter)
- Behavior: An organic fluid drop that stretches, wobbles, and merges with satellite drops as the pointer accelerates.
- How to build: SVG filter with feGaussianBlur (stdDeviation 8 to 12) and feColorMatrix (values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -9"); trailing divs lag behind pointer coords inside the filtered container.
- Best-fit styles: Organic / Tactile, Surreal, Maximalism.

## 6. Crosshair with coordinates (technical)
- Behavior: Fine hairline crosshair spanning screen axes with live numeric coordinate readout and HUD framing brackets.
- How to build: Fixed hairline divs for horizontal and vertical axes; small label span showing tabular-nums X and Y client coordinates; coordinates snap or highlight on hoverable data items.
- Best-fit styles: Swiss / International, Neo-brutalism.

## 7. Particle trail
- Behavior: A stream of fading spark or dust motes emitted along the pointer vector that decay and drift over time.
- How to build: Lightweight full-screen canvas with pointer-events none; push {x, y, vx, vy, life} on pointermove up to max 25 particles; animation frame updates positions, reduces life, and fades alpha; stops RAF when idle.
- Best-fit styles: Surreal, Y2K / Retro-future, Maximalism.

## 8. Lens/magnifier
- Behavior: Circular glass pane with subtle chromatic aberration or optical zoom distorting the content underneath.
- How to build: Fixed circular container with border and subtle drop shadow; renders a secondary scaled canvas crop or CSS transform scale(1.2) of target media aligned with inverted relative coordinates.
- Best-fit styles: Editorial, Retro-print / Vintage, Dark luxe.

## 9. Morphing shape that matches hovered element
- Behavior: Cursor smoothly expands, squares off, and snaps to the exact bounding box and border-radius of whatever element is hovered.
- How to build: Single fixed div with transitions on transform, width, height, and border-radius; on pointerenter of nav or card targets, call getBoundingClientRect once and match target size, position, and radius.
- Best-fit styles: Glassmorphism, Minimalism, Swiss / International.

## 10. Custom emoji/object follower
- Behavior: A miniature 3D sprite, vector stamp, or themed product glyph that floats and rotates with movement inertia.
- How to build: Fixed div containing inline SVG or canvas sprite; calculate delta movement angle via Math.atan2(dy, dx) and lerp rotation toward movement vector; trigger a spring scale punch on click.
- Best-fit styles: Retro-print / Vintage, Organic / Tactile, Y2K / Retro-future.

## 11. Velocity-stretch ellipse
- Behavior: A circle that squashes and stretches into an elongated ellipse oriented along the direction and velocity of pointer movement.
- How to build: Calculate instantaneous pointer velocity hypot(dx, dy) and angle atan2(dy, dx); map clamped speed to scaleX(1 + speed * 0.003) and scaleY(1 / (1 + speed * 0.003)); rotate(angle) and lerp back to 1 on slow down.
- Best-fit styles: Neo-brutalism, Maximalism, Y2K / Retro-future.

## 12. Ripple on click
- Behavior: An expanding concentric shockwave ring emanating from the click coordinate that dissolves outward.
- How to build: On pointerdown, spawn or reuse a pooled circular span at click coordinates; animate transform scale from 0.2 to 2.4 and opacity from 0.8 to 0 over 450ms; remove from DOM or reset pool on complete.
- Best-fit styles: Glassmorphism, Minimalism, Organic / Tactile.

## Rules

1. Pick the cursor from the brief and style. Never default to the same one.
2. Never reuse the cursor recorded as cursor: in the previous project's DECISIONS.md or the last build in this workspace.
3. At Gate 3, show 3 cursor options as a live previews/cursors.html and ask the client to pick; record cursor: <name> in DECISIONS.md.
4. Disable custom cursor on touch devices and when prefers-reduced-motion is set.
