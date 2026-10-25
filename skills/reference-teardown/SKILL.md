---
name: reference-teardown
description: Use when the user provides reference images, screenshots or URLs of sites they like. Breaks each reference into concrete reusable design and motion rules, never copying code, text or brand assets, and binds those rules to the brief and storyboard.
---

# Reference Teardown

References only help if they become rules. Write REFERENCES.md before DESIGN.md and STORYBOARD.md.

## 1. Inventory
List every reference. For URLs, open them with browser tools if available and capture frames at several scroll points. If only still images exist, say what stills cannot show (motion, transitions) and ask for a screen recording or a short description of the motion.

## 2. Teardown (one block per reference)
- What it is, and why it works, one line each
- Layout and composition: grid, zones, depth layers (ghost wordmark behind the object, copy at the edges), scale contrast
- Typography: roles, pairing, approximate size ratios, case
- Color and light: approximate palette with hex, light direction, atmosphere
- 3D hero: object, materials, camera, interaction hints and labels
- Motion and transitions: what scrolls or pins, how scenes change, which technique likely makes it
- UI chrome: HUD elements, meters, callouts, scrubbers, thumbnails
- The signature mechanic
- Reuse and avoid: principles to reuse; things never to copy (logos, brand names, copy, illustrations, licensed images, paid source code)

## 3. Reference DNA
Merge all teardowns into 5 to 8 prioritized rules, each noting which references support it. If references conflict, the user's stated priority wins.

## 4. Bind
Put the DNA into DESIGN.md and STORYBOARD.md. Choose an archetype, style and effects consistent with it. If a reference depends on assets we do not have, list substitutes.

## 5. Originality
Reuse mechanics, not identity. Never reproduce a reference's layout, copy or brand one to one. New concept, new composition, new copy.

## 6. Verify
In visual-qa, check screenshots against the DNA rules as a checklist, not against pixels.