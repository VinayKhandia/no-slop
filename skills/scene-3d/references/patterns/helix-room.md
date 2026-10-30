# Pattern: helix room (spiral camera path inside rotating enclosure)

An environment where the camera travels along a helix inside a box or cylinder while the room slowly rotates, like being inside a spring.

## Structure & Geometry

- **Room**: BoxGeometry or CylinderGeometry with `THREE.BackSide` material. Add architectural ribs or rings along the enclosure walls for scale and parallax.
- **Spring**: TubeGeometry generated along a custom `THREE.Curve` helix.
- **Hero Object**: Anchored at the helix axis (center line `[0, y, 0]`), revealed as the camera spirals inward along the path.

## Camera Path & Mathematics

- Progress parameter `p` (0 to 1) comes from the damped scroll value (see [fluid-scroll.md](file:///Users/vinaykhandia/projects/no-slop/skills/scene-3d/references/patterns/fluid-scroll.md)).
- Helix formula:
  - `angle = p * turns * Math.PI * 2`
  - `pos = (R * Math.cos(angle), y0 + p * height, R * Math.sin(angle))`
- Camera orientation: `camera.lookAt()` evaluates the point at `p + 0.02` on the same helix so the camera points forward along the curved travel path.
- Enclosure rotation: `room.rotation.y = baseIdleRotation + dampedScrollVelocity * 0.1`.

## Depth & Lighting

- **Fog**: Tinted to match the enclosure background palette, adding atmospheric density and masking distant geometry boundaries.
- **Point light**: Positioned to travel synchronously with the camera, casting moving highlights along walls and ribs.
- **Emissive rim**: Emissive color and intensity on the spring TubeGeometry material for edge luminescence.

## Minimal Three.js Implementation

```js
import * as THREE from 'three';

// 1. Custom Helix Curve
class HelixCurve extends THREE.Curve {
  constructor(radius = 6, height = 24, turns = 3, y0 = -12) {
    super();
    this.radius = radius;
    this.height = height;
    this.turns = turns;
    this.y0 = y0;
  }
  getPoint(t, optionalTarget = new THREE.Vector3()) {
    const angle = t * this.turns * Math.PI * 2;
    const x = this.radius * Math.cos(angle);
    const y = this.y0 + t * this.height;
    const z = this.radius * Math.sin(angle);
    return optionalTarget.set(x, y, z);
  }
}

// 2. Room & Geometry Setup
const roomGroup = new THREE.Group();
scene.add(roomGroup);

// Enclosure with BackSide material
const roomGeo = new THREE.CylinderGeometry(10, 10, 32, 32, 1, true);
const roomMat = new THREE.MeshStandardMaterial({
  color: 0x111116,
  side: THREE.BackSide,
  roughness: 0.6
});
const room = new THREE.Mesh(roomGeo, roomMat);
roomGroup.add(room);

// Spring along the helix curve
const helixCurve = new HelixCurve(7, 24, 3, -12);
const springGeo = new THREE.TubeGeometry(helixCurve, 200, 0.25, 12, false);
const springMat = new THREE.MeshStandardMaterial({
  color: 0x333344,
  emissive: 0x5566ff,
  emissiveIntensity: 0.6,
  roughness: 0.3
});
const spring = new THREE.Mesh(springGeo, springMat);
roomGroup.add(spring);

// Architectural ribs along enclosure walls
for (let i = 0; i < 8; i++) {
  const ringGeo = new THREE.TorusGeometry(9.9, 0.08, 8, 48);
  const ringMat = new THREE.MeshBasicMaterial({ color: 0x222230 });
  const ring = new THREE.Mesh(ringGeo, ringMat);
  ring.rotation.x = Math.PI / 2;
  ring.position.y = -12 + (i / 7) * 24;
  roomGroup.add(ring);
}

// Hero object anchored at the helix axis
const heroGeo = new THREE.IcosahedronGeometry(2, 2);
const heroMat = new THREE.MeshStandardMaterial({ color: 0xffffff, metalness: 0.8, roughness: 0.2 });
const hero = new THREE.Mesh(heroGeo, heroMat);
hero.position.set(0, 0, 0);
scene.add(hero);

// Depth elements: fog and camera-tracking point light
scene.fog = new THREE.FogExp2(0x0a0a0f, 0.04);
const camLight = new THREE.PointLight(0xffffff, 25, 18);
scene.add(camLight);

// 3. Update in ticker loop (p from fluid-scroll.md, dt in seconds)
let idleAngle = 0;
function updateHelixRoom(p, vel, dt) {
  // Camera travels along helix path looking ahead
  const camPos = helixCurve.getPoint(p);
  const lookTarget = helixCurve.getPoint(Math.min(p + 0.02, 1));
  camera.position.copy(camPos);
  camera.lookAt(lookTarget);
  camLight.position.copy(camPos);

  // Enclosure rotates with idle drift + damped scroll velocity
  idleAngle += dt * 0.15;
  roomGroup.rotation.y = idleAngle + vel * 0.1;

  // Hero object revealed as camera spirals in
  hero.rotation.y += dt * 0.4;
}
```

## Quality Assurance (QA)

- Capture frames at `p = 0`, `0.25`, `0.5`, `0.75`, and `1`.
- Inspect frames to verify no clipping through enclosure walls, ribs, or the spring tube.
