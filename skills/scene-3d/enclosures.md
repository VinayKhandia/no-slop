# Enclosures: the world is a shape

Required for scene-3d. The camera is INSIDE a closed shape. At least two surfaces (walls, floor, ceiling) must be visible in the hero frame, and the shape must be recognizable in the first screenshot.

## Choose the shape (write choice and reason in DESIGN.md)
- Cube or cuboid room: cafes, galleries, studios, products, interiors. Use BoxGeometry roughly 14x8x14 with a BackSide material. Long cuboid corridor (6x6x40) for journeys and stories.
- Sphere or dome: wellness, music, space, immersive brands. SphereGeometry(30, 64, 48), BackSide, canvas-generated texture or shader.
- Cylinder tunnel: process, transport, sport, speed. CylinderGeometry open-ended, BackSide, UVs scrolling.
- Icosahedron, octahedron or dodecahedron: tech, crystal, abstract. Flat faces in 3 to 4 palette colors, edges lit.
- Torus interior: cycles, subscriptions, loops.
- Half-dome greenhouse or arch alcove: nature, craft, wedding styles.
The style recipe's "3D environment" line suggests a shape. Follow it unless the product clearly needs another.

## Build rules
- Walls are never flat colors. Generate a 1024 to 2048px canvas texture (plaster grain, wood planks, tile grid, panel seams, wallpaper pattern, concrete, paper fibers) and also use it as bumpMap. Set anisotropy and mipmaps.
- Add architecture for scale: baseboard or molding, a window or light panel, shelves or arches or pillars, and at least 5 props sized correctly (lamp, plant, frames, pedestal, stools, shelves of items). Instance repeated props.
- Floor: slightly reflective (roughness 0.25 to 0.4) plus a soft contact shadow under the hero object (radial gradient plane). Real reflections only if frame time stays low.
- Lighting: one warm or colored key through the window or panel, one rim light in a palette color, hemisphere fill, light fog tinted to the wall color. Add 2 to 4 additive light-shaft planes and 200 to 400 dust-mote points.
- Camera FOV 35 to 50. Never let the camera leave the enclosure.
- Enclosure colors come from DESIGN.md. The hero object must be the highest-contrast thing in view.

## Scroll behavior
- Scroll rotates the enclosure or orbits the camera inside it (full turn across the page, plus slow idle drift).
- Every section changes the world: wall material or color lerp via a uniform, a wall panel slides open to reveal the next space, lights change color or intensity, props swap or animate in.
- Keep the hero object anchored to the object zone from DESIGN.md while the world moves around it.
- Smooth all values with the damped scroll value s. No direct jumps.

## Fallback
No WebGL or reduced motion: CSS layered gradient of the same room (two or three skewed panels) as a static background.
