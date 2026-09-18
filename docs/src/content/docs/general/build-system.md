---
title: Build System
description: How the EPS firmware is built — CCS project, linker, make fragments and tooling.
---

# Build System

The firmware targets the **TI TMS570** (Cortex-R4, big-endian) and is built
with **TI Code Composer Studio (CCS)** plus Vector/GENy make fragments.

## Evidence in the repository

- `PSA_BMPV_EPS_TMS570/SwProject/.ccsproject` — CCS project definition.
- `PSA_BMPV_EPS_TMS570/SwProject/Linker.cmd` — linker command file (memory
  layout: Flash/RAM sections for code, calibration and NVRAM).
- `PSA_BMPV_EPS_TMS570/SwProject/Source/GenDataRte/mak/` — generated make
  fragments (`Rte_cfg.mak`, `Rte_rules.mak`, `Rte_defs.mak`, `Rte_check.mak`).
- `PSA_BMPV_EPS_TMS570/SwProject/Source/BSW/*/mak/` — per-BSW-module fragments
  (e.g. `Dem_cfg.mak`, `Dem_rules.mak`).
- `PSA_BMPV_EPS_TMS570/SwProject/postbuild.bat` — post-build steps.
- `PSA_BMPV_EPS_TMS570/SwProject/Tools/` — host-side tooling: `QAC` (static
  analysis), `Polyspace`, `Metrics`, `CCT`, `GnuWin32`, `GliwaT1`, `AsrProject`
  (Vector generators incl. `Artt`), `Patch`, `OilTool`.
- Per-module `tools/QAC/` projects and `utp/` TESSY contracts for unit testing;
  per-module `generate/*_Generate.bat` launchers for the DaVinci generation step.

## Typical build flow

1. **Generate**: run the DaVinci/GENy generation (module `generate/*.bat` and
   the central RTE/BSW generation) to refresh `GenData*` and RTE files.
2. **Compile**: build the CCS project for the TMS570 target
   (TI ARM compiler, big-endian Cortex-R4; `Fls` ships the prebuilt
   `F021_API_CortexR4_BE_V3D16.lib`).
3. **Static analysis / unit test**: QAC per-module projects; TESSY project-under-test
   contracts in each `utp/contract` folder.
4. **Flash**: program the image plus default calibration (`DfltConfigData`)
   onto the ECU.

## Toolchain assumptions

Host tooling is Windows-oriented (`.bat` launchers, CCS). The documentation
site in `docs/` is independent of the firmware toolchain — it builds with
Node.js (see the deployment workflow).
