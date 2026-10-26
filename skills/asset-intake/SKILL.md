---
name: asset-intake
description: Use at the start of any UI, 3D or brand build and again when building the hero. Collects the client's real photos, logos, copy and models, and turns them into realistic web assets using a realism ladder, instead of inventing generic shapes that look like AI slop.
---

# Asset Intake

Realism comes from the client's real material. A generated shape will always look generic. Ask for assets first, use them faithfully, and label anything that is not real.

## 1. What to ask for (Gate 0)
Ask for what fits the project, in this priority order:
- Product or place: 1 high-resolution straight-on photo on a plain background (minimum), ideally front, side, back and top, plus 2 to 3 close-ups (cap, label, texture) and 1 lifestyle photo. 2000 px on the long side or more.
- Flat artwork: label or packaging artwork, logo as SVG or PNG with transparency.
- Brand: color hex codes, fonts, tone words, real copy, prices, pack sizes.
- Models: any existing .glb, .gltf or .usdz file.
- Places and cafes: photos of the interior, exterior, menu, signature dishes or drinks.
- Apps and SaaS: real screenshots, logo, pricing, key copy.
- People and portfolios: portraits and project images.
If an item is missing, say how it will be replaced (placeholder or fallback) and what the user can do cheaply to improve it. Never silently invent products, labels or claims.

## 2. Cheap ways for the client to get better assets
- Background removal on a Mac (macOS Ventura or newer): right-click the image in Finder, Quick Actions, Remove Background. Save as PNG.
- Turntable video: put the product on a lazy Susan or any spinning surface, fixed phone on a stack of books or a tripod, plain background, bright even light from a window plus a white card, one slow 360 degree spin. Extract frames: ffmpeg -i spin.mov -vf "fps=24,scale=1280:-2" -q:v 3 frames/f_%03d.jpg
- Glass and shiny objects photograph badly. Use diffuse light, a white card reflection and no direct flash.

## 3. The realism ladder (pick the highest level the assets allow)
Level 1, photo cutout with depth. A transparent PNG or WebP on a PlaneGeometry (MeshStandardMaterial with map, transparent true, alphaTest 0.5). Add pointer tilt (plus or minus 8 degrees), a soft contact shadow plane, a subtle rim highlight, parallax against background layers and light that matches the scene. Honest limit: it is flat, so keep rotations small.
Level 2, turntable sequence. 24 to 72 frames, same framing and light. Load progressively (every 4th frame first, then fill in), draw to a 2D canvas, frame index = round(s * (n - 1)) from the damped scroll value, optional crossfade between neighboring frames. Frames as WebP or JPG at 1280 px wide, about 60 to 120 KB each. Best option for complex shapes (shoes, headphones, devices).
Level 3, real 3D model (.glb). From the client, a designer, or a photo-to-3D or scanning tool (tools such as Polycam, Luma, Meshy or Tripo exist, quality varies). Scans of glass, chrome and thin parts are poor, so inspect them. Clean up in Blender if needed, then compress (gltf-transform with Draco or meshopt, textures to WebP). Hero model budget: under 3 MB and under 100k triangles. Load with GLTFLoader plus DRACOLoader or MeshoptDecoder, normalize scale with Box3, set scene.environment, fix materials (glass becomes MeshPhysicalMaterial with transmission, ior 1.5, thickness).
Level 4, silhouette lathe plus real label. For objects that are round when viewed from the top (perfume bottles, cups, cans, vases, candles): derive the exact profile from a straight-on side cutout and spin it with LatheGeometry. Wrap the real label artwork as a decal on a slightly larger partial CylinderGeometry (thetaLength about 120 degrees, facing the camera). Glass: MeshPhysicalMaterial transmission 1, ior 1.5, thickness, roughness near 0.05, clearcoat. Cap and metal parts: separate lathe meshes with metalness. Check the result against the photo.
Level 5, procedural generic shape. Last resort. Label it PLACEHOLDER everywhere it appears and tell the client what real asset would replace it.
Choosing: round object with one side photo, Level 4, or Level 2 if a turntable exists. Complex object, Level 2 or 3 (Level 1 as a fallback). No photos at all, Level 5 plus a clear request for photos.

## 4. Silhouette to lathe (Level 4)
Use this as a starting point, then test it and adapt.
```js
async function profileFromCutout(url, samples = 96, heightUnits = 2) {
  const img = await new Promise((res, rej) => { const i = new Image(); i.onload = () => res(i); i.onerror = rej; i.src = url; });
  const c = document.createElement('canvas'); c.width = img.width; c.height = img.height;
  const ctx = c.getContext('2d'); ctx.drawImage(img, 0, 0);
  const { data, width, height } = ctx.getImageData(0, 0, c.width, c.height);
  const widths = new Array(height).fill(0);
  let top = -1, bottom = -1;
  for (let y = 0; y < height; y++) {
    let l = -1, r = -1;
    for (let x = 0; x < width; x++) {
      if (data[(y * width + x) * 4 + 3] > 128) { if (l < 0) l = x; r = x; }
    }
    if (l >= 0) { widths[y] = r - l + 1; if (top < 0) top = y; bottom = y; }
  }
  const span = bottom - top;
  const pts = [];
  for (let k = 0; k < samples; k++) {
    const y = Math.round(top + (span * k) / (samples - 1));
    const radius = (widths[y] / 2) * (heightUnits / span);
    pts.push(new THREE.Vector2(Math.max(radius, 0.001), heightUnits / 2 - (heightUnits * k) / (samples - 1)));
  }
  pts.reverse();                                   // LatheGeometry wants bottom to top
  // smooth: moving average of 3 to 5 points on x, keep y
  pts.unshift(new THREE.Vector2(0, pts[0].y));     // close the bottom
  pts.push(new THREE.Vector2(0, pts[pts.length - 1].y)); // close the top
  return pts;
}
```
Rules: the photo must be a straight-on side view without perspective tilt, with a clean alpha mask. Preserve the photo's aspect ratio when scaling. Use at least 96 profile points and 128 radial segments. Compare the rendered silhouette to the photo at 2x zoom and fix any difference over 5 percent in width or height.

## 5. Optimization and organization
- Images: WebP or AVIF, hero at most 250 KB, sequence frames at most 120 KB. Textures at most 2048 px (4096 only for the hero), power of two when possible.
- Folder: assets/images, assets/models, assets/frames, assets/textures, assets/brand.
- assets/README.md manifest: file, what it is, source, license, dimensions, where it is used.
- Never hotlink. Copy assets into the project. Add an attribution line for anything not owned by the client.

## 6. Rules
- Use only assets the client supplied or that are clearly licensed (own, CC0 or equivalent). No third-party logos, product shots or brand imagery unless they are the client's.
- If the tool can generate images, generated imagery may be offered only as moodboard or texture help, labeled as generated, with the client's approval. It never stands in for the client's actual product.
- Update the Assets section of DECISIONS.md: path, status (received, missing, placeholder) and the ladder level used.
- If assets are missing at Gate 4, show what a real photo would change and ask once more. In autopilot, continue with the best available level and flag it.

## 7. Photo fidelity check (Gate 4)
Capture the hero at 2x zoom next to the source photo. Check silhouette, proportions, color, label placement and material feel. List differences and fix the top three before showing the client.

## 8. Final check
- [ ] Assets were requested before the hero was designed.
- [ ] The highest feasible ladder level was used, and its limit stated.
- [ ] Every asset is supplied, licensed or labeled placeholder.
- [ ] Manifest and DECISIONS.md are updated.
- [ ] The photo fidelity check was done.