# Glassmorphism style recipe

Best for: fintech apps, modern dashboards, smart home controls, premium weather apps.

## Palette family
Luminous multi-hue backdrop glow, translucent frosted surfaces, crisp bright text. Adapt, do not copy:
- Deep twilight #0B1021, luminous cyan #00D4FF, violet glow #7928CA, frosted tint #FFFFFF15
- Obsidian blue #080D1A, emerald pulse #00F5A0, ocean blue #0070F3, ice surface #FFFFFF1A
- Dark slate #0F172A, aurora rose #F43F5E, amber neon #F59E0B, frosted glass #FFFFFF20

## Type
Modern ultra-clean geometric sans (Plus Jakarta Sans, Manrope, Space Grotesk). Crisp high-legibility numerals with tabular-nums. Medium weight labels, subtle letter-spaced uppercase captions.

## Layout
Layered floating cards with 1px translucent borders (rgba(255,255,255,0.12)). Limit backdrop-filter blur strictly to one or two small priority panels for 60fps performance; use pre-rendered translucent tints elsewhere.

## Motion
Smooth elevation lifts on hover (translateY -4px), soft specular light sweep along card edges on mousemove, subtle depth parallax between glass layers, fluid gradient background shift.

## 3D environment
Deep rich colored atmosphere with soft floating refractive crystals or frosted translucent geometric lenses, 2 soft contrasting point lights creating iridescent rim refractions on the hero.

## Cursor
Smooth diffused glowing dot with a soft translucent frosted ring lagging behind via lerp.

## Copy tone
Precision-oriented, crisp, transparent. Clear metrics, status indicators, and confident summaries.

## Avoid
Heavy backdrop-filter on large full-screen containers, flat opaque dull cards, cluttered high-contrast borders, retro textured grain.
