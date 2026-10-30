# Motion Kit

Menus of motion options for interface elements. Every element in the experience must have an intentional motion behavior.

## Text Animation

### Split-line reveal
Lines mask upward from an overflow-hidden wrapper with staggered easing.

### Per-letter stagger
Individual characters animate in sequentially with subtle Y-translation and opacity.

### Scramble/decode
Characters cycle through randomized glyphs before settling on the target text.

### Blur-in
Text transitions from high Gaussian blur and reduced opacity into sharp focus.

### Scroll-scrubbed highlight
Text color fills or brightens progressively linked directly to scroll progress.

### Variable-font weight shift
Font weight and optical size dynamically interpolate on scroll or hover.

## Card Animation

### Tilt/3D hover
Card rotates in 3D perspective based on relative pointer position within its bounds.

### Stack and fan-out
Cards layered in a stack spread into an arched fan layout on scroll or hover.

### Parallax layers
Internal image, text, and floating accents translate at differential speeds on movement.

### Flip
Card performs a 3D Y-axis rotation revealing a detailed reverse face on trigger.

### Magnetic
Entire card pulls smoothly toward the pointer with damped spring physics on hover.

### Spotlight border
Border or outline gradient tracks pointer coordinates via a radial mask.

## Button Animation

### Magnetic
Button core displaces toward the pointer with spring tension while hovering near it.

### Fill sweep
Background color sweeps across the button area from the entry angle of the pointer.

### Liquid
Fluid blob shape morphs and distorts within the button boundary on interaction.

### Arrow slide
Accompanying icon or arrow slides out of frame and loops in from the opposite side.

### Ripple
Concentric shockwave ring expands outward from click coordinates across the button face.

### Text swap
Current button label slides vertically out as a secondary label slides in.

## Environment Animation

### Helix/spring room
3D scene elements arranged in a vertical spiral that coils and compresses on scroll.

### Rotating cube room
Background space formed by an inverted cube whose faces rotate on axis changes.

### Particle field
Floating constellation of points or motes that drift and react to camera motion.

### Floating shapes
Geometric or organic primitives that bob and rotate with subtle independent physics.

### Fog depth tunnel
Infinite camera travel through volumetric layered atmospheric mist or rings.

### Shader gradient
WebGL fragment shader rendering smooth, slowly shifting chromatic noise fields.

## Page Transitions

### Curtain wipe
Full-viewport color slab slides across the screen to conceal the outgoing view and reveal the incoming view.

### Clip-path morph
Viewport unmasks through an expanding geometric clip-path polygon or expanding circle.

### Shared-element
Hero image or card seamlessly expands and animates into the destination layout container.

### Zoom-through
Camera pushes past the outgoing screen content into the depth of the new scene.

### Directional push
Outgoing and incoming views translate synchronously along the navigation axis with easing.

## Rules

Element-by-element rule: every text block, card, button and environment gets a chosen animation. Nothing is static.
