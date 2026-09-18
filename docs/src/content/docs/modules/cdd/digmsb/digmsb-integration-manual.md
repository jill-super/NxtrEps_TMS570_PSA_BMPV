---
title: 'DigMSB Integration Manual'
description: 'Converted design document: DigMSB Integration Manual'
---

> **Source:** `DigMSB/doc/DigMSB_Integration_Manual.docx`  
> **Module:** [DigMSB](../../../../cdd/digmsb/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

### Integration Manual

### For

### DigMSB (ES-50A)

### VERSION: 8.0

### DATE: 02-06-2015

### Prepared By:

### Rijvi Ahmed

### Nexteer Automotive,

### Saginaw, MI, USA

Location: The official version of this document is stored in the Nexteer Configuration Management System.

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

Note : Referencing the external components should be avoided in most cases. Only in unavoidable circumstance external components should be referred. Developer should track the references.

Note:  Integration of DigMSBSigCorr component is required  if using DigMSB component of version 5 or less. DigMSBCorr Component is not needed after the integration DigMSB v6 or more.

### Global Functions(Non RTE) to be provided to Integration Project

DigMSB_Per1

## Configuration REQUIREMeNTS

### Build Time Config

### Configuration Files to be provided by Integration Project

DigMSB_Cfg.h ( Refer DigMSB_Cfg_Template.h in tools folder)

(Data synchronization must be provided at the integration level between 2 ms periodic and Motor Control ISR Periodics)

### Da Vinci Parameter Configuration Changes

### DaVinci Interrupt Configuration Changes

### Manual Configuration Changes

## Integration  DATAFLOW REQUIREMENTS

### Required Global Data Inputs

### Required Global Data Outputs

MechMtrPos1_Rev_u0p16

SysCMechMtrPos1_Rev_u0p16

SysCorrectedElecMtrPos_Rev_u0p16

MechMtrPos1TimeStamp_uSec_u32

MechMtrPos2TimeStamp_uSec_u32

CorrectedElecMtrPos_Rev_u0p16

UncorrMechMtrPos1_Rev_u0p16

CumMechMtrPos_Rev_s15p16

Die1RxError_Cnt_u16

Die2RxError_Cnt_u16

Die1RxRevCtr_Cnt_u16

Die2RxRevCtr_Cnt_u16

Die1RxMtrPos_Cnt_u16

Die2RxMtrPos_Cnt_u16

RxMtrPos1ParityAccum_Cnt_u16

RxMtrPos1UnderVoltgFltAccum_Cnt_u16

### Specific Include Path present

Yes

## Runnable Scheduling

This section specifies the required runnable scheduling.

### .

## Memory Map REQUIREMENTS

### Mapping

* Each …START_SEC… constant is terminated by a …STOP_SEC… constant as specified in the AUTOSAR Memory Mapping requirements.

### Usage

Table : ARM Cortex R4 Memory Usage

### Non  RTE NvM Blocks

Note : Size of the NVM block if configured in developer

### RTE NvM Blocks

Note : Size of the NVM block if configured in developer

## Compiler Settings

### Preprocessor MACRO

None

### Optimization Settings

None

## Appendix

None

| Sl. No. | Description | Author | Version | Date |

| --- | --- | --- | --- | --- |

| 1 | Initial version | nzt9hv | 1 | 31-May-13 |

| 2 | Corrected the Digital MSB | Nzt9hv | 2 | 02-Aug-13 |

| 3 | Updated for v 2 ES 50A Draft | Nzt9hv | 3 | 08-Aug-13 |

| 4 | Note added to provide buffer output synchronisation | Nzt9hv | 4 | 28-Aug-13 |

| 5 | Added new Memmap statement  for cleared DIGMSB_START_SEC_VAR_CLEARED_8 | Nzt9hv | 5 | 23-Sep-13 |

| 6 | Updated for ES50A prerelease | Selva | 6 | 3-Apr-14 |

| 7 | Updated for ES50A v6 | Selva | 7 | 23-Apr-14 |

| 8 | Updated for FDD rev.008 and updated to latest Integration Manual Template | Rijvi | 8 | 06-Feb-15 |

| Abbreviation | Description |

| --- | --- |

| DFD | Design functional diagram |

| MDD | Module design Document |

| FDD | Functional Design Document |

|  |  |

|  |  |

| Sr. No. | Title | Version |

| --- | --- | --- |

| 1 | ES50A_DigMSBAllegro1331 | 008 |

|  |  |  |

|  |  |  |

|  |  |  |

|  |  |  |

| Module | Required Feature |

| --- | --- |

| SPINxt |  |

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

| DigMSB_Init | None | RTE |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| DigMSB_Per2 | None | RTE(2 ms) |

| DigMSB_Per3 | None | RTE(100 ms) |

| DigMSB_Per1 | Before  Motor <br/>Velocity and before Current Measurement | ISR (50 us) |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| DIGMSB_START_SEC_VAR_CLEARED_16 |  |  |

| DIGMSB_START_SEC_VAR_CLEARED_8 |  |  |

| DIGMSB_START_SEC_VAR_CLEARED_BOOLEAN |  |  |

| DIGMSB_START_SEC_VAR_CLEARED_UNSPECIFIED |  |  |

| DIGMSB_START_SEC_VAR_CLEARED_32 |  |  |

| SA_DIGMSB_CODE |  |  |

| RTE_START_SEC_SA_DIGMSB_APPL_CODE |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| None |  |  |

| Block Name |

| --- |

| None |

| Block Name |

| --- |

| DigMSBEOLData |
