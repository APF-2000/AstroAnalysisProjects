# Finding a Black Hole in GS2000

This folder contains an HTML notebook export, [GS2000_BlackHole_Analysis.html](/Applications/Data Intensive Science/AstroAnalysisProjects/FindingBlackHoles/GS2000_BlackHole_Analysis.html), analyzing the binary system GS2000 to determine whether its unseen compact object is a neutron star or a black hole.

## Overview

The notebook studies `13` spectra of GS2000 taken at different orbital phases and compares them against a library of template-star spectra. The broad idea is:

- normalize the template and target spectra by fitting and dividing out the continuum;
- identify the donor-star absorption features, especially the Na D region;
- exclude the strong `H-alpha` emission near `6530 A` because it is not tracing the donor-star photosphere;
- cross-correlate / chi-squared fit the target spectra against a best-matching template to estimate the donor-star radial velocity at each phase;
- fit a sinusoidal radial-velocity curve to recover the semi-amplitude `K`;
- use the mass function and Monte Carlo sampling over uncertain system parameters to infer the mass of the compact object.

## Key Spectral Findings

- The spectra show a strong `H-alpha` emission feature near `6530 A`.
- The averaged spectrum also shows Na D absorption around `5890/5896 A`.
- The notebook concludes that K- and M-type templates are the best qualitative match for the donor star.
- The chosen working template is `K5`, selected because its normalized absorption pattern resembles the averaged GS2000 spectrum well.

## Radial Velocity Results

For each of the `13` phases, the notebook fits a velocity shift by minimizing chi-squared over a dense velocity grid. The resulting radial velocities are:

| Phase | Radial Velocity (km/s) | Uncertainty (km/s) |
| --- | ---: | ---: |
| -0.1405 | -412.566257 | 8.610861 |
| -0.0583 | -165.991599 | 9.885989 |
| 0.0325 | 171.752175 | 8.155816 |
| 0.0998 | 338.938894 | 5.120512 |
| 0.1740 | 492.334233 | 5.360536 |
| 0.2310 | 530.328033 | 4.840484 |
| 0.3079 | 518.676868 | 4.735474 |
| 0.3699 | 393.714371 | 10.266027 |
| 0.4388 | 225.547555 | 5.945595 |
| 0.5008 | 56.160616 | 9.900990 |
| 0.5698 | -203.435344 | 6.980698 |
| 0.6371 | -394.704470 | 6.480648 |
| 0.7276 | -498.494849 | 6.505651 |

These velocities vary sinusoidally with orbital phase, as expected for a star orbiting an unseen companion.

### Velocity semi-amplitude

The fitted radial-velocity semi-amplitude is:

- `K = 529.13 +/- 2.60 km/s`

This is the key observational input to the compact-object mass estimate.

## Mass Function and Compact-Object Mass

Using the orbital period and the measured `K`, the notebook computes the mass function:

- `f(M_x) = 1.0502593330960314e+31 +/- 6.489886385264378e+19` in SI units

It then converts this into a compact-object mass estimate.

### Preliminary estimate

Under the simplifying assumptions:

- inclination `i = 90 deg`
- donor mass `M_c = 0.5 M_sun`

the notebook gets:

- `M_x = 6.1707 M_sun`

That already places the compact object well above the usual upper bound for a neutron star, around `3 M_sun`.

### Monte Carlo result

The notebook then performs a Monte Carlo simulation with:

- `1,000,000` samples
- inclination sampled over `50 deg < i < 80 deg`
- donor mass sampled uniformly between `0.6` and `0.75 M_sun`
- `K` sampled from its measurement uncertainty
- orbital period sampled with a small assumed uncertainty

The key result is:

- `P(M_x > 3 M_sun) = 1.0000`

So within the assumptions of the notebook, every Monte Carlo draw is consistent with a black hole rather than a neutron star.

## Physical Conclusion

The main conclusion of the notebook is:

- the unseen compact object in GS2000 is very likely a **black hole**

The logic is straightforward:

- the donor-star radial-velocity amplitude is large;
- the inferred mass function is high;
- even conservative sampling over inclination and donor mass still puts the compact object above the neutron-star limit.

## Caveats

The notebook notes or implies several modeling assumptions:

- The donor-star template match is chosen qualitatively, with `K5` used as the working template.
- The `H-alpha` emission is masked because it is not assumed to trace the stellar absorption-line motion.
- The orbital-period uncertainty is not well constrained in the notebook and is assigned a small assumed value in the Monte Carlo stage.
- The donor mass and inclination are sampled from plausible ranges rather than measured directly in this workflow.

These assumptions affect the exact inferred mass distribution, but not the central conclusion that the compact object is comfortably above the neutron-star regime.

## Files

- [GS2000_BlackHole_Analysis.html](/Applications/Data Intensive Science/AstroAnalysisProjects/FindingBlackHoles/GS2000_BlackHole_Analysis.html): full notebook export with spectral normalization, velocity fitting, mass-function calculation, and Monte Carlo inference
