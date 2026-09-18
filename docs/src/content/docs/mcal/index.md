---
title: 'MCAL & MCU Drivers'
description: 'Microcontroller-abstraction drivers and startup code for the TI TMS570 (DMA, Flash/EEPROM emulation, startup, HALCoGen-derived files).'
sidebar: { order: 0 }
---

# MCAL & MCU Drivers

Microcontroller-abstraction drivers and startup code for the TI TMS570 (DMA, Flash/EEPROM emulation, startup, HALCoGen-derived files).

## Modules in this layer

| Module | Component | Summary |
| --- | --- | --- |
| [Dma](./dma/) | Dma | TMS570 DMA driver: memory-to-memory/peripheral transfers used by ADC and communication paths. |
| [Fee](./fee/) | Fee | TI F021 Flash-EEPROM emulation (FEE) driver used as the NVRAM medium below the memory stack. |
| [Fls](./fls/) | Fls | TI F021 Flash API (binary library plus headers) for TMS570 on-chip Flash access; used by Fee and the flash tes |
| [TMS570_Startup](./tms570_startup/) | TMS570 startup code | TMS570 startup code (TI HALCoGen-derived, Nexteer-adapted): reset, clocks, memory init and vector tables. |
