# Pattern: fluid scroll (layered critical damping)

- Why: raw or single-lerp scroll feels robotic. Use a critically damped spring per layer.
- Code (JS):
```js
function smoothDamp(cur, target, vel, smoothTime, dt){
  const omega = 2 / smoothTime, x = omega * dt;
  const e = 1 / (1 + x + 0.48*x*x + 0.235*x*x*x);
  const change = cur - target;
  const temp = (vel.v + omega * change) * dt;
  vel.v = (vel.v - omega * temp) * e;
  return target + (change + temp) * e;
}
```
- Layered lag: keep separate damped values with different smoothTime: camera 0.35, object rotation 0.55, background/environment 0.9, text 0.2, so layers settle at different moments.
- Drive everything from ONE gsap.ticker loop with Lenis; pass dt in seconds, clamp dt to 0.05.
- Overlap scene ranges by 10 to 15 percent; no hard-ranged states; use smoothstep to blend between scenes.
- Idle drift: when scroll velocity is near 0, add slow sine motion to camera and objects so the scene never freezes.
- Respect prefers-reduced-motion by raising smoothTimes and disabling drift.
- QA: record frame times with Playwright; no frame over 33ms during scroll.
