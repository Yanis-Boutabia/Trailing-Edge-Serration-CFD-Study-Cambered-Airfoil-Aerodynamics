# CFD Report — Effect of Serration Density on Cambered Airfoil Aerodynamics

Comparative CFD study using STAR-CCM+ on the effect of trailing-edge serration density on a cambered airfoil's aerodynamic performance.

**Authors:** Yanis Boutabia · Ilhan Tabich · Mohammed Ziani — IPSA Paris, 2025-2026

## Overview

Two airfoil geometries, designed in CATIA V5, were compared under identical flow conditions to isolate the effect of trailing-edge serration density:
- **Case A** (`Aile.CATPart`) — 9 large serrations (high density)
- **Case B** (`Aile_Fine.CATPart`) — 7 finer serrations (low density)

**Key result: Case A (9 serrations) delivers a +13.3% lift gain over Case B for a virtually unchanged drag (≈0.2% difference), yielding a +13.1% improvement in lift-to-drag ratio (L/D).**

![CATIA V5 geometry for both cases](./images/fig1-catia-parts.png)
*Figure 1 — CATIA V5 part for both cases*

## Methodology

- **Tool:** STAR-CCM+, geometry built in CATIA V5
- **Domain:** Virtual wind tunnel, dimensions scaled to chord length — no-slip walls on top/bottom/lateral faces
- **Flow regime:** Subsonic steady-state RANS, M ≈ 0.06, Re ≈ 10⁶ (fully turbulent)
- **Turbulence model:** k-ω SST, segregated flow solver, 2nd-order spatial discretisation
- **Boundary conditions:** Velocity inlet U∞ = 20 m/s (turbulence intensity 1%) · Pressure outlet P_gauge = 0 Pa · smooth adiabatic walls
- **Mesh:** Polyhedral, 83,368 cells (identical setup for both cases), cylindrical refinement region + prism-layer near-wall treatment
- **Convergence:** Residuals reached 1×10⁻⁸ after ~150 iterations, 380 total iterations run

![Computational domain — virtual wind tunnel](./images/fig2-domain.png)
*Figure 2 — Domain tunnel*

![Mesh overview and detail](./images/fig3-mesh.png)
*Figure 3 — Mesh overview and zoom detail for both cases*

## Results

Results are reported in relative form (Case A = reference), since the solver's internal reference area was not normalised to the actual wing planform — see [Limitations](#limitations).

| Parameter | Case A (9 serrations) | Case B (7 serrations) | Δ (A vs B) |
|---|---|---|---|
| Lift coefficient (CL, relative) | Reference | −11.7% | **+13.3% ▲** |
| Drag coefficient (CD, relative) | Reference | ≈ −0.2% | ≈ equivalent |
| Lift-to-drag ratio (L/D, relative) | Reference | −11.6% | **+13.1% ▲** |

The 9-serration geometry fragments the trailing-edge pressure gradient, reducing trailing-edge vortex coherence and sustaining suction further aft along the chord — increasing lift without a drag penalty. Drag remained essentially unaffected by serration density under the tested conditions.

### Flow field visualization

![Pressure contour for both cases](./images/fig9-pressure-contour.png)
*Case A shows a more pronounced suction peak on the upper surface, consistent with its higher CL*

![Velocity field for both cases](./images/fig11-velocity-field.png)
*Case A generates a more fragmented, distributed wake; Case B produces a more compact, coherent wake*

![Vorticity field — Case A (9 serrations)](./images/fig13-vorticity-caseA.png)
*Case A — max vorticity ≈ 984 s⁻¹, extended rotational region along the suction side*

![Vorticity field — Case B (7 serrations)](./images/fig14-vorticity-caseB.png)
*Case B — max vorticity ≈ 885 s⁻¹, more concentrated and compact wake*

## Limitations

- Single mesh density (83,368 cells) — no formal mesh independence study; absolute CL/CD values should be interpreted with caution, results are most reliable as a **relative comparison** between the two geometries
- Steady-state RANS (k-ω SST) cannot fully capture the unsteady vortex shedding of serrated trailing edges — LES/DES would be needed for the full physical mechanism
- No experimental (wind-tunnel) validation available
- Absolute CD values appear high relative to standard airfoil literature, likely tied to the reference-area normalisation used internally by the solver

## Recommended perspectives

- Mesh convergence study (100k / 500k / 1M cells) with Richardson extrapolation
- LES/DES simulation to resolve unsteady trailing-edge vortex shedding
- Ffowcs Williams–Hawkings acoustic analysis (trailing-edge noise — the main industrial motivation for serrations)
- Parametric sweep over 5+ serration configurations (density, amplitude, wavelength)
- Experimental validation via wind-tunnel testing of 3D-printed serration inserts

## Tools

`CATIA V5` (geometry) · `STAR-CCM+` (CFD — polyhedral mesh, k-ω SST RANS)

---
*Academic project — IPSA Paris, CFD in Aerospace Engineering, 17/05/2026.*
