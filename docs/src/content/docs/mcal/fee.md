---
title: 'Fee'
description: 'TI F021 Flash-EEPROM emulation (FEE) driver used as the NVRAM medium below the memory stack.'
---

# Fee

:::note[Origin: Third-party]
Provided by a silicon/tool vendor (TI HALCoGen/F021 Flash API, Gliwa T1) and adapted for this project. Keep vendor files pristine; put adaptations in clearly marked wrapper files.
:::

## Purpose

TI F021 Flash-EEPROM emulation (FEE) driver used as the NVRAM medium below the memory stack.

Parts of this module (configuration and RTE scaffolding) are generated — edit the generator inputs (`.tt` templates, DaVinci model), not the outputs.

## Module facts

- **AUTOSAR layer:** MCAL & MCU Drivers
- **Full name:** Flash EEPROM Emulation (AUTOSAR memory stack)
- **Repository path:** `Fee`
- **Directory layout:** `doc/`, `generate/`, `include/`, `src/`, `tools/`, `utp/`

## Key files

- `Fee/generate/Fee/T_Fee_Cfg.c`
- `Fee/generate/Fee/T_Fee_Cfg.h`
- `Fee/src/Device_TMS570LS07.c`
- `Fee/src/Device_TMS570LS12.c`
- `Fee/src/fee.c`
- `Fee/src/ti_fee_Info.c`
- `Fee/src/ti_fee_cancel.c`
- `Fee/src/ti_fee_eraseimmediateblock.c`
- `Fee/src/ti_fee_format.c`
- `Fee/src/ti_fee_ini.c`
- `Fee/src/ti_fee_invalidateblock.c`
- `Fee/src/ti_fee_main.c`
- `Fee/src/ti_fee_read.c`
- `Fee/src/ti_fee_readSync.c`
- `Fee/src/ti_fee_shutdown.c`
- `Fee/src/ti_fee_util.c`
- `Fee/src/ti_fee_writeAsync.c`
- `Fee/src/ti_fee_writeSync.c`
- `Fee/utp/contract/Fee/Compiler_Cfg.h`
- `Fee/utp/contract/Fee/Constants.h`

## Dependencies (quoted includes)

- `fee_interface.h`
- `F021.h`
- `Std_Types.h`
- `Device_types.h`
- `Device_TMS570LS07.h`
- `Device_TMS570LS12.h`
- `MemMap.h`
- `ti_fee.h`
- `Fee_Cfg.h`
- `ti_fee_cfg.h`
- `fee_cfg.h`
- `nvm.h`
- `ti_fee_types.h`
- `Device_header.h`

## Generation inputs

DaVinci/generator artefacts shipped with this module (inputs — regenerate, don't hand-edit outputs):

- `Fee/generate/Fee`

## Design documentation (converted)

- [AutoSAR FEE Parameter Configuration](../../modules/mcal/fee/autosar-fee-parameter-configuration/)
- [AutoSAR FEE User Guide](../../modules/mcal/fee/autosar-fee-user-guide/)
- [DataSheet TMS570LS0714](../../modules/mcal/fee/datasheet-tms570ls0714/)
- [DataSheet TMS570LS1227](../../modules/mcal/fee/datasheet-tms570ls1227/)
