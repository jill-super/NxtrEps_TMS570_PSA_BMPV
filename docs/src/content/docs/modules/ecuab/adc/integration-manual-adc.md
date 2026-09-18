---
title: 'Integration Manual ADC'
description: 'Converted design document: Integration Manual ADC'
---

> **Source:** `Adc/doc/Integration_Manual_ADC.docx`  
> **Module:** [Adc](../../../../ecuab/adc/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual –<Name of component>

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

3	Integration	6

3.1	Required Global Data Inputs	6

3.2	Required Global Data Outputs	6

3.3	Specific Include Path present	6

4	Runnable Scheduling	7

5	Memory Mapping	8

5.1	Mapping	8

5.2	Usage	8

5.3	Non  RTE NvM Blocks	8

5.4	RTE NvM Blocks	8

6	Compiler Settings	8

6.1	Preprocessor MACRO	8

6.2	Optimization Settings	8

7	Revision Control Log	9

## Dependencies

### SWCs

Note : Referencing the external components should be avoided in most cases. Only in unavoidable circumstance external components should be refered. Developer should track the references.

### Global Functions(Non RTE) to be provided to Integration Project

- Adc_Init()   NOTE this is a macro mapped to Adc_Init_FixedCfg for Autosar interface compatibility.  The Adc_Init macro takes a parameter which is not used by the function.

- FUNC(void, ADC_CODE) Adc_StartGroupConversion(Adc_GroupType Group)

- FUNC(Std_ReturnType, ADC_CODE) Adc_ReadGroup(Adc_GroupType Group, Adc_ValueGroupRefType DataBufferPtr)

- FUNC(Adc_StatusType, ADC_CODE) Adc_GetGroupStatus(Adc_GroupType Group)

- inline uint16 Adc2_ReadConversion(uint16 ConvId)  NOTE this function directly accesses Adc RAM and should not be used when using DMA to transfer Adc data

- void Adc2_Init1(void)

- void Adc2_StartGroupConversion(uint8 group)

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

Adc_Cfg.h and Adc2_Cfg.h.   Configuration file templates are in the Tools folder.

NOTE:

For Projects using 33E, make sure “D_ADC1CURRENTMODE_ULS_LGC”  is defined in Adc_Cfg.h file.

For Projects using 33C, make sure “D_ADC1CURRENTMODE_ULS_LGC”  is  NOT defined in Adc_Cfg.h file.

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

*NOTE: See template Adc_Cfg.h and Adc2_Cfg.h files in Tools folder for settings to maintain pre-DMA (FDD33C rev008 and FDD33E rev002) behavior.

**NOTE: Additional manual configuration constants are needed, and are included in the template config header files, but are not listed here.  To be added in CR 11738 complete design review of this component.

## Integration

### Required Global Data Inputs

None

### Required Global Data Outputs

### Specific Include Path present

Yes

## Runnable Scheduling

This section specifies the required runnable scheduling.

*NOTE: Depending on configuration, some of the other listed init functions may not be present.  Other application-specific scheduling requirements may exist.

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

| IoHwAbsUsr | Parts of the Adc FDDs (33C or 33E) are intended to be implemented at the integration level and are typically included in IoHwAbsUsr.  Note that this includes implementation of NTC 0x32 and/or NTC 0x33 as needed for the specific application.  <br/>NOTE that as of FDD33C rev 008 and FDD33E rev 002, DMA-related updates are not included in the FDDs. The looping on group busy and associated timeouts and NTC setting should not be implemented when using with DMA; alternate means of getting the data when ready and associated fault setting are outlined in the DMA FDD ES-52. |

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| <Configurator  Changes for parameters> |  |  |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| <Configurator  Changes for  Interrupts> |  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| D_ADC1GEVTSRC_CNT_U32* | Initialization value for adcREG1->G0SRC | Adc_Cfg.h |

| D_ADC1GEVTDMACR_CNT_U32* | Initialization value for adcREG1->G0DMACR | Adc_Cfg.h |

| D_ADC1G1SRC_CNT_U32* | Initialization value for adcREG1->G1SRC | Adc_Cfg.h |

| D_ADC1G1DMACR_CNT_U32* | Initialization value for adcREG1->G1DMACR | Adc_Cfg.h |

| D_ADC1G2SRC_CNT_U32* | Initialization value for adcREG1->G2SRC | Adc_Cfg.h |

| D_ADC1G2DMACR_CNT_U32* | Initialization value for adcREG1->G2DMACR | Adc_Cfg.h |

| D_ADC1USEDMA_CNT_LGC* | STD_ON if using DMA to transfer ADC1 data; otherwise STD_OFF | Adc_Cfg.h |

| D_HWTRGADC1GEVT_CNT_LGC* | STD_ON to reconfigure ADC1 event group for hardware trigger after initial reads; otherwise STD_OFF | Adc_Cfg.h |

| D_HWTRGADC1G1_CNT_LGC* | STD_ON to reconfigure ADC1 group 1 for hardware trigger after initial reads; otherwise STD_OFF | Adc_Cfg.h |

| D_HWTRGADC1G2_CNT_LGC* | STD_ON to reconfigure ADC1 group 2 for hardware trigger after initial reads; otherwise STD_OFF | Adc_Cfg.h |

| D_ADC2EVINTENA_CNT_U32* | Initialization value for adcREG2-><br/>GxINTENA[D_GROUPEV_CNT_U8] | Adc2_Cfg.h |

| D_ADC2EVSAMPDISEN_CNT_U32* | Initialization value for adcREG2-><br/>G0SAMPDISEN | Adc2_Cfg.h |

| D_ADC2EVFIFORESETCR_CNT_U32* | Initialization value for adcREG2-><br/>GxFIFORESETCR[D_GROUPEV_CNT_U8] | Adc2_Cfg.h |

| D_ADC2EVDMACR_CNT_U32* | Initialization value for adcREG2-><br/>G0DMACR | Adc2_Cfg.h |

| D_ADC2G1INTENA_CNT_U32* | Initialization value for adcREG2-><br/>GxINTENA[D_GROUP1_CNT_U8] | Adc2_Cfg.h |

| D_ADC2G1SAMPDISEN_CNT_U32* | Initialization value for adcREG2-><br/>G0SAMPDISEN | Adc2_Cfg.h |

| D_ADC2G1FIFORESETCR_CNT_U32* | Initialization value for adcREG2-><br/>GxFIFORESETCR[D_GROUP1_CNT_U8] | Adc2_Cfg.h |

| D_ADC2G1DMACR_CNT_U32* | Initialization value for adcREG2-><br/>G0DMACR | Adc2_Cfg.h |

| D_ADC2G2INTENA_CNT_U32* | Initialization value for adcREG2-><br/>GxINTENA[D_GROUP2_CNT_U8] | Adc2_Cfg.h |

| D_ADC2G2SAMPDISEN_CNT_U32* | Initialization value for adcREG2-><br/>G0SAMPDISEN | Adc2_Cfg.h |

| D_ADC2G2FIFORESETCR_CNT_U32* | Initialization value for adcREG2-><br/>GxFIFORESETCR[D_GROUP2_CNT_U8] | Adc2_Cfg.h |

| D_ADC2G2DMACR_CNT_U32* | Initialization value for adcREG2-><br/>G0DMACR | Adc2_Cfg.h |

| D_HWTRGADC2GEVT_CNT_LGC* | STD_ON to reconfigure ADC2 event group for hardware trigger after initial reads; otherwise STD_OFF | Adc2_Cfg.h |

| D_HWTRGADC2G1_CNT_LGC* | STD_ON to reconfigure ADC2 group 1 for hardware trigger after initial reads; otherwise STD_OFF | Adc2_Cfg.h |

| D_HWTRGADC2G2_CNT_LGC* | STD_ON to reconfigure ADC2 group 2 for hardware trigger after initial reads; otherwise STD_OFF | Adc2_Cfg.h |

| D_ADC2USEDMA_CNT_LGC* | STD_ON if using DMA to transfer ADC2 data; otherwise STD_OFF | Adc2_Cfg.h |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| Adc_Init() | Before  Adc2_Init1 <br/>Before IoHwAb_Init<br/>After SystemTime_Init<br/>After Dma_Init | ECU Startup |

| Adc2_Init1() | Before PWMCdd_Init <br/>Before enabling Motor Control ISR <br/>After SystemTime_Init<br/>After Dma_Init | ECU Startup |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| Adc_StartGroupConversion | As determined by application needs and configuration |  |

| Adc2_StartGroupConversion | As determined by application needs and configuration |  |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| ADC2_START_SEC_CODE |  |  |

| ADC2_START_SEC_CONST_32 |  |  |

| ADC_START_SEC_CONST_32 |  |  |

| ADC_START_SEC_CODE |  |  |

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

| 1 | Initial version | 09-Apr-13 | Selva |

| 2 | Updated to latest integration manual template.  Updated per changes made for use with DMA.  Added init function scheduling requirements that had previously been listed in the MDDs. | 11-Apr-14 | KMC |

|  |  |  |  |
