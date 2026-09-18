---
title: Glossary
description: Abbreviations and terms used across the EPS codebase and docs.
---

# Glossary

| Term | Meaning |
| --- | --- |
| AP / Ap_ | Application software component (AUTOSAR SW-C) |
| ASIL | Automotive Safety Integrity Level (ISO 26262); this EPS targets ASIL-D |
| ASW | Application Software |
| BMPV | PSA small-car platform family (now Stellantis) |
| BSW | Basic Software |
| CBD | Component-based development unit used by the EPS team |
| CDD | Complex Device Driver |
| DCF / ARXML | DaVinci / AUTOSAR XML component descriptions |
| Dem / DemIf | Diagnostic Event Manager and its project interface |
| EOT | End of travel (rack end-stops) |
| EPS | Electric Power Steering |
| FEE / Fee | Flash EEPROM Emulation (TI F021) |
| GENy | Vector network/IL configuration generator |
| HLDD | High-level design documents (Vector Technical References) |
| IL | Interaction layer (signal-based communication) |
| MCAL | Microcontroller Abstraction Layer |
| MDD | Module Design Document (per-module design spec in `doc/`) |
| MSB | Motor sensor board (rotor position sensor) |
| NvM / NvMMgr | NVRAM manager |
| QAC | Static-analysis tool (per-module `tools/QAC` projects) |
| RTE | Runtime Environment (Vector MICROSAR-generated) |
| Sa_ / Cd_ | Sensor-actuator SW-C / CDD component prefixes |
| SENT | Single Edge Nibble Transmission (sensor protocol) |
| TESSY / UTP | Unit-test tool and unit-test-package contracts (`utp/`) |
| TMS570 | TI Hercules Cortex-R4 automotive MCU |
| UDS | Unified Diagnostic Services |
| XCP | Universal measurement & calibration protocol |

## Naming conventions in code

- `Ap_<Name>_Per1/Per2` — periodic runnables; `Ap_<Name>_Init1` — init runnable;
  `Ap_<Name>_Trns1` — transition runnable.
- `Rte_IRead_<RE>_<Port>_<Type>()` / `Rte_IWrite_<RE>_<Port>_<Type>()` —
  implicit RTE port access.
- `D_*` / `d_*` macros and `CalConstants` — calibration constants; defaults in
  `DfltConfigData`.
- Fixed-point suffixes (`_f32`, `_s16`, `_u16`, `_Uls`, `_HwNm`, `_MtrNm`,
  `_Kph`) encode type, unit and scaling per the project data dictionary.
