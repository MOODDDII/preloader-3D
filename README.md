# 3D Preloader (Three.js Wireframe Sphere)

A lightweight, dependency-free 3D preloader/loading animation built with **Three.js**. It renders a rotating wireframe sphere on a transparent `<canvas>` that fills the entire browser window, making it easy to drop into any page as a loading screen.

## Demo - [Demo Link](https://moodddii.github.io/preloader-3D/)

Open `index.html` in a browser (with `three.js` in the same folder) to see a slowly rotating wireframe sphere centered on the screen.

## Features

- Full-screen, transparent canvas background
- Wireframe sphere rendered with `MeshNormalMaterial`
- Smooth continuous rotation via `requestAnimationFrame`
- Automatically resizes with the browser window
- No external dependencies besides `three.js`

## Project Structure

```
.
├── index.html      # Main HTML file with embedded JS
├── three.js        # Three.js library (must be included locally)
└── 3d_sphere.png   # Favicon
```

## Getting Started

1. Clone or download this repository.
2. Make sure `three.js` is present in the project root (download it from the [Three.js releases](https://github.com/mrdoob/three.js/) if missing).
3. Open `index.html` in your browser — no build step or server required.

## How It Works

- A `THREE.Scene`, `THREE.PerspectiveCamera`, and `THREE.WebGLRenderer` are created and attached to the `#canv` canvas element.
- `renderer.setClearColor(0x00000)` combined with `alpha: true` keeps the background transparent, so the preloader can sit on top of any page content.
- An `AmbientLight` evenly illuminates the scene.
- A `SphereGeometry` (radius `160`, `18x18` segments) is wrapped in a wireframe `MeshNormalMaterial` to create the signature faceted look.
- The `render()` function rotates the sphere on its Y axis every frame and calls itself recursively via `requestAnimationFrame` for smooth animation.
- A `resize` event listener keeps the camera aspect ratio and renderer size in sync with the window.

## Customization

| What to change | Where |
|---|---|
| Sphere size | `THREE.SphereGeometry(160, 18, 18)` — first argument is radius, next two are width/height segments |
| Rotation speed | `mesh.rotation.y += Math.PI / 320` — decrease the divisor to speed up |
| Camera distance/FOV | `camera.position.set(0, 0, 800)` and `new THREE.PerspectiveCamera(52, ...)` |
| Wireframe color | Swap `MeshNormalMaterial` for `MeshBasicMaterial({ color: 0xffffff, wireframe: true })` |
| Background color | `renderer.setClearColor(0x00000)` (note: currently missing 2 digits — should be a full 6-digit hex like `0x000000`) |

## Browser Support

Requires a browser with WebGL support. All modern browsers (Chrome, Firefox, Edge, Safari) are supported.

## License

No license specified in the source repository — check with the repository owner before reuse in commercial projects.
