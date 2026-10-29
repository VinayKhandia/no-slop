# Pattern: scroll world core (one ticker, damped scroll, camera on a path)

Use as the base of every scroll-driven 3D page. Adapt, do not rewrite. Verify that every CDN URL loads, and pin current stable versions.

## HTML
<canvas id="world"></canvas>
<main> sections here </main>
CSS: #world { position: fixed; inset: 0; z-index: 0; pointer-events: none; } main { position: relative; z-index: 1; }

## Libraries
Import map for three (and three/addons/), plain script tags for GSAP, ScrollTrigger and Lenis.

## main.js
````js
import * as THREE from 'three';
gsap.registerPlugin(ScrollTrigger);

const lenis = new Lenis({ lerp: 0.1 });
lenis.on('scroll', ScrollTrigger.update);

const canvas = document.querySelector('#world');
const renderer = new THREE.WebGLRenderer({ canvas, antialias: true });
renderer.setPixelRatio(Math.min(devicePixelRatio, 1.5));
renderer.toneMapping = THREE.ACESFilmicToneMapping;
renderer.outputColorSpace = THREE.SRGBColorSpace;

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(40, 1, 0.1, 200);

function resize() {
  renderer.setSize(innerWidth, innerHeight, false);
  camera.aspect = innerWidth / innerHeight;
  camera.updateProjectionMatrix();
}
addEventListener('resize', resize); resize();

// scroll progress 0..1, smoothed
let target = 0, s = 0;
ScrollTrigger.create({
  trigger: document.body, start: 'top top', end: 'bottom bottom',
  onUpdate: self => { target = self.progress; }
});

// camera and look-at paths (fill with points from STORYBOARD.md)
const camPath  = new THREE.CatmullRomCurve3([ /* Vector3 points */ ]);
const lookPath = new THREE.CatmullRomCurve3([ /* Vector3 points */ ]);
const p = new THREE.Vector3(), l = new THREE.Vector3();   // reused, never allocate per frame

gsap.ticker.add((time, deltaTime) => {
  lenis.raf(time * 1000);                                  // the ONLY loop
  const dt = Math.min(deltaTime / 1000, 0.05);
  s += (target - s) * (1 - Math.exp(-dt * 5));             // damped scroll value
  camPath.getPoint(s, p); lookPath.getPoint(s, l);
  camera.position.copy(p); camera.lookAt(l);
  // update scene state from s here (object transforms, light colors, uniforms)
  if (!document.hidden) renderer.render(scene, camera);
});
gsap.ticker.lagSmoothing(0);
````

## Rules this pattern enforces
- No requestAnimationFrame anywhere else. Everything runs inside gsap.ticker.
- All 3D state derives from the damped value s, never from raw scroll.
- No object creation inside the ticker.
- Text behind the hero object but in front of the room: render the ghost wordmark as a canvas-texture plane inside the scene, between the environment and the object. DOM text can only sit above or below the whole canvas.
- Reduced motion: set s directly from target (no damping), skip parallax and scrub, keep fades.
- Pause or lower quality when document.hidden, and drop pixel ratio further when navigator.hardwareConcurrency <= 4.