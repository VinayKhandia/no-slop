---
name: visual-qa
description: Use after building any UI. Opens the page, captures screenshots at several scroll positions and sizes, and fixes overlap, readability, rough 3D and layout problems before reporting done.
---

# Visual QA

Run after the build and before the reviewer. Code that reads fine often looks wrong. Look at the real page.

## 1. Capture
- Serve locally: python3 -m http.server 8080. Use the built-in browser if available. If you cannot take screenshots, ask the user to send them and stop until they arrive.
- Screenshots at scroll 0%, 15%, 30%, 50%, 70%, 90%, 100% at 1440x900, and again at 390x844.
- Also capture one card hover, one button hover, and the cursor at screen center.
- Use Playwright with headless Chromium (npx playwright install chromium if missing) in a script at .qa/shots.js. Save screenshots to .qa/. Add .qa/ to .gitignore.
- For every pinned or stepped sequence, capture the center of EACH step and confirm that step's copy is visible. A blank step is a failed round.
- Dead-scroll sweep: scroll the whole page in 10% increments and flag any viewport with fewer than 3 visible content elements or no visible motion.
- Hero zoom: one screenshot at deviceScaleFactor 2 cropped on the hero object for the realism self-check in skills/scene-3d/realism.md.
- Enclosure check: at least two surfaces of the enclosure are visible in the hero screenshot and the shape can be named.

## 2. Inspect every screenshot
- Text over 3D: no body text, button or small label sits on the 3D object or on a busy area. At most one large display line may overlap the object, deliberately, with the object in front.
- Contrast: all text readable at a glance. If not, move it, add a calm surface behind it, or change colors.
- 3D quality: no jagged or faceted curves, no gaps or open edges, no clipping between objects, nothing cropped by accident.
- Realism: ceramic and liquid pass the self-check. Fix before reporting.
- Environment: describable in one sentence from the first screenshot. If barely visible, strengthen it.
- Composition: one clear focal point per screen, balanced whitespace.
- Cursor: hidden until the first pointer move, never parked in a corner.
- Style: still matches the style chosen in DESIGN.md. If it looks like generic dark mode with an accent color, fix it.
- Mobile: no horizontal scroll, no clipped text, 3D scaled down.
- Smoothness: scroll slowly and fast. If frames drop, remove the heaviest effect first.

## 3. Fix loop
List each issue as: screenshot, problem, fix. Apply fixes as minimal diffs. Re-capture the affected screenshots. Maximum 3 rounds, then report what remains.

## 4. Report
One line per round: issues found, issues fixed. Never claim a pass without having looked at the screenshots.

## Motion QA (screenshots cannot judge motion)

Static screenshots miss transitions, jank and dead scroll. Also do this:

1. Scripted scroll run. In Playwright load the page, then scroll from 0 to 100 percent with many small page.mouse.wheel steps and short waits (about 20 seconds total, so Lenis behaves like a real user). Save a frame every 250 ms to .qa/frames/. Look at the frames in order (tile them into contact sheets with sharp or Pillow if helpful).
2. Frame-time measurement, in a separate run with no screenshots:
   await page.evaluate(() => { window.__dt = []; let last = performance.now(); const f = n => { window.__dt.push(n - last); last = n; requestAnimationFrame(f); }; requestAnimationFrame(f); });
   Run the scroll, read window.__dt, sort it, and report median, p95 and the count of frames over 33 ms. Headless Chromium renders WebGL in software, so absolute numbers are pessimistic. Use them to compare changes and to catch p95 above 100 ms or sudden spikes, and tell the user that real smoothness must be checked by a human in a real browser.
3. Transition inspection. For every boundary in STORYBOARD.md capture 6 frames across its scroll range. In each frame the continuity element must be visible and nothing may be blank, broken or clipped.
4. Dead-scroll detection. Flag any stretch longer than 1.5 viewports where consecutive frames differ by under 2 percent.
5. Console: zero errors and zero failed network requests.

## Wow rubric (score honestly, 0 to 5 each)
1. Signature moment present and memorable
2. 3D quality: materials, light, shadows, proportions
3. Transitions: continuity, purpose, smoothness
4. Typography and layout: scale contrast, hierarchy, text and 3D in separate zones
5. Motion quality: easing, timing, stagger, no jank
6. Color and light: cohesive, atmospheric, readable
7. Interaction delight: cursor, drag, hover, feedback
8. Polish: loading, responsive, real copy, no console errors

Rule: average must be at least 4 and no category below 3. List the three weakest categories with screenshot or frame names as evidence. Do not praise. If it fails, run a Wow Pass.

## Wow Pass (maximum 2)
Pick the three weakest categories. Add three unexpected delights that fit the concept (a cursor-driven light, a hover reveal, a hidden interaction, a micro-transition between states). Apply them as minimal diffs, re-run Motion QA and the rubric, and report the new scores.