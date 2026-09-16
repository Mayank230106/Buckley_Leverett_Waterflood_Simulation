# Buckley–Leverett Waterflood Simulation & Recovery Analysis

A computational reservoir-engineering study that models one-dimensional immiscible waterflooding using relative permeability, fractional-flow theory and Buckley–Leverett displacement.

The project investigates how fluid properties and rock-fluid interaction affect water movement, breakthrough and oil recovery.

## Project Objectives

- Build synthetic relative-permeability curves using Corey correlations.
- Calculate phase mobility and water fractional flow.
- Determine shock-front saturation using the Buckley–Leverett tangent condition.
- Estimate analytical water breakthrough and injected pore volume.
- Solve the saturation-transport equation numerically using a finite-volume upwind scheme.
- Generate synthetic water-cut and oil-rate responses.
- Calculate cumulative oil recovery.
- Analyze mobility ratio.
- Perform sensitivity studies on oil viscosity, water viscosity and relative-permeability shape.

## Physical Model

The project considers a homogeneous 1-D reservoir under the following assumptions:

- Immiscible oil-water displacement
- Incompressible fluids and rock
- Homogeneous and isotropic formation
- Constant fluid viscosities
- No gravity segregation
- No capillary pressure
- Uniform initial water saturation
- Constant total injection rate

The phase mobilities are:

\[
\lambda_w = \frac{k_{rw}}{\mu_w},
\qquad
\lambda_o = \frac{k_{ro}}{\mu_o}
\]

Water fractional flow is calculated from:

\[
f_w =
\frac{k_{rw}/\mu_w}
{k_{rw}/\mu_w+k_{ro}/\mu_o}
\]

## Relative Permeability

Normalized water saturation is defined as:

\[
S_{wn} =
\frac{S_w-S_{wi}}
{1-S_{wi}-S_{or}}
\]

Corey-style correlations are then used:

\[
k_{rw}=k_{rw,end}S_{wn}^{n_w}
\]

\[
k_{ro}=k_{ro,end}(1-S_{wn})^{n_o}
\]

## Buckley–Leverett Analysis

The shock-front saturation satisfies:

\[
\left.\frac{df_w}{dS_w}\right|_{S_{wf}}
=
\frac{f_w(S_{wf})}
{S_{wf}-S_{wi}}
\]

The corresponding breakthrough pore volume is:

\[
\left(\frac{PV_{inj}}{PV}\right)_{BT}
=
\frac{S_{wf}-S_{wi}}
{f_w(S_{wf})}
\]

The notebook solves the shock condition numerically and converts the result into an analytical breakthrough time.

## Numerical Simulation

The water-saturation transport equation is:

\[
\phi\frac{\partial S_w}{\partial t}
+
\frac{q_t}{A}
\frac{\partial f_w}{\partial x}=0
\]

A first-order finite-volume upwind method is used to propagate the saturation front through the reservoir.

A CFL-based timestep is selected for numerical stability.

The numerical solution provides:

- Water-saturation profiles
- Outlet water cut
- Oil-rate response
- Cumulative recovery
- Numerical breakthrough time

The numerical breakthrough is compared with the analytical Buckley–Leverett prediction.

## Base Reservoir

| Parameter | Value |
|---|---:|
| Reservoir length | 1000 ft |
| Reservoir width | 500 ft |
| Net thickness | 50 ft |
| Porosity | 0.22 |
| Absolute permeability | 150 md |
| Initial water saturation | 0.22 |
| Residual oil saturation | 0.20 |
| Oil viscosity | 10 cP |
| Water viscosity | 1 cP |
| Injection rate | 1000 STB/day |
| Water Corey exponent | 2.0 |
| Oil Corey exponent | 2.0 |
| Endpoint \(k_{rw}\) | 0.60 |
| Endpoint \(k_{ro}\) | 0.80 |

## Mobility Ratio

The water/oil mobility ratio is evaluated as:

\[
M =
\frac{k_{rw}\mu_o}
{k_{ro}\mu_w}
\]

with the shock-front relative permeabilities used for the primary diagnostic.

The mobility ratio is used to interpret the fluid-mobility contrast; it is not treated as a standalone predictor of full-field recovery.

## Sensitivity Analysis

### Oil viscosity

The model compares oil viscosities of:

- 2 cP
- 5 cP
- 10 cP
- 20 cP
- 30 cP

Outputs include breakthrough time, shock saturation, mobility ratio and recovery.

### Water viscosity

Water viscosity is varied across:

- 0.5 cP
- 1.0 cP
- 2.0 cP
- 3.0 cP

This demonstrates the effect of changing water mobility and provides a simple mobility-control interpretation.

### Relative permeability

The water Corey exponent is varied to demonstrate how the shape of the relative-permeability relationship affects fractional flow and breakthrough.

## Visualizations

The notebook generates:

- Corey relative-permeability curves
- Fractional-flow curve
- Buckley–Leverett shock construction
- Water-saturation profiles through time
- Water-cut response
- Oil-rate response
- Cumulative recovery
- Breakthrough sensitivity to oil viscosity
- Recovery sensitivity to oil viscosity
- Mobility-ratio sensitivity to water viscosity
- Fractional-flow sensitivity to relative-permeability shape
- Breakthrough sensitivity to Corey exponent

## Tech Stack

- Python
- Jupyter Notebook
- NumPy
- Pandas
- SciPy
- Matplotlib

## Repository Structure

```text
.
├── Buckley_Leverett_Waterflood_Simulation.ipynb
└── README.md
```

## Engineering Interpretation

The project demonstrates the link between microscopic rock-fluid properties and macroscopic waterflood performance:

```text
Relative Permeability
        ↓
Phase Mobility
        ↓
Fractional Flow
        ↓
Shock Saturation
        ↓
Water Breakthrough
        ↓
Water Cut / Oil Rate
        ↓
Cumulative Recovery
```

The model shows how viscosity contrast and relative-permeability assumptions can materially alter the predicted displacement behavior.

## Limitations

This is an educational 1-D analytical/numerical model rather than a commercial reservoir simulator.

It does not include:

- Geological heterogeneity
- Gravity segregation
- Capillary pressure
- Compressibility
- Multiphase PVT
- Fractures
- Well-pattern geometry
- 2-D/3-D sweep
- Polymer rheology
- Relative-permeability hysteresis
- Reservoir pressure coupling

All reservoir properties are synthetic and should not be used for real-field development or reserves decisions.
