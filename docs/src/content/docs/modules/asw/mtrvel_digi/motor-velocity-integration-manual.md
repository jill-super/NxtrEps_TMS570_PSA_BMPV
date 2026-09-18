---
title: 'Motor Velocity Integration Manual'
description: 'Converted design document: Motor Velocity Integration Manual'
---

> **Source:** `MtrVel_Digi/doc/Motor Velocity_Integration_Manual.docx`  
> **Module:** [MtrVel_Digi](../../../../asw/mtrvel_digi/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual –Motor Velocity

Table of Contents

1	Dependencies	2

1.1	SWCs	2

1.2	Functions to be provided to Integration Project	2

2	Configuration	3

2.1	Build Time Config	3

2.2	Configuration Files to be provided by Integration Project	3

2.2.1	Da Vinci Config Configuration Changes	3

2.2.2	Manual Configuration Changes	3

3	Integration	4

3.1	Required Global Data Inputs	4

3.2	Specific Include Path present	4

4	Runnable Scheduling	5

5	Memory Mapping	5

5.1	Mapping	5

5.2	Usage	6

5.3	RTE NvM Blocks	6

5.4	Non RTE NvM Blocks	6

6	Compiler Settings	6

6.1	Preprocessor MACRO	6

6.2	Optimization Settings	6

7	Revision Control Log	7

## Dependencies

### SWCs

Note : Referencing the external components should be avoided in most cases. Only in unavoidable circumstance external components should be refered. Developer should track the references.

### Functions to be provided to Integration Project

MtrVel3_Per1

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

MtrVel_Cfg.h (Refer MtrVel_Cfg_Template.h in tools folder)

#### Da Vinci Config Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

Motor Position calculated in  Motor Control ISR should be used.  Motor Position Non RTE inputs should be processed at the same time rate of Motor Velocity Buffering Periodic

MtrVel_Read_MechMtrPos1TimeStamp_uS_u32   /* MtrPos Timestamp Calculated in 0.062  mSec should be used.  Motor Pos should be processed at the same time rate of Motor Velocity 3 periodic 1*/

MtrVel_Read_MechMtrPos1_Rev_u0p16   /* MtrPos Calculated in 0.062  mSec should be used.  Motor Pos should be processed at the same time rate of Motor Velocity 3 periodic 1  */

### Specific Include Path present

Yes

## Runnable Scheduling

This section specifies the required runnable scheduling.

Note :  The Scheduling of the periodic between MtrVel_Per1, MtrVel_Per2, MtrVel2_Per1 should take care of the following constraints. MtrVel_Per1 and MtrVel_Per2 should reside on the same application . MtrVel2_Per1 should reside on the separate application.

MtrVel_Per1output is used by MtrVel2_Per1 and MtrVel_Per2

MtrVel2_Per1 Output is used by MtrVel_Per2

Hence scheduler should schedule in such a way that there is consistent set of data are used as inputs for MtrVel_Per2.

## Memory Mapping

### Mapping

* Each …START_SEC… constant is terminated by a …STOP_SEC… constant as specified in the AUTOSAR Memory Mapping requirements.

### Usage

Table 1: ARM Cortex R4 Memory Usage

### RTE NvM Blocks

Note : Size of the NVM block if configured in developer

### Non RTE NvM Blocks

Note : Size of the NVM block if configured in developer

## Compiler Settings

### Preprocessor MACRO

None

### Optimization Settings

None

## Revision Control Log

| Module | Required Feature |

| --- | --- |

|  |  |

|  |  |

|  |  |

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| None |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| None |  |  |

| D_MTRVELOSBUFSZ_CNT_U08 | D_MTRVELOSBUFSZ_CNT_U08” is defined  as Cal “k_BuffSize_Cnt” in SF40AB <br/>Confirm with the Program being integrated on for the value that needs to be configured for this constant |  |

|  |  |  |

|  |  |  |

|  |  |  |

|  |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| MtrVel3_Init1 | Once | RTE |

| MtrVel_Init | Once | RTE |

| MtrVel2_Init | Once | RTE |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| MtrVel3_Per1 | After DigMSBCorrPer1 Motor ISR periodic (ES51 ) | Motor Control ISR |

| MtrVel_Per1 | After DigMSBCorr Per2 periodic (ES51 ) | RTE(2mS) |

| MtrVel_Per2 |  | RTE(2mS) |

| MtrVel2_Per1 |  | RTE(2mS) |

| MtrVel2_Per2 |  | RTE(2mS) |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| MTRVEL_START_SEC_VAR_CLEARED_32 |  |  |

| MTRVEL_START_SEC_VAR_CLEARED_16 |  |  |

| MTRVEL_START_SEC_VAR_CLEARED_8 |  |  |

| MTRVEL2_START_SEC_VAR_CLEARED_32 |  |  |

| MTRVEL2_START_SEC_VAR_CLEARED_16 |  |  |

| MTRVEL2_START_SEC_VAR_CLEARED_8 |  |  |

| MTRVEL3_START_SEC_VAR_CLEARED_16 |  |  |

| MTRVEL3_START_SEC_VAR_CLEARED_8 |  |  |

| MTRVEL3_START_SEC_VAR_CLEARED_32 |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

|  |  |  |

| Block Name |

| --- |

| None |

| Block Name |

| --- |

| None |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 1-Aug-13 | nzt9hv |

|  |  |  |  |
