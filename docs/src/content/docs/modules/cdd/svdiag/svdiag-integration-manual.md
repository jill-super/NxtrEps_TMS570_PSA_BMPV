---
title: 'SVDiag Integration Manual'
description: 'Converted design document: SVDiag Integration Manual'
---

> **Source:** `SVDiag/doc/SVDiag_Integration_Manual.docx`  
> **Module:** [SVDiag](../../../../cdd/svdiag/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual –

Table of Contents

1	Dependencies	2

1.1	SWCs	2

1.2	Functions to be provided to Integration Project	2

2	Configuration	3

2.1	Build Time Config	3

2.2	Configuration Files to be provided by Integration Project	3

2.2.1	Da Vinci Config generation	3

2.2.2	Manual Configuration Changes	3

3	Integration	4

3.1	Required Global Data Inputs	4

3.2	Optional Global Data Inputs	4

3.3	Specific Include Path present	4

4	Runnable Scheduling	5

5	Memory Mapping	6

5.1	Mapping	6

5.2	Usage	6

5.3	NvM Blocks	6

6	Compiler Settings	6

6.1	Preprocessor MACRO	6

6.2	Optimization Settings	6

7	Revision Control Log	7

## Dependencies

### SWCs

### Global Functions(Non RTE) to be provided to Integration Project

< Global function (except the ones that are defined in RTE modules) that is defined in this component but used by other function>

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

<Configuration file that will generated from this components that will require Da Vinci Config generation or manual generation. Describe each parameter >

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

ExpectedOnTimeA_Cnt_u32

ExpectedOnTimeB_Cnt_u32

ExpectedOnTimeC_Cnt_u32

LRPRCorrectedMtrPosCaptured_Rev_f32

LRPRModulationIndexCaptured_Uls_f32

LRPRPhaseadvanceCaptured_Cnt_s16

MeasuredOnTimeA_Cnt_u32

MeasuredOnTimeB_Cnt_u32

MeasuredOnTimeC_Cnt_u32

MotorVelMRFUnfiltered_MtrRadpS_f32

MtrElecMechPolarity_Cnt_s08

PDActivateTest_Cnt_lgc

MtrDrvrInitStart_Cnt_lgc

VswitchClosed_Cnt_lgc

### Required Global Data Outputs

SVDiag_LowPhReasErrorAcc_Cnt_u16

SVDiag_HighResPhsReasDisable_u8

SVDiag_LowResPhsReasDisable_u8

SVDiag_MtrDrvInitComp_Cnt_lgc

SVDiag_GateDriveFltAcc_Cnt_u16

SVDiag_GenGateDriveFltAcc_Cnt_u16

SVDiag_OnStateFltAcc_Cnt_u16

### Specific Include Path present

None

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

| None |  |

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| None |  |  |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| None |  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| None |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| DigPhsReasDiag_Init | Executed once after the RTE is started before first call of MtrDrvDiag_Per1 | RTE (at Startup) |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| DigPhsReasDiag_Per1 | Not in OFF, DISABLE, or WARMINIT modes | Rte 2ms task |

| DigPhsReasDiag_Trans1 | In OPERATE mode | On entering mode |

| MtrDrvDiag_Per1 | Not in DISABLE or OFF modes | Rte 2ms task |

| MtrDrvDiag_Per2 | Not in OPERATE or WARMINIT modes | Rte 2ms task |

| MtrDrvDiag_Trns1 | In WARMINIT mode | On entering mode |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| < Memory mapping Info> |  |  |

| DIGPHSREASDIAG_START_SEC_VAR_CLEARED_32 |  |  |

| DIGPHSREASDIAG_START_SEC_VAR_CLEARED_BOOLEAN |  |  |

| DIGPHSREASDIAG_START_SEC_VAR_CLEARED_16 |  |  |

| DIGPHSREASDIAG_START_SEC_VAR_CLEARED_8 |  |  |

| MTRDRVDIAG_START_SEC_VAR_CLEARED_32 |  |  |

| MTRDRVDIAG_START_SEC_VAR_CLEARED_16 |  |  |

| MTRDRVDIAG_START_SEC_VAR_CLEARED_BOOLEAN |  |  |

| MTRDRVDIAG_START_SEC_VAR_CLEARED_UNSPECIFIED |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| Full |  |  |

| Block Name |

| --- |

| None |

| Block Name |

| --- |

| None |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 3-Oct-13 | VT |
