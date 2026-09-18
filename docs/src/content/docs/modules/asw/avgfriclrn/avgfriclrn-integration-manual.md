---
title: 'AvgFricLrn Integration Manual'
description: 'Converted design document: AvgFricLrn Integration Manual'
---

> **Source:** `AvgFricLrn/doc/AvgFricLrn_Integration_Manual.docx`  
> **Module:** [AvgFricLrn](../../../../asw/avgfriclrn/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual –AvgFricLrn

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

< None>

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

Ap_AvgFricLrn_Cfg.h for checkpoint enable

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

CRFMtrTrq_MtrNm_f32

DefeatFricLearning_Cnt_lgc

HwAng_HwDeg_f32

HwPosAuthority_Uls_f32

HwTrq_HwNm_f32

HwVel_HwRadpS_f32

LatAcc_g_f32

Temperature_DegC_f32

VehSpd_Kph_f32

VehicleSpeedValid_Cnt_lgc

### Required Global Data Outputs

EstFric_HwNm_f32

FricOffset_HwNm_f32

SatEstFric_HwNm_f32

### Specific Include Path present

No

## Runnable Scheduling

This section specifies the required runnable scheduling.

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

| <None> |  |  |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| <None> |  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| <None> |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| AvgFricLrn_Init1() | None | Init |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| AvgFricLrn_Per1 | triggered on TimingEvent | 10ms |

| AvgFricLrn_SCom_GetEOLFric | triggered by server invocation for OperationPrototype <GetEOLFric> of PortPrototype <AvgFricLrn_SCom> |  |

| AvgFricLrn_SCom_GetOffsetOutputDefeat | triggered by server invocation for OperationPrototype <GetOffsetOutputDefeat> of PortPrototype <AvgFricLrn_SCom> |  |

| AvgFricLrn_SCom_GetSelect | triggered by server invocation for OperationPrototype <GetSelect> of PortPrototype <AvgFricLrn_SCom> |  |

| AvgFricLrn_SCom_InitLearnedTables | triggered by server invocation for OperationPrototype <InitLearnedTables> of PortPrototype <AvgFricLrn_SCom> |  |

| AvgFricLrn_SCom_ResetToZero | triggered by server invocation for OperationPrototype <ResetToZero> of PortPrototype <AvgFricLrn_SCom> |  |

| AvgFricLrn_SCom_SetEOLFric | triggered by server invocation for OperationPrototype <SetEOLFric> of PortPrototype <AvgFricLrn_SCom> |  |

| AvgFricLrn_SCom_SetOffsetOutputDefeat | triggered by server invocation for OperationPrototype <SetOffsetOutputDefeat> of PortPrototype <AvgFricLrn_SCom> |  |

| AvgFricLrn_SCom_SetSelect | triggered by server invocation for OperationPrototype <SetSelect> of PortPrototype <AvgFricLrn_SCom> |  |

| AvgFricLrn_Trns1 | triggered on entering of Mode <OFF> of ModeDeclarationGroupPrototype <Mode> of PortPrototype <SystemState> |  |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| AVGFRICLRN_START_SEC_VAR_CLEARED_32 |  |  |

| AVGFRICLRN_START_SEC_VAR_CLEARED_BOOLEAN |  |  |

| AVGFRICLRN_START_SEC_VAR_CLEARED_UNSPECIFIED |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| <Memmap usuage info> |  |  |

| Block Name |

| --- |

| <NVM block used Non RTE functions > |

| Block Name |

| --- |

| <NVM block used in RTE functions > |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 12-May-14 | SB |
