---
title: 'GliwaT1'
description: 'Gliwa T1 timing/protection executive (third-party) providing deterministic scheduling and timing supervision.'
---

# GliwaT1

:::note[Origin: Third-party]
Provided by a silicon/tool vendor (TI HALCoGen/F021 Flash API, Gliwa T1) and adapted for this project. Keep vendor files pristine; put adaptations in clearly marked wrapper files.
:::

## Purpose

Gliwa T1 timing/protection executive (third-party) providing deterministic scheduling and timing supervision.

## Module facts

- **AUTOSAR layer:** BSW Services
- **Full name:** Gliwa T1 timing executive
- **Repository path:** `GliwaT1`
- **Directory layout:** `doc/`, `include/`, `src/`, `tools/`, `utp/`

## Key files

- `GliwaT1/src/T1_AppInterface.c`
- `GliwaT1/src/T1_config.c`
- `GliwaT1/utp/Example_Integration_Specific/T1_AppInterface_Cfg.c`
- `GliwaT1/utp/Example_Integration_Specific/T1_AppInterface_Cfg.h`
- `GliwaT1/utp/Example_Tools_GliwaT1/Overlay/GM_C1XX_EPS_TMS570/SwProject/Source/BSW/Can/can_drv.c`
- `GliwaT1/utp/Example_Tools_GliwaT1/Overlay/GM_C1XX_EPS_TMS570/SwProject/Source/BSW/Gpt/Gpt_Irq.c`
- `GliwaT1/utp/Example_Tools_GliwaT1/Overlay/GM_C1XX_EPS_TMS570/SwProject/Source/BSW/Os/osektask.c`

## Dependencies (quoted includes)

- `T1_AppInterface.h`
- `T1_AppInterface_Cfg.h`
- `T1_targetSpecifics.h`
- `T1_MemMap.h`
- `T1_baseInterface.h`
- `T1_scopeInterface.h`
- `sys_common.h`

## Design documentation (converted)

- [GliwaT1 IntegrationManual](../../modules/services/gliwat1/gliwat1-integrationmanual/)
