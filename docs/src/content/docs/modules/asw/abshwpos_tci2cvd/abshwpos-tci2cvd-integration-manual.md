---
title: 'AbsHwPos TcI2cVd Integration Manual'
description: 'Converted design document: AbsHwPos TcI2cVd Integration Manual'
---

> **Source:** `AbsHwPos_TcI2cVd/doc/AbsHwPos_TcI2cVd_Integration_Manual.docx`  
> **Module:** [AbsHwPos_TcI2cVd](../../../../asw/abshwpos_tci2cvd/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual – Absolute Handwheel Position – Turns Counter, I2C, and Vehicle Dynamics

Table of Contents

1	Dependencies	2

1.1	SWCs	2

1.2	Global Functions(Non RTE) to be provided to Integration Project	2

2	Configuration	3

2.1	Build Time Config	3

2.2	Configuration Files to be provided by Integration Project	3

2.2.1	Da Vinci Parameter Configuration Changes	3

2.2.2	DaVinci Interrupt Configuration Changes	3

2.2.3	Manual Configuration Changes	3

3	Integration	4

3.1	Required Global Data Inputs	4

3.2	Required Global Data Outputs	4

3.3	Specific Include Path present	4

4	Runnable Scheduling	5

5	Memory Mapping	6

5.1	Mapping	6

5.2	Usage	6

5.3	Non  RTE NvM Blocks	6

5.4	RTE NvM Blocks	6

6	Compiler Settings	6

6.1	Preprocessor MACRO	6

6.2	Optimization Settings	6

7	Revision Control Log	7

## Dependencies

### SWCs

Note : Referencing the external components should be avoided in most cases. Only in unavoidable circumstance external components should be refered. Developer should track the references.

### Global Functions(Non RTE) to be provided to Integration Project

None

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

Ap_AbsHwPos_Cfg.h   (generated using Ap_AbsHwPos_Cfg.h.tt)

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

CumMechMtrPosCRF_Deg_f32

AlignedCumMechMtrPosCRF_Deg_f32

TurnsCntrValidity_Cnt_u08

I2CHwAbsPos_HwDeg_f32

I2CHwAbsPosValid_Cnt_lgc

_HwDeg_f32

_Uls_f32

ComplError_HwDeg_f32

DiagStatusHwPosReducedPerf_Cnt_lgc

ManufMode_Cnt_enum

### Required Global Data Outputs

HandwheelPosition_HwDeg_f32

HandwheelAuthority_Uls_f32

RelHwPos_HwDeg_f32

HwPosSource_Cnt_u16

SrlComHwPos_HwDeg_f32

SrlComHwPosStatus_Cnt_u16

### Specific Include Path present

No

## Runnable Scheduling

This section specifies the required runnable scheduling.

### .

## Memory Mapping

### Mapping

* Each …START_SEC… constant is terminated by a …STOP_SEC… constant as specified in the AUTOSAR Memory Mapping requirements.

### Usage

Table 1: ARM Cortex R4 Memory Usage

### Non  RTE NvM Blocks

Note : Size of the NVM block if configured in developer

### RTE NvM Blocks

Note : Size of the NVM block if configured in developer

## Compiler Settings

### Preprocessor MACRO

<Define all the preprocessor Macros needed and conditions when needed>.

### Optimization Settings

<Define Optimization levels that are needed and conditions when needed>.

## Revision Control Log

| Module | Required Feature |

| --- | --- |

| <Name of SWC> | <Addition of global data, function*. |

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| AbsHwPosGeneral\AbsHwPosCPEnable | Enable checkpoints if needed | AbsHwPos |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| <None> |  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| <None> |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| AbsHwPos_Init1 | Called from RTE before first call of periodic function | RTE at init |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| AbsHwPos_Per1 | Call before 2ms periodic that uses RelHwPos_HwDeg_f32 | RTE 2 ms |

| AbsHwPos_Per2 | Call after 2ms periodic that outputs VDHwPos_HwDeg_f32 | RTE 2 ms |

| AbsHwPos_Per3 | None | RTE 4 ms |

| AbsHwPos_Per4 | None | RTE 10 ms |

| AbsHwPos_SCom_CustSetTrim | Common Manufacturing | On event |

| AbsHwPos_SCom_CustClrTrim | Common Manufacturing | On event |

| AbsHwPos_SCom_NxtSetTrim | Common Manufacturing | On event |

| AbsHwPos_SCom_NxtClearTrim | Common Manufacturing | On event |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| ABSHWPOS_START_SEC_VAR_CLEARED_UNSPECIFIED |  |  |

| ABSHWPOS_START_SEC_VAR_CLEARED_BOOLEAN |  |  |

| ABSHWPOS_START_SEC_VAR_CLEARED_16 |  |  |

| ABSHWPOS_START_SEC_VAR_CLEARED_32 |  |  |

| RTE_START_SEC_AP_ABSHWPOS_APPL_CODE |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| <Memmap usuage info> |  |  |

| Block Name |

| --- |

| <None > |

| Block Name |

| --- |

| EOLVehCntrOffset |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1.0 | Initial version | 26-Nov-13 | KMC |

|  |  |  |  |
