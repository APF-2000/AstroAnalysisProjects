# Lightcurve QPO Analysis

This folder contains a notebook export, [QPO_analysis.html](/Applications/Data Intensive Science/AstroAnalysisProjects/lightcurve/QPO_analysis.html), analyzing quasi-periodic oscillations (QPOs) in the lightcurve of an eclipsing binary system with a white-dwarf primary and a main-sequence secondary.

## Overview

The analysis starts from the optical count-rate lightcurve and identifies an eclipse-like drop in flux between roughly `1250 s` and `1750 s`. To isolate higher-frequency oscillations, the notebook fits a loose B-spline trend and subtracts it, producing a residual lightcurve used for Fourier and chi-squared frequency analysis.

The study then:

- computes the sampling cadence and frequency limits of the dataset;
- searches trial frequencies up to the Nyquist limit using a sinusoidal chi-squared model;
- refines the strongest QPO frequency using a dense local frequency grid and a `chi^2_min + 1` uncertainty estimate;
- estimates the QPO amplitude from the best-fit sine/cosine coefficients;
- whitens the residuals with iterative optimal scaling (IOS) to search for additional candidate QPOs;
- inspects time dependence with a dynamic power spectrum and amplitude/phase tracking.

## Key Numerical Findings

### Sampling and resolution

- Sampling interval: `5.5965909091 s`
- Sampling frequency: `0.1786802030 Hz`
- Total duration: `2339.375 s`
- Nyquist frequency: `0.0893401015 Hz`
- Frequency resolution: `0.0004264444 Hz`
- Number of trial frequencies: `210`

### Strongest detected QPO

- Best frequency: `0.055747 +/- 0.000006 Hz`
- Period: `17.93834 +/- 0.00192 s`
- Amplitude: `193.47007 +/- 3.56540` flux units
- Relative amplitude: `0.0160027 +/- 0.0002949` of the out-of-eclipse flux, about `1.60%`

The strongest mode sits well below the Nyquist limit and is consistent with the notebook's expectation of QPO periods on the order of tens of seconds.

### Additional candidate QPOs after whitening

After iterative whitening, the notebook reports six candidate peaks:

| Candidate | Frequency (Hz) | Frequency Uncertainty (Hz) | Period (s) | Period Uncertainty (s) | Amplitude (flux units) | Amplitude Uncertainty |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| 1 | 0.055121 | 0.000009 | 18.141931 | 0.003088 | 165.356721 | 3.430462 |
| 2 | 0.055709 | 0.000021 | 17.950287 | 0.006870 | 56.628330 | 3.409874 |
| 3 | 0.054458 | 0.000021 | 18.362842 | 0.007190 | 52.433522 | 3.401800 |
| 4 | 0.069110 | 0.000021 | 14.469685 | 0.004464 | 41.671108 | 3.807419 |
| 5 | 0.068524 | 0.000020 | 14.593412 | 0.004359 | 57.958383 | 3.365923 |
| 6 | 0.067275 | 0.000021 | 14.864454 | 0.004711 | 43.018657 | 4.032705 |

These cluster into two approximate families:

- a group near `0.055 Hz` with periods around `18 s`;
- a group near `0.068-0.069 Hz` with periods around `14.5-14.9 s`.

## Physical Interpretation

The notebook highlights two main physical conclusions:

- The residual oscillation amplitude drops significantly during eclipse, implying that the QPO-emitting region is at least partly obscured.
- Because the signal weakens but does not vanish entirely, the author argues the QPO likely originates in the inner accretion disk rather than from a fully eclipsed point source.

The dynamic power-spectrum and phase/amplitude sections are intended to support this interpretation by showing that the oscillation strength changes over time and across eclipse.

## Caveats

The notebook also states a few important limitations:

- The QPO model is sinusoidal, while the signal is quasi-periodic, so the fit is not expected to be perfect.
- Aliasing appears once trial frequencies are extended beyond the Nyquist frequency, as expected.
- The amplitude-versus-time analysis is marked by the author as uncertain because overlapping QPOs remain in the residuals even after whitening.
- Some peaks seen after IOS may be influenced by imperfect subtraction of earlier modes rather than fully independent oscillations.

## Files

- [QPO_analysis.html](/Applications/Data Intensive Science/AstroAnalysisProjects/lightcurve/QPO_analysis.html): full notebook export with figures, derivations, and frequency-search workflow
- [file1.py](/Applications/Data Intensive Science/AstroAnalysisProjects/lightcurve/file1.py): placeholder script currently empty
