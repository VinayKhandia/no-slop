# Realism recipe for procedural hero objects

Read before building the hero object. Goal: reads as a product render, not a diagram.

## Renderer and light
- renderer.toneMapping = ACESFilmicToneMapping, toneMappingExposure about 1.0, outputColorSpace = SRGBColorSpace.
- Reflections must match the room: build a PMREMGenerator environment from the enclosure scene (or RoomEnvironment as fallback) and assign scene.environment. envMapIntensity 0.8 to 1.2.
- One shadow-casting directional or spot light, shadow map 2048, PCFSoftShadowMap, tight shadow camera bounds, bias tuned. Hero object casts, floor receives. Add a soft contact shadow plane too. Nothing floats without a shadow.
- Never use flatShading. Call computeVertexNormals() after building geometry.

## Ceramic (cups, plates, vases)
- MeshPhysicalMaterial: roughness 0.18 to 0.3, clearcoat 1, clearcoatRoughness 0.08 to 0.15, sheen 0.2. Add a canvas noise roughnessMap and bumpMap (very subtle) for uneven glaze.
- Correct proportions: cappuccino cup height about 0.6 of rim diameter, wall about 3 to 4% of diameter, rolled rim (rounded top), foot ring, visible concave interior. Profile from a spline with 40+ points, 128 radial segments.
- Saucer is opaque ceramic with a shallow well and rolled rim, same material as the cup. Never translucent.
- Handle: TubeGeometry along an elliptical CatmullRomCurve3 (64+ tube segments, 12+ radial), ends buried inside the wall, tapering is welcome.
- Slight asymmetric imperfection (tiny scale or rotation variation) beats perfect symmetry.

## Liquid
- Surface sits 6 to 10% of cup height below the rim, a high-resolution circle (64x64) with gentle two-sine vertex ripple. Drag or pointer movement adds slosh with damping.
- Meniscus: a thin brighter ring where liquid meets the wall (radial gradient or thin torus).
- Surface material MeshPhysicalMaterial, clearcoat 1, roughness 0.1 to 0.15. Color from a radial canvas texture: darker center, lighter caramel rim, noise swirl, tiny bubbles near the edge. For latte art, draw the pattern into that canvas.
- Optional: inner wall darker below the liquid line.

## Steam, particles and props
- Steam: 40 to 80 soft sprites (canvas radial gradient, opacity 0.08 to 0.2), rising with noise drift, expanding and fading. Normal blending, not additive white blobs.
- Coffee beans: displaced sphere with a center groove, InstancedMesh with per-instance color and scale variation, they cast and receive shadows.
- Depth cue: fog plus a slightly different scale and blur-like fade for far props.

## Optional model path
If an assets/ folder contains a .glb or .gltf, use GLTFLoader (plus DRACOLoader when compressed) for the hero instead of procedural geometry. Normalize scale with Box3, apply scene.environment, enable shadows, and keep procedural liquid, steam and particles. Never download or hotlink models. In the README, tell users to put licensed or CC0 models in assets/.

## Self-check (look at a 2x zoom screenshot)
- [ ] Reflections of the room are visible on the glaze.
- [ ] Contact shadow grounds the object.
- [ ] Rim is rounded and catches a highlight.
- [ ] Liquid is below the rim with a visible meniscus.
- [ ] No faceting on any curve, no translucent ceramic.
