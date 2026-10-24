# AEGIS Bio-Node

**Concept study: Modular Gyroid Perfusion Bioreactor with Optical Sensor Docking Interfaces**

AEGIS Bio-Node is a browser-based, interactive engineering concept viewer. It is intended for communicating a proposed modular perfusion-reactor assembly and exploring a mathematical gyroid level-set preview. It is **not** a validated bioreactor, manufacturing-ready CAD package, CFD solver, or experimentally verified design.

## Live prototype

[Open AEGIS Bio-Node on GitHub Pages](https://meenavignesh-svg.github.io/AEGIS-BIO-NODE/)

The website is a static frontend. Three.js and OrbitControls are loaded from jsDelivr using browser ES modules/import maps; no Node.js runtime, database, private server, or local development server is required after deployment. An internet connection is required for the CDN-hosted Three.js modules.

## Current interactive features

- Procedural 3D assembly with a transparent concept chamber, end collars, clamp/fastener details, inlet/outlet unions, support saddles, and four proposed optical docking locations.
- Procedural sampled gyroid level-set preview with adjustable cell count, threshold, and preview resolution.
- Solid, wireframe, X-ray, and core-only views (keyboard shortcuts **1–4**).
- Orbit, zoom and pan; Focus model, Reset view, Explode/restore, X-ray toggle, and fullscreen controls.
- Component visibility toggles and chamber opacity adjustment.
- In-browser reference calculations and a pressure-drop-versus-flow chart for a straight circular tube.
- Responsive layout and a WebGL startup error message.

## Engineering calculations and limitations

Inputs use SI units internally. The interface calculates:

- Cross-sectional area: (A=\pi D^2/4)
- Mean velocity: (v=Q/A)
- Reynolds number: (Re=\rho vD/\mu)
- Nominal tube residence time: (t=AL/Q)
- Straight-tube pressure drop: \(\Delta P=128\mu LQ/(\pi D^4)\), from Hagen–Poiseuille flow.

The pressure-drop relation assumes steady, fully developed laminar flow of a Newtonian fluid through a straight circular tube. The interface does not apply it as a prediction for the gyroid. It does not calculate gyroid wall shear, pressure fields, porosity, surface-area-to-volume ratio, oxygen transfer, or residence-time distributions.

The animated points are visual flow markers only, not a computed flow field. No CFD, experimental, sensor-calibration, sterility, or performance data are currently included. No percentage performance claims should be inferred from the concept.

## Geometry interpretation

The core is a sampled pair of gyroid level surfaces at \(g=\pm t\), based on:

\[
g(x,y,z)=\sin(x)\cos(y)+\sin(y)\cos(z)+\sin(z)\cos(x)
\]

This is a visual mathematical level-set preview, not a robustly thickened, watertight, parametric, or print-ready solid. The threshold is dimensionless. Mesh resolution trades detail for browser performance. No validated porosity or solid fraction is reported.

The dimensions, material appearances, docking interfaces, fasteners, seals, and port arrangements are provisional visual concepts. The metallic finish does not certify a specific alloy. Sensor interfaces are proposed—not tested optical sensors.

## Run locally

Because the app uses JavaScript modules, open it through a local static HTTP server for development (not by double-clicking the HTML file). For example, with Python installed:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000/AEGIS-BIO-NODE/` if serving the parent folder, or `http://localhost:8000/` if serving the repository directory itself. The deployed site does not require Python.

## GitHub Pages deployment

This repository uses a single root-level `index.html` and no build step.

1. Push the desired commit to the repository's `main` branch.
2. Open **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select branch `main` and folder `/(root)`, then save.
5. Wait for the Pages deployment to finish, then open [the published site](https://meenavignesh-svg.github.io/AEGIS-BIO-NODE/).

The page uses no root-relative local asset paths, so the repository subpath is supported. Three.js imports are CDN URLs. Confirm the published page and browser console after each change; a successful GitHub commit alone does not prove the deployment is healthy.

## Validation still required before engineering use

A research/manufacturing design would need dimensioned parametric CAD and tolerances, mesh-quality checks, validated seals and pressure boundaries, material compatibility and sterilisation evidence, sensor calibration, flow-loop experiments, and CFD from a documented external solver with mesh/time-step independence and suitable boundary conditions. The static GitHub Pages app is not a CFD backend.

## Libraries and attribution

- [Three.js](https://threejs.org/) — browser-based 3D rendering.
- [OrbitControls](https://threejs.org/docs/#examples/en/controls/OrbitControls) — camera orbit, zoom and pan.
- [jsDelivr](https://www.jsdelivr.com/) — CDN delivery of Three.js ES modules.

Third-party library licensing remains with the respective projects. See [LICENSE](LICENSE) for this repository's license.

---
Designed by Meena Vignesh M.
