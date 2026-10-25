---
name: storyboard
description: Use before building any immersive, 3D or motion-heavy site. Plans the page like a short film (scenes, camera moves, transitions, pacing, one signature moment) so the result feels directed instead of assembled from sections.
---

# Storyboard

Sites feel generic when they are a stack of sections. Wow comes from a directed sequence. Write STORYBOARD.md before any code.

## 1. The signature moment (exactly one)
The one thing a visitor will describe to a friend. It must be specific to this product, driven by scroll or interaction, and doable at 60fps. Examples: scrolling pours the cup and the liquid level is the progress bar; the camera flies through a perfume bottle's glass into the next scene; the page descends through depth zones with a live depth meter; headline letters assemble into the product; the object explodes into parts with spec callouts and reassembles.
Write: "Signature: <what>. Mechanism: <what scroll drives, what the visitor sees, what changes>."

## 2. Structure
Pick one archetype and say why: Descent, Turntable, Walk-through, Shelf, Type storm, Focus tour, Portal chain.

## 3. Shot list (5 to 8 scenes)
For every scene write:
- Name and length in viewports of scroll
- Camera: position, move, FOV
- Hero object state and environment or light change
- Text beat: the final headline and supporting line, plus its screen zone
- Entry transition and exit transition
- Interaction available
- Intensity: calm, build, peak or release

## 4. Pacing
Calm opening, build, one PEAK (the signature, placed at 55 to 70 percent of the scroll), release, then a clear call to action. Never two peaks in a row. One focal point per scene. First interaction available within one second.

## 5. Transition toolkit (different type at each boundary, at most 3 types per page)
- Camera fly-through: the camera path continues into the next environment, with fog or shared geometry hiding the join.
- Shader dissolve or wipe: render two scenes to render targets and mix them with a progress uniform and a noise threshold.
- Clip-path portal: a circle or shape expands from the hero object into the next scene.
- Object morph: the hero changes variant or deforms while the environment shifts.
- Depth-sandwich shift: the ghost wordmark scales past the camera as the next scene emerges.
- Pinned scrub: one viewport changes state across scroll, with a step indicator.
- Color wash: background and light lerp through a palette midpoint.
- Focus pull: depth of field or blur shifts from one layer to another.
- Scale-through: zoom into a detail that becomes the whole next frame.
For each boundary write: type, scroll range, duration and ease, and the CONTINUITY ELEMENT, something that stays on screen across the cut so scenes feel connected.

## 6. Copy
Final headlines, no placeholders. Maximum 12 words per headline. Voice follows the style. No jargon unless the product is technical.

## 7. Output: STORYBOARD.md
Signature and mechanism, archetype, shot-list table, transition map, a one-line intensity curve (for example calm, build, build, PEAK, release, close), asset list (models, textures, images, with a fallback for each), performance budget per scene.

## 8. Final check
- [ ] One signature moment with a clear mechanism.
- [ ] 5 to 8 scenes, each with camera, text, entry and exit transition.
- [ ] Every boundary has a continuity element.
- [ ] Exactly one peak.
- [ ] Copy is final, assets have fallbacks.