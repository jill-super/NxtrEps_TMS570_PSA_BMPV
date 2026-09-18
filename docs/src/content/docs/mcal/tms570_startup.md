---
title: 'TMS570_Startup'
description: 'TMS570 startup code (TI HALCoGen-derived, Nexteer-adapted): reset, clocks, memory init and vector tables.'
---

# TMS570_Startup

:::note[Origin: Third-party]
Provided by a silicon/tool vendor (TI HALCoGen/F021 Flash API, Gliwa T1) and adapted for this project. Keep vendor files pristine; put adaptations in clearly marked wrapper files.
:::

## Purpose

TMS570 startup code (TI HALCoGen-derived, Nexteer-adapted): reset, clocks, memory init and vector tables.

## Module facts

- **AUTOSAR layer:** MCAL & MCU Drivers
- **Full name:** TMS570 Startup Code (reset, clocks, vectors)
- **Repository path:** `TMS570_Startup`
- **Directory layout:** `doc/`, `include/`, `src/`, `tools/`, `utp/`

## Key files

- `TMS570_Startup/src/AppStartup.c`
- `TMS570_Startup/src/BootStartup.c`
- `TMS570_Startup/src/ResetCause.c`
- `TMS570_Startup/src/errata_SSWF021_45.c`
- `TMS570_Startup/src/prooftestv02.c`
- `TMS570_Startup/src/prooftestv02.het`
- `TMS570_Startup/src/sys_startup.c`
- `TMS570_Startup/utp/contract/Compiler_Cfg.h`
- `TMS570_Startup/utp/contract/MemMap.h`
- `TMS570_Startup/utp/contract/appinit_cfg.h`
- `TMS570_Startup/utp/contract/startup_cfg.h`
- `TMS570_Startup/utp/contract/std_nhet.h`
- `TMS570_Startup/utp/contract/uDiag.h`

## Dependencies (quoted includes)

- `Platform_Types.h`
- `Compiler.h`
- `errata_SSWF021_45_defs.h`
- `std_nhet.h`
- `Std_Types.h`

## Design documentation (converted)

- [TMS570 Startup BootStartup MDD](../../modules/mcal/tms570_startup/tms570-startup-bootstartup-mdd/)
- [TMS570 Startup FiqIntVect MDD](../../modules/mcal/tms570_startup/tms570-startup-fiqintvect-mdd/)
- [TMS570 Startup Integration Manual](../../modules/mcal/tms570_startup/tms570-startup-integration-manual/)
- [TMS570 Startup SysCore MDD](../../modules/mcal/tms570_startup/tms570-startup-syscore-mdd/)
- [TMS570 Startup SysStartup MDD](../../modules/mcal/tms570_startup/tms570-startup-sysstartup-mdd/)
- [TMS570 Startup errata SSWF021 45 MDD](../../modules/mcal/tms570_startup/tms570-startup-errata-sswf021-45-mdd/)
- [spna106a](../../modules/mcal/tms570_startup/spna106a/)
