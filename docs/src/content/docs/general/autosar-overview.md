---
title: AUTOSAR Architecture Overview
description: How this repository maps onto the AUTOSAR layered architecture.
---

# AUTOSAR Architecture Overview

This project implements an Electric Power Steering (EPS) ECU for the PSA BMPV
platform on a **TI TMS570** microcontroller, following the **AUTOSAR**
layered architecture and targeting **ISO 26262 ASIL-D**.

## Layer map

```text
┌──────────────────────────────────────────────────────────────┐
│ Application Software (ASW) — Ap_* SW-Cs                      │
│  Assist · Damping · Return · StaMd · DiagMgr helpers · PSA    │
├──────────────────────────────────────────────────────────────┤
│ RTE (Vector MICROSAR, generated — GenData/GenDataRte)        │
├──────────────────────────────────────────────────────────────┤
│ Complex Device Drivers  │  BSW Services  │  ECU Abstraction  │
│  Sa_*/Cd_* (SENT, MSB,  │  Dem/DemIf ·   │  Adc · IoHwAb     │
│  SPI, ePWM, SrlCom)     │  NvM/NvMMgr ·  │                   │
│                         │  Xcp · WdgM    │  MCAL             │
│                         │  EcuM · Os     │  Dio/Port/Mcu/Gpt │
│                         │                │  DMA · Fee/Fls    │
├──────────────────────────────────────────────────────────────┤
│ Microcontroller (TI TMS570, startup code, HALCoGen-derived)  │
└──────────────────────────────────────────────────────────────┘
```

## Conventions used in this repository

- **Application SW-Cs** are named `Ap_<Name>` (`Ap_Assist`, `Ap_StaMd`, …) and
  expose periodic runnables (`*_Per1/Per2`, `*_Init`, `*_Trns`) via
  `FUNC(void, RTE_...)` with `Rte_IRead_*` / `Rte_IWrite_*` port access.
- **Sensor/actuator SW-Cs and CDDs** are named `Sa_*` / `Cd_*`
  (`Sa_DigHwTrqSENT`, `Cd_FeeIf`, …).
- Each module ships `src/` (implementation), `include/` (public headers),
  `autosar/` (DaVinci component model), `generate/` (generator inputs),
  `tools/` (QAC/project scripts), `utp/` (TESSY unit-test contracts) and
  `doc/` (design documents, converted on this site).
- Safety-relevant outputs pass through **firewall** components
  (`AssistFirewall`, `DampingFirewall`, `ReturnFirewall`, `EtDmpFw`) and are
  supervised by the **temporal monitor** (`TmprlMon`) and diagnostics manager.

## Layer sections

- [Application Software](../../asw/) · [Complex Device Drivers](../../cdd/) ·
  [BSW Services](../../services/) · [ECU Abstraction](../../ecuab/) ·
  [MCAL & MCU Drivers](../../mcal/) · [Libraries](../../syslib/) ·
  [Project Integration](../../integration/)
