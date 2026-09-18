---
title: 'DigHwTrqSENT Integration Manual'
description: 'Converted design document: DigHwTrqSENT Integration Manual'
---

> **Source:** `DigHwTrqSENT/doc/DigHwTrqSENT_Integration_Manual.docx`  
> **Module:** [DigHwTrqSENT](../../../../cdd/dighwtrqsent/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual - DigHwTrqSENT

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

Note : Referencing the external components should be avoided in most cases. Only in unavoidable circumstance external components should be refered. Developer should track the references.

### Global Functions(Non RTE) to be provided to Integration Project

< None>

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

Sa_DigHwTrqSENT_Cfg.h for checkpoint enables

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

T1_HwNm_f32 from FDD ES-34B

T2_HwNm_f32 from FDD ES-34B

### Required Global Data Outputs

HwTorque_HwNm_f32

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

| <None> |  |

| Modules | Notes |  |

| --- | --- | --- |

| BC_DIGHWTRQSENT_FAULTINJECTIONPOINT | Fault injection points |  |

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

| DigHwTrqSENT_Init1() | None | Init |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| DigHwTrqSENT_Per1 | After update of T1_HwNm_f32 and T2_HwNm_f32 | 2 ms |

| DigHwTrqSENT_Per2 | None | 4 ms |

| DigHwTrqSENT_Per3 | None | 100 ms |

| DigHwTrqSENT_SCom_ClrTrqTrim | triggered by server invocation for OperationPrototype <ClrTrqTrim> of PortPrototype <DigHwTrqSENT_SCom> | On event |

| DigHwTrqSENT_SCom_SetTrqTrim | triggered by server invocation for OperationPrototype <SetTrqTrim> of PortPrototype <DigHwTrqSENT_SCom> | On event |

|  |  |  |

|  |  |  |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| DIGHWTRQSENT_START_SEC_VAR_CLEARED_32 |  |  |

| DIGHWTRQSENT_START_SEC_VAR_CLEARED_UNSPECIFIED |  |  |

| DIGHWTRQSENT_START_SEC_VAR_SAVED_ZONEH_32 |  | Zone H EEPROM |

| Feature | RAM | ROM |

| --- | --- | --- |

| <Memmap usuage info> |  |  |

| Block Name |

| --- |

| <None > |

| Block Name |

| --- |

| DigHwTrqSENTTrim |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 01-Jul-13 | KMC |

| 2 | Updated per Design Review CR 11619 – Corrected Runnable Names – Removed “Sa_” from Init, Per functions | 03-Mar-14 | SB |

| 3 | Turned on track changes and corrected rev 2 changes | 01-Apr-14 | SB |

| 4 | Implemented ES04C Rev 006 | 09-Jun-14 | SB |

|  |  |  |  |
