---
title: 'Libraries & Shared Code'
description: 'Shared libraries, compiler/platform abstraction, diagnostic-service helpers and RTE wrapper utilities used across the project.'
sidebar: { order: 0 }
---

# Libraries & Shared Code

Shared libraries, compiler/platform abstraction, diagnostic-service helpers and RTE wrapper utilities used across the project.

## Modules in this layer

| Module | Component | Summary |
| --- | --- | --- |
| [CMS_Common](./cms_common/) | EPS_DiagSrvcs | Shared calibration-manufacturing-service (CMS) headers: common XCP/ISO diagnostic-service data definitions. |
| [NxtrLib](./nxtrlib/) | NxtrLib | In-house fixed-point/math library: filters, interpolation, atan2/SinCos, checksums, system time. |
| [StdDef](./stddef/) | StdDef | AUTOSAR platform/compiler abstraction (Std_Types, Platform_Types, Compiler) for the TI TMS570 toolchain. |
| [SwProject/CMS_PSA](./swproject-cms_psa/) | AUTOSAR EPS_DiagSrvcs_* (customised) | PSA calibration-manufacturing services built on Vector XCP/ISO artefacts (project-customised). |
| [SwProject/Header](./swproject-header/) | — | Project header/scheduler integration files (BSW scheduler, global headers). |
| [SwProject/NtWrap](./swproject-ntwrap/) | NtWrap | RTE wrapper utilities decoupling application code from generated RTE APIs for unit testing. |
