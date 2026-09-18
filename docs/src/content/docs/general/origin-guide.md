---
title: Vector vs. Custom Code
description: How to tell Vector-provided, customised and in-house modules apart.
---

# Vector vs. Custom Code

Every module page carries an origin badge. The four categories used in this
documentation are:

## Custom (in-house)

Application and driver code developed by the EPS (Nexteer) team: all `Ap_*`
steering functions, `Sa_*/Cd_*` drivers, wrappers (`Adc`, `Dma`, `SpiNxt`,
`ePWM`, …) and utilities (`NxtrLib`, `NtWrap`). These files are the ones you
edit for functional changes.

> Note: custom `.c` files often start from a **MICROSAR RTE Generator
> template** (`Generator: MICROSAR RTE Generator …` in the file header). The
> template scaffolding is generated; the control logic between the
> `Start of include and declaration area` markers is hand-written.

## Vector-provided

Delivered verbatim as part of the **Vector MICROSAR** BSW stack and
documentation — recognise them by `Copyright … by Vector Informatik GmbH`
headers and the `TechnicalReference_*` manuals:

- `PSA_BMPV_EPS_TMS570/SwProject/Source/BSW/*` (CAN driver, IL, Tp, Nm, EcuM,
  Dem, Det, NvM/MemIf, Crc, MCAL drivers, WdgM, XCP, VStdLib),
- `PSA_BMPV_EPS_TMS570/HLDD/BSW/*` (Technical References, see
  [HLDD references](../../integration/hldd/)).

Do not modify these files; configure them through DaVinci/GENy and regenerate.

## Vector-provided, customised

Vector-based artefacts with project-specific customisation:

- **RTE & generated configuration** (`GenData`, `GenDataRte`, `GenDataOS`) —
  see [RTE & GenData](../../integration/rte-gendata/),
- **`SrlComDriver` / `SrlComInput` / `SrlComOutput`** — PSA serial
  communication on top of the Vector interaction layer,
- **`CMS_PSA`** — PSA manufacturing services including a Vector-derived XCP
  file (`EPS_DiagSrvcs_XCP.Vector.c`).

Regenerate these from the DaVinci/GENy models; never hand-edit generated outputs.

## Third-party (TI / Gliwa)

Silicon/tool-vendor code adapted for this project:

- **`Fee` / `Fls`** — TI F021 Flash API and Flash-EEPROM emulation,
- **`TMS570_Startup`** — TI HALCoGen-derived startup (reset, clocks, vectors),
  adapted by the project,
- **`GliwaT1`** — Gliwa T1 timing executive.

Keep vendor files pristine; put adaptations in marked wrapper files.

## Quick reference

| Path pattern | Typical origin |
| --- | --- |
| `<Module>/src/Ap_*.c`, `Sa_*.c`, `Cd_*.c` | Custom |
| `SwProject/Source/BSW/*` | Vector |
| `SwProject/Source/GenData*` | Vector, customised |
| `<Module>/generate/*.tt` | Generator inputs (edit these, not outputs) |
| `Fee/`, `Fls/`, `GliwaT1/`, `TMS570_Startup/` | Third-party |
| `*.dcf`, `*.arxml` in `autosar/` | DaVinci models (inputs) |
