---
name: design-taste
description: Use before building any website, landing page, portfolio or UI. Chooses a concept, a design style that fits the product, palette, type and layout. Prevents generic template output.
---

# Design Taste

Run first for any UI task. Output goes to DESIGN.md (max 70 lines). Then load motion-craft, and scene-3d if 3D applies.

## 1. Concept
- One sentence: the central metaphor plus one signature moment only this product could have.
- If the concept fits any other business, rewrite it.

## 2. Commit to a style (required)
- Pick ONE primary style from the table. A second style may add ONE trait only (example: Editorial with a Swiss grid). The primary must be visibly dominant in the first screenshot.
- Write 2 lines in DESIGN.md on why this style fits the audience and product.
- Open skills/design-taste/styles/<style>.md and follow that recipe literally for palette family, type, layout, motion, 3D environment, cursor and copy tone. Load only that one file.
- Choose the background mode on purpose: light, mid-tone or dark. Dark is right only for Dark luxe, nightlife, cinema and some dev tools. Food, hospitality, wellness, kids, fashion and culture default to light or mid-tone.
- Copy tone follows the style (editorial reads like a magazine, swiss is terse and factual). No lab, telemetry or HUD jargon unless the product is technical.

| Style | Best for | Signature traits |
|---|---|---|
| Editorial | cafes, fashion, magazines, portfolios | huge serif/grotesk headlines, image-text overlap, captions, numbered sections |
| Swiss / International | agencies, tools, architecture | strict grid, flush-left type, 2 colors, big numerals, lots of white |
| Minimalism | premium products, SaaS | one idea per screen, tiny palette, massive spacing, slow motion |
| Maximalism | festivals, music, creative studios | layered textures, clashing type, dense collage, loud color |
| Surreal | art, experiences, perfume, games | impossible scale, floating objects, dreamy gradients, distorted perspective |
| Y2K / Retro-future | youth brands, music, fashion | chrome, bubbles, gradients, pixel/techno type, sticker shapes |
| Glassmorphism | fintech, dashboards, weather, apps | frosted panels over rich color, soft borders, depth (use sparingly, blur is costly) |
| Neo-brutalism | startups, indie tools, edgy brands | thick borders, flat hard shadows, raw type, bold flat color |
| Organic / Tactile | food, wellness, craft, kids | soft shapes, grain, warm tones, clay-like 3D, hand-made feel |
| Dark luxe | watches, cars, spirits, nightlife | near-black base, one metallic accent, cinematic lighting, slow reveals |
| Retro-print / Vintage | bakeries, barbers, breweries | paper texture, stamps, limited ink colors, badges |

Selection rules:
- Match the audience first, trend second.
- Food/drink/hospitality: lean Editorial, Organic/Tactile, Retro-print or Surreal.
- Dev tools/data: Swiss, Minimalism, Neo-brutalism.
- Entertainment/youth: Maximalism, Y2K, Surreal.
- Luxury: Dark luxe, Minimalism.

## 3. Palette
- Start from the palette family in the style recipe, then adapt it to the product's real materials. Max 5 colors with hex and role: background, surface, text, accent, object-contrast.
- The first palette that comes to mind for the industry is banned (coffee: dark brown + orange + cream, fintech: navy + teal, fitness: black + neon). Use the second or third idea.
- The 3D hero is the brightest or most saturated thing against the background. Environment colors come from the same palette.
- About 60% background, 30% surface and text, 10% accent.
- Banned: black background + single orange or blue accent, purple-blue gradients, pure #000 and #fff.
- Text contrast at least 4.5:1. Squint test: you should still see three distinct zones (background, object, text).

## 4. Typography
- One display font and one body font from Google Fonts. Name both.
- Banned as display: Inter, Roboto, Arial, system-ui.
- Display size fluid with clamp(), hero at least 8vw on desktop. Mix scale boldly (tiny labels next to giant headlines).

## 5. Layout
- Asymmetry, overlap, big whitespace or deliberate density (per style).
- Never repeat a three-equal-cards row. Each section uses a different layout idea.
- Content sits over the 3D scene, never in a separate boring block.

## 6. DESIGN.md format
Concept / Signature moment / Style (primary, secondary, why) / Palette table / Fonts / Section list with layout + motion idea per section / zones per section (object side, text side).

## 7. Final check
- [ ] Style chosen with a reason, max two.
- [ ] Palette has no banned defaults.
- [ ] Concept is specific.
- [ ] motion-craft and scene-3d checks also pass (if applicable).
- [ ] Style recipe file was loaded and followed
- [ ] Background mode chosen on purpose