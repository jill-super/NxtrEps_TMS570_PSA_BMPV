---
title: 'MtrCntrl Integration Manual'
description: 'Converted design document: MtrCntrl Integration Manual'
---

> **Source:** `MtrCtrl_CM/doc/MtrCntrl_Integration_Manual.docx`  
> **Module:** [MtrCtrl_CM](../../../../asw/mtrctrl_cm/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual -- MtrCntrl

Table of Contents

1	Dependencies	2

1.1	SWCs	2

1.2	Configuration Files to be provided by Integration Project	2

1.3	Functions to be provided by Integration Project	2

2	Configuration	3

2.1	Build Time Config	3

2.2	Generator Config	3

3	Integration	4

3.1	Global Data	4

3.2	Component Conflicts	4

3.3	Include Path	4

3.4	ADC2 Changes	4

3.5	Configurator Changes	4

3.5.1	DIO	4

3.5.2	Port	5

4	Runnable Scheduling	6

5	Memory Mapping	7

5.1	Mapping	7

5.2	Usage	7

6	Revision Control Log	8

## Dependencies

### SWCs

### Configuration Files to be provided by Integration Project

MtrCtrl_Cfg.h

### Functions to be provided to Integration Project

PICurrCntrl_Per1()

TrqCogCancRefPer1()

## Configuration

### Build Time Config

### Generator Config

## Integration

### Global Data

The global symbols mapping done in MtrCtrl_Cfg.h.

### Component Conflicts

None

### Include Path

The “include” directory of this SWC needs to be included in the integration project include search path.

.

### Configurator Changes

None

## Runnable Scheduling

This section specifies the required runnable scheduling.

*Note: In motor control ISR include Ap_MtrCtrl.h instead of CDD_Func.h

Proper Initialization of input signals should occur before running each function for the first time.  (CurrParamComp_Init).

## Memory Mapping

### Mapping

* Each …START_SEC… constant is terminated by a …STOP_SEC… constant as specified in the AUTOSAR Memory Mapping requirements.

### Usage

### Table 1: ARM Cortex R4 Memory Usage

## Revision Control Log

| Module | Required Feature |

| --- | --- |

|  |  |

| Modules | Notes |  |

| --- | --- | --- |

| PICurrentCntrl<br/>TrqCanc | Optimization level greater than 3 |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| None |  |  |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| TrqCogCancRefPer1() | Must be placed in the motor control ISR, after MtrPos | Cyclic (ISR) |

| PICurrCntrl_Per1() | Must be placed in the motor control ISR after TrqCogCancRefPer1() | Cyclic (ISR) |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

|  |  |  |

|  |  |  |

| QuadDet_Per1 | Must run after TrqReasonable Diagnostics | RTE (2ms) |

| CurrCmd_Per1 | Must run after  QuadDet | RTE (2ms) |

| TrqCanc_Per1 | Must run after CurrCmd_Per1 | RTE (2ms) |

| PICurrCntrl_Per2() | Must be placed after TrqCanc_Per1 | RTE (2ms) |

| CurrParamComp_Per1() | Must be placed after PICurrCntrl_Per2 | RTE (2ms) |

| PeakCurrEst_Per1() | Must be placed after PICurrCntrl_Per2 | RTE (2ms) |

|  |  |  |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| RTE Memory mapping |  |  |

|  |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| Full driver |  |  |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 25-Mar-13 | Selva |

|  |  |  |  |

|  |  |  |  |
