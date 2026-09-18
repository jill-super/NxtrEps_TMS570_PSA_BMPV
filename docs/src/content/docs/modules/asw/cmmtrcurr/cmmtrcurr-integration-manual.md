---
title: 'CmMtrCurr Integration Manual'
description: 'Converted design document: CmMtrCurr Integration Manual'
---

> **Source:** `CmMtrCurr/doc/CmMtrCurr_Integration_Manual.docx`  
> **Module:** [CmMtrCurr](../../../../asw/cmmtrcurr/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual –CmMtrCurr

Table of Contents

## Dependencies

### SWCs

Note : Referencing the external components should be avoided in most cases. Only in unavoidable circumstance external components should be refered. Developer should track the references.

### Functions to be provided to Integration Project

CurrDQPer1

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

CmMtrCurr_Cfg.h ( Refer CmMtrCurr_Cfg_Template.h in tools folder)

(Data synchronization must be provided at the integration level between 2 ms periodic and Motor Control ISR Periodic’s)

Outputs from the CmMtrCurr (Motor Control ISR) periodic must be synchronized with  from

#### Da Vinci Config Configuration Changes

Note: Only one of the configuration can be selected based on the requirements. Make sure order matches oreder in ADC  data read  ie MTRCURRPHASEBC -   “BC” represents current_1 is phase B and current_2 is phase C  .

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

For other inputs  Refer the template in tools folder of this component

### Required Global Output Inputs

For other inputs  Refer the template in tools folder of this component

### Specific Include Path present

Yes

## Runnable Scheduling

This section specifies the required runnable scheduling.

### .

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

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| MTRCURRPHASEBC | PhaseB and Phase C used in Curr Measurement |  |

| MTRCURRPHASECB | PhaseC and Phase B used in Curr Measurement |  |

| MTRCURRPHASEAC | PhaseA and Phase C used in Curr Measurement |  |

| MTRCURRPHASECA | PhaseC and Phase A used in Curr Measurement |  |

| MTRCURRPHASEAB | PhaseA and Phase B used in Curr Measurement |  |

| MTRCURRPHASEBA | PhaseB and Phase A used in Curr Measurement |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| none |  |  |

|  |  |  |

|  |  |  |

|  |  |  |

|  |  |  |

|  |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| CmMtrCurr_Init | None | RTE |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| CmMtrCurr_Per2 | None | RTE(2MilliS) |

|  |  |  |

| CmMtrCurr_Per1 | None | RTE(100 MilliS) |

| CurrDQPer1 | After  processing | ISR MicroS) |

|  |  |  |

|  |  |  |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| CMMTRCURR_START_SEC_VAR_CLEARED_16 |  |  |

| CMMTRCURR_START_SEC_VAR_CLEARED_8 |  |  |

| CMMTRCURR_START_SEC_VAR_CLEARED_BOOLEAN |  |  |

| CMMTRCURR_START_SEC_VAR_CLEARED_32 |  |  |

| SA_CMMTRCURR_CODE |  |  |

| RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |  |  |

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

| 1 | Initial version | 7-Sep- 13 | nzt9hv |

| 2 |  |  |  |

|  |  |  |  |

|  |  |  |  |
