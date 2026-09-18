---
title: 'BVDiag Integration Manual'
description: 'Converted design document: BVDiag Integration Manual'
---

> **Source:** `BVDiag/doc/BVDiag_Integration_Manual.docx`  
> **Module:** [BVDiag](../../../../asw/bvdiag/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual - BVDIAG

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

Ap_BVDiag_Cfg.h for checkpoint enables

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

Batt_Volt_f32 from SER

CCLMSAActive_Cnt_lgc (Note : Only required for BMW as per its SER)

### Required Global Data Outputs

Sets BatteryVoltage Diagnostics

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

| <None> |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| B1_BATTVOLTDIAG | This parameter will be turned ON only if customer requires $B1 NTC<br/>STD_ON : Enables NTC $B1 logic<br/>STD_Off : Disables NTC $B1 logic |  |

|  |  |  |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| <None> |  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| <None> |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| None | None | Init |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| BVDiag_Per1 |  | 10ms |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| BVDIAG_START_SEC_VAR_CLEARED_32 |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| <Memmap usuage info> |  |  |

| Block Name |

| --- |

| <None > |

| Block Name |

| --- |

| None |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 13-Sep-13 | NRAR |

|  |  |  |  |
