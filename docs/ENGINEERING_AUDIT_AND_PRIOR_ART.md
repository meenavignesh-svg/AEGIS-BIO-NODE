# AEGIS Bio-Node — preliminary engineering and prior-art audit

**Status:** preliminary desk review, 24 October 2026  
**Evidence status:** concept / design hypothesis. No wet-lab data, validated CFD, sterility validation, pressure testing, or mesh-integrity report is claimed.

## 1. Current implementation audit

The current site is a single-page HTML/CSS/JavaScript application using Three.js 0.165.0 via an import map/CDN and a WebGL canvas. The source includes camera/view controls, Solid/Wireframe/X-ray/Core-only modes, component visibility toggles, adjustable gyroid settings, and a clipping-based section view.

The gyroid is represented by the implicit scalar field

\[
g(x,y,z)=\sin(x)\cos(y)+\sin(y)\cos(z)+\sin(z)\cos(x).
\]

The current renderer samples the field and extracts level surfaces. It then clips triangle polygons to an approximate cylindrical envelope. That is not equivalent to constructing a closed, constant-thickness TPMS solid: clipping a surface can leave open boundary edges, and the displayed section cut clips rather than caps the cut. The visible lobed/rough appearance in the supplied screenshot is consistent with a mesh-generation or surface-boundary problem; the exact rendering cause has not been confirmed in a live browser.

The chamber and assembly details are constructed from Three.js primitives. The model has visually represented vessel walls, end flanges/rings, inlet/outlet-like ports, sensor docks and seals. Their presence in a rendering does not establish a pressure-tight fluid path, correct sealing compression, manufacturability, sterility or sensor performance. The current page's flow particles are illustrative and are not CFD.

### Verified from source
- Single-page, client-side Three.js application; Three.js 0.165.0 is loaded from a CDN.
- Solid, Wireframe, X-ray, Core-only and Section-cut controls exist in the markup/source.
- Geometry is generated in browser code from an implicit gyroid field.
- A cylinder-envelope clipping step is present.
- No server-side API or required paid service was identified in the inspected main HTML.

### Not verified
- Live deployment correctness, all controls in a browser, browser console, performance on ordinary hardware, mobile behavior.
- Mesh watertightness, manifoldness, self-intersections, connected components, or STL/STEP export.
- Chamber sealing, pressure rating, material compatibility, sterilization, optical calibration, cell culture performance.
- Any numerical CFD output.

## 2. Preliminary prior-art review

This is a targeted search, not an exhaustive patentability or freedom-to-operate search. Google Patents records below are starting points; claim scope, prosecution history, family status, and jurisdiction must be checked by a qualified patent professional. The search did not establish that the complete AEGIS combination is new.

