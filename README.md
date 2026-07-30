# NeuroData Interface

> **⚠️ Deprecated.** This project has been superseded by **[PhysicsAnalysisGUI](https://github.com/zakgm2/PhysicsAnalysisGUI)**, a general-purpose lab data analysis GUI that includes full TDT fiber photometry support (motion correction, ΔF/F, PETH/z-score, plus Oxysoft NIRS, generic tabular data, and more) with a more complete and actively maintained feature set. This repo is kept for reference/reproducibility of the original literature review and prototype only — **new development happens in PhysicsAnalysisGUI.**

---

A platform-agnostic, open-source Python framework for the preprocessing and visualization of fiber photometry data in behavioral neuroscience, developed at Concordia University.

## Overview

Fiber photometry analysis is often locked behind proprietary, closed-source software with limited cross-platform support and no transparency into how signals are actually processed. NeuroData Interface was built to address that: a pipeline-based, fully inspectable Python tool for turning raw TDT photometry recordings into interpretable, denoised fluorescence traces and event-aligned analyses.

## Pipeline

Raw dual-wavelength recordings (465 nm calcium-dependent / 415 nm isosbestic control) are processed through a fixed, documented sequence:

1. **Motion artifact correction** — linear regression of the isosbestic (415 nm) signal onto the calcium-dependent (465 nm) signal; the fitted control trace is subtracted to remove shared non-neural variance.
2. **Photobleaching correction & baseline estimation** — double-exponential decay model fit to a masked subset of the signal.
3. **ΔF/F normalization** — signal expressed relative to estimated baseline fluorescence.
4. **Signal denoising** — low-pass filtering (~5 Hz cutoff) to suppress high-frequency motion/electronic noise while preserving GCaMP-scale kinetics.
5. **Event alignment & PETH construction** — z-score normalized peri-event time histograms aligned to behavioral events (e.g. reward delivery, stimulation).

## Features

- Platform-agnostic (Windows/macOS/Linux), no proprietary dependencies
- Interactive pan/zoom (cursor-centered scroll zoom, click-drag pan)
- Event-centered analysis via double-click
- Z-score PETH visualization
- Figure export (PNG/PDF) with auto-generated, timestamped filenames

## Requirements

- Python 3.x
- TDT tank data (`.Tbk`, `.tev`, etc.)

## Background

Developed as part of an undergraduate literature review and lab course at Concordia University, supervised by Dr. Uri Shalev. Full methodology and theoretical background are documented in the accompanying literature review.

## Related Projects

- **[PhysicsAnalysisGUI](https://github.com/zakgm2/PhysicsAnalysisGUI)** — the actively maintained successor; a PyQt6 desktop app supporting TDT fiber photometry, Oxysoft/Artinis NIRS, generic tabular data, and more, built on shared logic from [PhysicsLibrary](https://github.com/zakgm2/PhysicsLibrary).

## License

MIT — see [LICENSE](LICENSE) for details.
