---
title: 'PSATA Integration Manual'
description: 'Converted design document: PSATA Integration Manual'
---

> **Source:** `PSATA/doc/PSATA_Integration Manual.docx`  
> **Module:** [PSATA](../../../../asw/psata/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

### Integration Manual

### For

### CF14 PSA Torque Arbitrator

### VERSION: 1.0

### DATE: 10-Mar-2015

### Prepared By:

### Sankardu Varadapureddi,

### Nexteer Automotive,

### Saginaw, MI, USA

### Revision History

### Table of Contents

1	Abbrevations And Acronyms	4

2	References	5

3	Dependencies	6

3.1	SWCs	6

3.2	Global Functions(Non RTE) to be provided to Integration Project	6

4	Configuration REQUIREMeNTS	7

4.1	Build Time Config	7

4.2	Configuration Files to be provided by Integration Project	7

4.3	Da Vinci Parameter Configuration Changes	7

4.4	DaVinci Interrupt Configuration Changes	7

4.5	Manual Configuration Changes	7

5	Integration  DATAFLOW REQUIREMENTS	8

5.1	Required Global Data Inputs	8

5.2	Required Global Data Outputs	8

5.3	Specific Include Path present	8

6	Runnable Scheduling	9

7	Memory Map REQUIREMENTS	10

7.1	Mapping	10

7.2	Usage	10

7.3	Non  RTE NvM Blocks	10

7.4	RTE NvM Blocks	10

8	Compiler Settings	11

8.1	Preprocessor MACRO	11

8.2	Optimization Settings	11

9	Appendix	12

## Abbrevations And Acronyms

## References

This section lists the title & version of all the documents that are referred for development of this document

## Dependencies

### SWCs

### Global Functions(Non RTE) to be provided to Integration Project

None

## Configuration REQUIREMeNTS

### Build Time Config

### Configuration Files to be provided by Integration Project

None

### Da Vinci Parameter Configuration Changes

### DaVinci Interrupt Configuration Changes

### Manual Configuration Changes

## Integration  DATAFLOW REQUIREMENTS

### Required Global Data Inputs

HwTorque_HwNm_f32

PosSrvoCmd_MtrNm_f32

PosSrvoEnable_Cnt_lgc

VehicleSpeed_Kph_f32

### Required Global Data Outputs

OpTrqOv_MtrNm_f32

PosSrvoNTC_Cnt_lgc

### Specific Include Path present

No

## Runnable Scheduling

This section specifies the required runnable scheduling.

### .

## Memory Map REQUIREMENTS

### Mapping

* Each …START_SEC… constant is terminated by a …STOP_SEC… constant as specified in the AUTOSAR Memory Mapping requirements.

### Usage

Table 1: ARM Cortex R4 Memory Usage

### Non  RTE NvM Blocks

### RTE NvM Blocks

## Compiler Settings

### Preprocessor MACRO

None.

### Optimization Settings

None

## Appendix

| Sl. No. | Description | Author | Version | Date |

| --- | --- | --- | --- | --- |

| 1 | Initial version | Sankardu Varadapureddi | 1.0 | 10-Mar-2015 |

|  |  |  |  |  |

| Abbreviation | Description |

| --- | --- |

| DFD | Design functional diagram |

| MDD | Module design Document |

|  |  |

|  |  |

| Sr. No. | Title | Version |

| --- | --- | --- |

| 1 | MDD Guidelines | 1.3 |

| 2 | Software Naming Conventions | 1.2 |

| 3 | Software Design and Coding Standards | 2.1 |

| 4 | FDD  - CF14 PSA Torque Arbitrator | 1.1.0 |

| 5 | Integration Manual Template.doc | 1.2 |

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

| PSATA_Init1 | None | RTE( Init) |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| PSATA_Per1 | None | RTE (2ms) |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| PSATA_START_SEC_VAR_CLEARED_BOOLEAN<br/>PSATA _START_SEC_VAR_CLEARED_16<br/>PSATA _START_SEC_VAR_CLEARED_32<br/>PSATA_START_SEC_VAR_CLEARED_UNSPECIFIED |  |  |

|  |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| <Memmap usuage info> |  |  |

| Block Name |

| --- |

| None |

| Block Name |

| --- |

| None |