| Reference | Verified subject matter | Overlap with AEGIS | Potential distinction / uncertainty |
|---|---|---|---|
| Merkel M, Noll P, Lilge L, Hausmann R, Henkel M (2023). “Design and evaluation of a 3D-printed, lab-scale perfusion bioreactor for novel biotechnological applications.” *Biotechnology Journal* 18(10), e2200554. DOI: [10.1002/biot.202200554](https://doi.org/10.1002/biot.202200554) | 3D-printed perfusion reactor; pH/DO probe ports, O-ring-sealed interfaces, membrane oxygen transfer and cell-retention membranes; experiments including mixing and oxygen transfer. | Modular 3D-printed perfusion hardware and probe access. | Does not, from the reviewed description, establish the same removable gyroid cartridge. Detailed comparison of full design and supplementary files remains necessary. |
| “An optimized 3D-printed perfusion bioreactor for homogeneous cell seeding in bone substitute scaffolds for future chairside applications” (2021; PMC full text). [Source](https://pmc.ncbi.nlm.nih.gov/articles/PMC8593024/) | Perfusion chamber and oxygen measurement using a commercial flow-through oxygen sensor at inlet/outlet. | Perfusion and oxygen sensing. | The exact cartridge-interface combination is not established by the retrieved summary; full-text review required. |
| “A Perfusion Bioreactor System for Cell Seeding and Oxygen-Controlled Cultivation of Three-Dimensional Cell Cultures” (2018). [Source](https://pmc.ncbi.nlm.nih.gov/articles/PMC6208160/) | Multiple perfusion microbioreactors, oxygen microsensors at scaffold centers, and a feedback loop that adjusts perfusion velocity; CFD used to examine flow distribution. | Sensor-based monitoring/control and perfusion. | The retrieved record does not establish a gyroid cartridge exchange interface. |
| “Customizable 3D printed perfusion bioreactor for the engineering of stem cell microenvironments” (2023). [Source](https://pmc.ncbi.nlm.nih.gov/articles/PMC9870251/) | 3D-printed perfusion chamber with a scaffold holder, threaded/interlocking chamber components, silicone O-ring, and syringe-accessible inlet/outlet. | Replaceable scaffold/chamber assembly and sealed interfaces. | A repeatable optical alignment interface combined with TPMS needs comparison against the complete paper and its cited work. |
| “Comparing ceramic Fischer-Koch-S and gyroid TPMS scaffolds for potential in bone tissue engineering” (2024). DOI: [10.3389/fbioe.2024.1410837](https://doi.org/10.3389/fbioe.2024.1410837) | Experimental permeability evaluation of gyroid and Fischer-Koch-S scaffolds using measured pressure drop at multiple flow rates. | Gyroid-versus-control hydraulic comparison. | Shows that comparison methodology is established; AEGIS needs a distinct, well-controlled research question rather than merely comparing gyroid and a control. |
| US20220064625A1, “Gas biocatalysis via an immobilized cell bioreactor.” [Google Patents](https://patents.google.com/patent/US20220064625A1/en) | Describes a bioreactor with a printed gyroid scaffold/lattice and a housing. | Direct overlap with gyroid scaffold inside a bioreactor. | This materially weakens any broad novelty claim based on “a gyroid in a bioreactor.” Specific architecture/operation must be compared claim by claim. |
| US20210348096A1, “Continuous flow microbioreactor.” [Google Patents](https://patents.google.com/patent/US20210348096A1/en) | Describes continuous-flow bioreactor minimodules including gyroid/double-gyroid/TPMS paths and interconnected modules. Related grant record: [US12331274B2](https://patents.google.com/patent/US12331274B2/en). | Direct overlap with modular gyroid flow architecture. | Strong evidence against claiming modular gyroid flow architecture alone as new. Exact claims and family/jurisdiction require professional review. |
| US20190233787A1, “Bioreactor.” [Google Patents](https://patents.google.com/patent/US20190233787A1/en) | Tissue-construct perfusion chamber with ports, detachable modules and an analyzing port for optical/infrared sensor or imaging access. | Modular perfusion chamber and optical sensor access. | Strong overlap with the broad sensor-docking concept. Specific repeatable alignment, sterility boundary and cartridge interface remain to be examined in claims and drawings. |
| US8008065B2, “Disposable bioreactor vessel port.” [Google Patents](https://patents.google.com/patent/US8008065B2/en) | Optical, electrical, acoustic, magnetic and microfluidic measurements through a bioreactor vessel port. | Sensor ports and optical measurement interfaces. | The AEGIS rendering alone does not demonstrate a novel sterile interface. |
| US20250257300A1, “Microtiter-plate-based high throughput perfusion bioreactor.” [Google Patents](https://patents.google.com/patent/US20250257300A1/en) | Describes perfusion plugs/channels, a fluorescence oxygen sensor and camera readout through a transparent well bottom. | Perfusion plus optical oxygen sensing. | Different format, but confirms optical sensor integration is already an active design space. |
| Han X et al. (2026). “3D triply periodic minimal surface gyroid hydrogel scaffolds for soft tissue engineering.” *Nature Communications* 17, 7283. DOI: [10.1038/s41467-026-73452-y](https://doi.org/10.1038/s41467-026-73452-y) | Gyroid hydrogel scaffold design and biological evaluation for vascularized tissue constructs. | Gyroid architecture for tissue engineering. | Does not establish the specific modular chamber interface from the retrieved record; nonetheless, gyroid tissue scaffolds are established prior art. |

### Preliminary novelty assessment

**Assessment B: a possible differentiating feature exists but needs further investigation.** There is clear prior art for gyroid structures in bioreactors, modular gyroid flow paths, perfusion chambers with sensor ports, and optical measurement interfaces. The combined phrase “modular gyroid perfusion bioreactor with optical sensor docking” is not a defensible novelty claim by itself.

A more testable contribution might be a **metrologically repeatable cartridge exchange interface** that preserves optical sensor-to-scaffold position after repeated swaps, evaluated alongside hydraulic resistance and bypass leakage. This is a research hypothesis, not a claim that prior art lacks it. The relevant patent families and full claims need more systematic review before asserting a gap.

## 3. Recommended research question

**Question:** Under matched chamber envelope, fluid properties and flow rates, how do a gyroid cartridge and a straight-channel control differ in pressure drop and flow-distribution uniformity, and does a keyed cartridge interface preserve optical measurement position after repeated cartridge exchanges?

**Hypothesis (to test, not assume true):** A keyed locating feature can reduce sensor-position variability across cartridge swaps relative to a non-keyed fixture. The gyroid may or may not improve flow distribution; it may increase pressure loss.

### Why this is stronger than the current broad claim
- It defines measurable outcomes rather than relying on visual novelty.
- It separates the interface repeatability question from the scaffold-hydraulics question.
- It permits a negative result and a fair comparison.
- It can start with water and a non-biological dye/tracer before cell culture.
- It avoids claiming sterility or cell performance without evidence.

## 4. Geometry and CAD plan

Use a physically dimensioned implicit sheet. Let physical coordinates be in metres or millimetres, but convert consistently. Define dimensionless coordinates:
\[
X=2\pi x/a,\quad Y=2\pi y/a,\quad Z=2\pi z/a
\]
where \(a\) is the unit-cell period in the same length unit as x, y and z. Then:
\[
g=\sin X\cos Y+\sin Y\cos Z+\sin Z\cos X.
\]

Two distinct construction options must not be confused:
1. **Level-set sheet band:** \(|g|\le t_g\), a solid region around a dimensionless field. This is convenient for voxel/implicit solid construction, but \(t_g\) is not a physical thickness in millimetres.
2. **Offset surface / signed-distance sheet:** construct an actual offset from the zero level set using a signed-distance approximation or robust CAD offset. A physical thickness \(t_s\) can then be specified in millimetres, subject to local curvature limits.

For a first reliable prototype, use a robust implicit-solid/voxel or marching-cubes pipeline with explicit resolution and test convergence of the mesh as resolution increases. Close the cartridge ends using designed end rings/manifolds; do not rely on cutting open TPMS triangles and pretending the edges are sealed. Export STL only after mesh repair/validation. STEP export requires an actual CAD/B-rep route and should not be promised from Three.js geometry.

### Geometry checks required before a “printable” label
- Watertightness and boundary-edge count.
- Manifoldness and consistent normals.
- Connected-component count.
- Self-intersection checks.
- Minimum wall thickness and minimum clearance.
- Mesh-resolution convergence.
- CAD/mesh slicer inspection and a small test coupon.

## 5. Engineering equations and limitations

Use SI units internally. For a circular tube, \(A=\pi D^2/4\) and \(v=Q/A\). For a non-circular duct, \(D_h=4A/P_w\), where \(P_w\) is wetted perimeter. \(Re=\rho vD_h/\mu\) is a useful regime indicator only when the characteristic velocity and hydraulic diameter are meaningfully defined.

For a straight, fully developed duct, Darcy–Weisbach gives:
\[
\Delta P=f\frac{L}{D_h}\frac{\rho v^2}{2}.
\]
Do **not** apply a straight-pipe friction factor directly to a gyroid. For a TPMS, pressure loss should be measured or obtained from a CFD solution with defined geometry, mesh, fluid properties and boundary conditions. For low-Re porous media, an experimentally fitted Darcy relation may be appropriate:
\[
\Delta P/L=(\mu/K)u
\]
where K is permeability and u is superficial velocity; check whether inertial Forchheimer terms are needed at higher flow rates.

Hydraulic pump power is \(P_h=\Delta P Q\), not the electrical input power. Nominal residence time \(\tau=V_{working}/Q\) is only a volume/flow estimate and does not describe residence-time distribution or stagnant zones. Oxygen transfer \(OTR=k_La(C^*-C_L)\) requires measured or sourced \(k_La\), saturation concentration and dissolved oxygen; it cannot be inferred from the current visual model.

## 6. Fair comparison protocol

Compare:
- A gyroid cartridge.
- A straight-channel control with the same external cartridge envelope.

Hold constant where feasible: chamber, working fluid and temperature, inlet/outlet fittings, test tubing, flow-rate set points, pressure-tap locations, and test procedure. Measure at multiple flow rates with replicate runs and record pressure drop after steady state. Use a dye pulse or conductivity tracer for residence-time distribution if appropriate.

Report:
- \(\Delta P(Q)\) and uncertainty.
- Estimated permeability only if the assumptions are satisfied.
- Residence-time distribution metrics from tracer data.
- Surface area and void fraction from validated CAD/mesh analysis.
- Sensor alignment error across repeated cartridge swaps.
- Leakage/bypass checks, separately from scaffold pressure loss.

Do not claim dead-zone volume or wall shear stress without a defined measurement method or converged flow solution. A CFD workflow should include a mesh-independence study, inlet/outlet boundary conditions, fluid-property source, solver/version, convergence criteria, mass-balance check and sensitivity analysis. Browser particles are visualization only.

## 7. Optical docking concept and risk

Treat the ports as **proposed optical access**, not sterile validated interfaces. A practical first test could use an external optical reader viewing a replaceable oxygen-sensitive or pH-sensitive spot through a defined window, while keeping electronics outside the fluid boundary. The window material, thickness, condensation, curvature, reflections, scaffold occlusion and sterilization compatibility can bias measurements. Calibration against a reference instrument and repeatability tests are required. A probe that physically penetrates the chamber needs a specified gasket/connector, sterilization approach and leakage validation.

## 8. Validation plan and safety

1. Validate CAD dimensions and cartridge fit with a printed non-biological test piece.
2. Test water leakage and pressure at a conservative, explicitly chosen test pressure with suitable guarding; do not use an unvalidated printed chamber as a pressure vessel.
3. Measure pressure drop and tracer response using water/dye and calibrated instruments.
4. Measure sensor alignment across repeated cartridge swaps.
5. Run CFD only after geometry and boundary conditions are established; compare CFD pressure drop with measured pressure drop.
6. Consider cell culture only after material compatibility, cleaning/sterilization strategy, leakage, and sensor calibration have been addressed.

Potential failure modes include leaks, trapped air, bypass around the cartridge, blocked ports, optical drift, nonuniform flow, rough printed surfaces, extractables/leachables and difficult cleaning. Standard consumer 3D-printing materials should not be assumed biocompatible, autoclavable or suitable for sterile culture.

## 9. Source and search limitations

Searches covered targeted web results and Google Patents records for gyroid bioreactors, modular continuous-flow gyroid systems, perfusion chambers and optical sensor ports. This was not a systematic search of every Google Patents family, Espacenet record or WIPO PATENTSCOPE database. No legal novelty, patentability or freedom-to-operate conclusion is made. Patent status, family members, priority dates and claim construction need a formal follow-up search.

## 10. Next most valuable experiment

**First experiment:** build a simple water-loop bench rig with pressure taps before and after each of two same-envelope cartridges (gyroid and straight-channel), then measure pressure drop at several controlled flow rates and repeat after cartridge reinstallation. This creates useful data even if the gyroid performs worse. A separate alignment test can quantify whether the keyed interface actually makes sensor placement repeatable.

## References

1. Merkel M, Noll P, Lilge L, Hausmann R, Henkel M. (2023). *Biotechnology Journal*, 18(10), e2200554. https://doi.org/10.1002/biot.202200554
2. Optimized 3D-printed perfusion bioreactor for homogeneous cell seeding in bone substitute scaffolds. (2021). https://pmc.ncbi.nlm.nih.gov/articles/PMC8593024/
3. A Perfusion Bioreactor System for Cell Seeding and Oxygen-Controlled Cultivation of Three-Dimensional Cell Cultures. (2018). https://pmc.ncbi.nlm.nih.gov/articles/PMC6208160/
4. Customizable 3D printed perfusion bioreactor for the engineering of stem cell microenvironments. (2023). https://pmc.ncbi.nlm.nih.gov/articles/PMC9870251/
5. Comparing ceramic Fischer-Koch-S and gyroid TPMS scaffolds for potential in bone tissue engineering. (2024). https://doi.org/10.3389/fbioe.2024.1410837
6. US20220064625A1. Gas biocatalysis via an immobilized cell bioreactor. https://patents.google.com/patent/US20220064625A1/en
7. US20210348096A1 / US12331274B2. Continuous flow microbioreactor. https://patents.google.com/patent/US20210348096A1/en
8. US20190233787A1. Bioreactor. https://patents.google.com/patent/US20190233787A1/en
9. US8008065B2. Disposable bioreactor vessel port. https://patents.google.com/patent/US8008065B2/en
10. US20250257300A1. Microtiter-plate-based high throughput perfusion bioreactor. https://patents.google.com/patent/US20250257300A1/en
11. Han X et al. (2026). Nature Communications, 17, 7283. https://doi.org/10.1038/s41467-026-73452-y
