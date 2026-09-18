---
title: 'VehDyn Integration Manual'
description: 'Converted design document: VehDyn Integration Manual'
---

> **Source:** `VehDyn/doc/VehDyn_Integration_Manual.docx`  
> **Module:** [VehDyn](../../../../asw/vehdyn/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual -- VehDyn

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

< Global function (except the ones that are defined in RTE modules) that is defined in this component but used by other function>

None

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

Ap_VehDyn_Cfg.h   (generated using Ap_VehDyn_Cfg.h.tt)

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

VehicleSpeed_Kph_f32

HwTorque_HwNm_f32

TorqueCmdCRF_MtrNm_f32

VehicleSpeedValid_Cnt_lgc

MotorVelCRF_MtrRadpS_f32

RelHwPos_HwDeg_f32

CcwEOT_HwDeg_f32

CwEOT_HwDeg_f32

HwAuth_Uls_f32

HandwheelPosition_HwDeg_f32

MechMtrPos_Rev_f32

SrlHwAgVld_Cnt_lgc

SrlHwAg_HwDeg_f32

### Required Global Data Outputs

SensorlessHwAuth_Uls_f32

SensorlessHwPos_HwDeg_f32

### Specific Include Path present

< No >

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

| None |  |

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| VehDynGeneral/VehDynCPEnable | Enable checkpoints if needed | VehDyn |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| None |  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| None |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| VehDyn_Init1 | Called from RTE before first call of periodic function | RTE at init |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| VehDyn_Per1 | Should be called after the 2ms periodic that outputs RelHwPos and before the 2ms periodic that uses VDHwPos and VDAuthority | RTE 2 ms |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| VehDyn_Trns1 | triggered on entering of Mode <OFF> of ModeDeclarationGroupPrototype <Mode> of PortPrototype <SystemState> | RTE at shutdown |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| VEHDYN_START_SEC_VAR_CLEARED_UNSPECIFIED |  |  |

| VEHDYN_START_SEC_VAR_CLEARED_BOOLEAN |  |  |

| RTE_START_SEC_AP_VEHDYN_APPL_CODE |  |  |

| VEHDYN_START_SEC_VAR_CLEARED_32 |  |  |

| VEHDYN_START_SEC_VAR_CLEARED_8 |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| <Memmap usage info> |  |  |

| Block Name |

| --- |

| None |

| Block Name |

| --- |

| VehDynReset |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 19-Aug-13 | KMC |

| 2 | Updated per SF42 - VCDMotPos rev 002 | 21-Aug-14 | SB |

| 3 | Updated to SF42 – VCDMotPos v004 | 16-Jan-15 | SB |

| 4 | Updated to SF42 – VCDMotPos v006 | 13-Aug-15 | JK |

| 5 | New MemMap section added and Input name change | 15-Dec-15 | SB |

|  |  |  |  |
