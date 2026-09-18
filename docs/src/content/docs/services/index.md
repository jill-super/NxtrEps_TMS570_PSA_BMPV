---
title: 'BSW Services'
description: 'AUTOSAR Basic Software services layer: diagnostics, NVRAM, OS/timing, XCP measurement and the Vector MICROSAR BSW stack.'
sidebar: { order: 0 }
---

# BSW Services

AUTOSAR Basic Software services layer: diagnostics, NVRAM, OS/timing, XCP measurement and the Vector MICROSAR BSW stack.

## Modules in this layer

| Module | Component | Summary |
| --- | --- | --- |
| [DiagMgr](./diagmgr/) | Ap_DiagMgr | Central diagnostics manager (core, Dem interface, fail-action handling) — the BSW-services-side fault manager. |
| [GliwaT1](./gliwat1/) | T1 | Gliwa T1 timing/protection executive (third-party) providing deterministic scheduling and timing supervision. |
| [NvMMgr](./nvmmgr/) | Cd_FeeIf | NVRAM manager CDD (Cd_FeeIf): project-specific NvM/Fee integration above the TI FEE driver. |
| [SwProject/DemIf](./swproject-demif/) | Ap_DemIf | Diagnostic-event-manager interface layer between DiagMgr and the Vector Dem. |
| [SwProject/DiagSvc](./swproject-diagsvc/) | Ap_DiagSvc | Diagnostic services (UDS) implementation for tester communication. |
| [SwProject/FaultLog](./swproject-faultlog/) | Ap_FaultLog | Fault-log storage and retrieval for workshop diagnostics. |
| [bsw-stack](./bsw-stack/) | AUTOSAR Can, Il, Tp, Nm, EcuM, Dem, Det, NvM, MemIf, Crc, Dio, Port, Mcu, Gpt, WdgM, Xcp, VStdLib | Vector MICROSAR BSW stack as integrated (CAN driver, Com/IL, Tp, Nm, EcuM, Dem, Det, NvM/MemIf, Crc, Dio/Port/ |
