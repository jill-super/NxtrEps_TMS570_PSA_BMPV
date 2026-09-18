---
title: 'Dma MDD'
description: 'Converted design document: Dma MDD'
---

> **Source:** `Dma/doc/Dma_MDD.docx`  
> **Module:** [Dma](../../../../mcal/dma/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

### Module Design Document

### For

### DMA

### Document Identifier: <Project_id>_<Config Id>

### VERSION:

### DATE:

Location: The official version of this document is stored in the Nexteer Configuration Management System and is uniquely identified by: <Project_ID>_<Config Id>

### Revision History

### Table of Contents

1	Abbrevations And Acronyms	5

2	References	6

3	DMA & High-Level Description	7

4	Design details of software module	8

4.1	Graphical representation of DMA	8

5	Variable Data Dictionary	9

5.1	User defined typedef definition/declaration	9

5.2	Variable definition for enumerated types	9

6	Constant Data Dictionary	10

6.1	Program(fixed) Constants	10

6.1.1	Embedded Constants	10

6.1.1.1	Local	10

6.1.1.2	Global	10

6.1.2	Module specific Lookup Tables Constants	10

6.1.3	Library Functions / Macros	10

6.1.4	Data Hiding Functions	11

7	Software Module Implementation	12

7.1	Initialization Functions	12

7.1.1	Init: Dma _Init	12

7.1.1.1	Design Rationale	12

7.1.1.1.1	MPU Settings	12

7.1.1.1.2	Priority Assignments	12

7.1.1.1.3	FlsTst Group (Channels 0 and 1)	12

7.1.1.2	Initialize DMA Registers	12

7.1.1.3	Module Outputs	12

7.1.1.4	Module Internal	13

7.2	PERIODIC FUNCTIONS	13

7.2.1	Per: Dma _Per1	13

7.2.1.1	Design Rationale	13

7.2.1.2	Store Module Inputs to Local copies	13

7.2.1.3	Clear DMA RAM Buffers	13

7.2.1.4	Store Local copy of outputs into Module Outputs	13

7.3	Interrupt Functions	13

7.4	TRANSIENT FUNCTIONS	13

7.5	Serial Communication Functions	13

7.6	Local Function/Macro Definitions	13

7.7	GLObAL Function/Macro Definitions	13

7.7.1	Setup MtrCtrl Groups	13

7.7.1.1	Description	13

7.7.2	Setup FlsTst Blocks	14

7.7.2.1	Description	14

7.7.3	Enable FlsTst Block	14

7.7.3.1	Description	14

7.7.4	Disable FlsTst Block	14

7.7.4.1	Description	14

7.7.5	Report DMA MPU Error	14

7.7.5.1	Description	14

8	Known Limitations With Design	15

9	UNIT TEST CONSIDERATION	16

10	Appendix A – Configuration Schemes	17

## Abbrevations And Acronyms

## References

This section Lists the title & version of all the documents that are referred for development of this document

## DMA & High-Level Description

DMA is a driver level module that performs flash, RAM, and peripheral reads and writes in the background, freeing up the CPU to do other work in parallel.  It is equipped with parity checking and an MPU, but timing and data consistency must be considered with respect to CPU execution.

## Design details of software module

### Graphical representation of DMA

## Variable Data Dictionary

### User defined typedef definition/declaration

* Note that the elements of this structure are dependent on whether the respective peripherals are configured to use DMA.  In the case that none of the ADC, SPI, or PWM groups are enabled in DMA, the type will not be defined.

### Variable definition for enumerated types

## Constant Data Dictionary

### Program(fixed) Constants

### Embedded Constants

### Local

### Global

### Module specific Lookup Tables Constants

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules shall be identified in this section

None

### Data Hiding Functions

The Data hiding functions that’s uses RTE interface or other macro interfaces shall be listed in this section.

DMA_REPORTERRORSTATUS(event, param, status)

## Software Module Implementation

### Initialization Functions

### Init: Dma_Init

### Design Rationale

The DMA module must encapsulate many possible configurations.  These configurations can be enabled or disabled per the configuration header file

enabled at the end of the function.  Once this is done, DMA will remain active for the remainder of the ignition cycle.  Individual channels can be enabled or disabled as needed, however.

### MPU Settings

The nature of the DMA MPU is different from that of the CPU.  The DMA has four configurable memory regions; anything outside of the declared regions is considered full access.  The regions may overlap, however, and are treated by “priority” – that is,  In light of this, the final memory region is used to cover the majority of the memory map.  The other three regions are configured to allow access to specific regions.  The following table shows the memory region allocations:

This configuration is based on safety analysis (included in FDD 52) and the DMA MPU limitations.

### Priority Assignments

Channels 0 and 1 are assigned low priority, while the other channels are assigned as high priority.  As channels 0 and 1 are used for FlsTst functionality, they are designed to be run “in the background”, while the other channels need high priority to ensure the MtrCtrl ISR is run on schedule.  Any unused channel is left at a default of low priority.

### Initialize DMA Registers

<flow chart>

### Module Outputs

None

### Module Internal

None

### PERIODIC FUNCTIONS

None

### Interrupt Functions

None

### TRANSIENT FUNCTIONS

None

### Serial Communication Functions

None

### Local Function/Macro Definitions

None

### GLObAL Function/Macro Definitions

### Check Validity of Slow ADC Group

### Design Rationale

This function is provided as one part of the data integrity scheme.  The FDD requires that the DMA buffer be checked before the data is read, and cleared after the data is read.  This function is designed to be called before the ADC data is read, and returns FALSE if the data is invalid.  The FDD specifies that the data be copied if it is valid; for throughput and memory reasons, this is left as the responsibility of the caller.

### Description

<flow chart>

### Invalidate Slow ADC Group Buffers

### Design Rationale

To ensure that the DMA is running, this function is provided to be run after the DMA data is collected by the 2ms IoHwAbstraction component.  The buffers are cleared to 0xFFFF with the expectation that the DMA will fill them with proper data before the data is collected again.  If the DMA fails to do so, the cleared buffers will trigger the internal DMA diagnostic (implemented in Dma_SlowADCGroupValidity).

This is intended to be used as part of a larger data consistency scheme.  See Appendix A for more information on how this is designed to be used.

### Description

<flow chart>

### Setup MtrCtrl Groups

### Description

<flow chart>

### Setup FlsTst Blocks

### Description

<flow chart>

### Enable FlsTst Block

### Description

<flow chart>

### Disable FlsTst Block

### Description

<flow chart>

## Known Limitations With Design

This design only considers DMA transfers for a specific sensor configuration.  Older or newer programs may have other DMA needs that are not considered, and the design will need to be updated to accommodate those sensor configurations in time.

This design has only been verified on Champion hardware.  It would need to be validated on Gladiator hardware before use.

## UNIT TEST CONSIDERATION

None

## Appendix A – Configuration Schemes

The DMA module is intended to be configurable for any number of use cases.  While each channel is specifically assigned, each channel can be enabled or disabled per program.

The following diagram shows the MtrCtrl ISR groups and where they are designed to run.  The trigger points for each group, as well as non-configurable data formats and lengths, are based on this data and the corresponding peripherals.

| Sl. No. | Description | Author | Version | Date |

| --- | --- | --- | --- | --- |

| 1 | Initial version | Owen Tosh | 1 | 04-Apr-2014 |

| 2 | Updated to FDD52 v001 | Owen Tosh | 2 | 29-Apr-2014 |

| 3 | Updated to FDD52 v002 | Owen Tosh | 3 | 02-May-2014 |

|  |  |  |  |  |

| Abbreviation | Description |

| --- | --- |

| MDD | Module design Document |

| MtrCtrl ISR | Motor Control Interrupt Service Routine.  This is the “fast” code loop that controls the main PWM signals. |

| Sr. No. | Title | Version |

| --- | --- | --- |

| 1 | MDD Guidelines | 1 |

| 2 | Software Naming Conventions | 1 |

| 3 | Coding Standands | 1 |

| 4 | ES 52 – DMA | 00 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| DMADataType_Str * |  |  |  |  |

| DMADataType_Str * | FastSPI_Cnt_u16[D_NUMFASTSPIWORDS_CNT_U16] | uint16 | 0 | 216 - 1 |

| DMADataType_Str * | SlowSPI_Cnt_u16[D_NUMSLOWSPIWORDS_CNT_U16] | uint16 | 0 | 216 - 1 |

| DMADataType_Str * | SlowADC_Cnt_u16[D_NUMFASTADCCHANNELS_CNT_U16] | uint16 | 0 | 216 - 1 |

| DMADataType_Str * | FastADC_Cnt_u16[D_NUMSLOWADCCHANNELS_CNT_U16] | uint16 | 0 | 216 - 1 |

| DMADataType_Str * | PWMCmp_Cnt_u16[4][2] | uint16 | 0 | 216 - 1 |

| DMADataType_Str * | PWMPeriod_Cnt_u32 | uint32 | 0 | 232 - 1 |

| Enum  Name | Element Name | Value |

| --- | --- | --- |

| None |  |  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_DMAFLSTSTENABLED_CNT_ENUM | enum | Count | configurable |

| D_FASTSPIGROUPENABLED_CNT_ENUM | enum | Count | configurable |

| D_FASTADCGROUPENABLED_CNT_ENUM | enum | Count | configurable |

| D_FASTPWMGROUPENABLED_CNT_ENUM | enum | Count | configurable |

| D_SLOWADCGROUPENABLED_CNT_ENUM | enum | Count | configurable |

| D_CRCCTRLREGSTART_CNT_U32 | 1 | Count | &(CRCCTRLREG->CRC_REGL1) |

| D_CRCPSASIGREGSTART_CNT_U32 | 1 | Count | &(CRCCTRLREG->PSA_SIGREGL1) |

| D_NUMFASTSPIWORDS_CNT_U16 | 1 | Count | D_TGSIZE_CNT_U16 |

| D_FASTSPISTARTADDR_CNT_U32 | 1 | Count | &(mibspiRAM3->rx[0].data) |

| D_NUMFASTADCCHANNELS_CNT_U16 | 1 | Count | D_ADC2G1BUFSZ_CNT_U08 |

| D_FASTADCSTARTADDR_CNT_U32 | 1 | Count | (D_ADC2RSLTBASEADR_CNT_U32 + (4u * D_ADC2EVTBUFSZ_CNT_U08) + 2u) |

| D_DMANHETPERIODADDR_CNT_U32 | 1 | Count | &(HET_PRD_BUF1_0.memory.data_word) |

| D_EPWMSTARTADDR_CNT_U32 | 1 | Count | &(ePWM1->CMPA) |

| D_NUMSLOWADCCHANNELS_CNT_U16 | 1 | Count | D_ADC1G2BUFSZ_CNT_U08 |

| D_SLOWADCSTARTADDR_CNT_U32 | 1 | Count | (0xFF3E0000ul + (4u * (D_ADC1EVTBUFSZ_CNT_U08 + D_ADC1G1BUFSZ_CNT_U08)) + 2u) |

| D_NUMSLOWSPIWORDS_CNT_U16 | 1 | Count | D_TGSIZE_CNT_U16 |

| D_SLOWSPISTARTADDR_CNT_U32 | 1 | Count | &(mibspiRAM5->rx[0].data) |

| Constant Name |

| --- |

| STD_OFF |

| STD_ON |

| CRCCTRLREG |

| D_TGSIZE_CNT_U16 |

| mibspiRAM3 |

| D_ADC2G1BUFSZ_CNT_U08 |

| D_ADC2RSLTBASEADR_CNT_U32 |

| D_ADC2EVTBUFSZ_CNT_U08 |

| HET_PRD_BUF1_0 |

| ePWM1 |

| D_ADC1G2BUFSZ_CNT_U08 |

| D_ADC1EVTBUFSZ_CNT_U08 |

| D_ADC1G1BUFSZ_CNT_U08 |

| mibspiRAM5 |

| DMA_PARITY_ENABLE |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Region | Access | Purpose | Start Address | End Address |

| --- | --- | --- | --- | --- |

| 0 | Read/Write | SPI, ADC, NHET | 0xFF0A0000 | 0xFF473FFF |

| 1 | Read/Write | ePWM, CRC | 0xFCF78C00 | 0xFE0001FF |

| 2 | Read/Write | RAM | &DMAData_G_str | &DMAData_G_str + sizeof(DMAData_G_str) - 1 |

| 3 | No Access | Everything but Flash | 0x00200000 | 0xFFFFFFFF |

| Function Name | Dma_SlowADCGroupValidity | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Return Value | RetValue_Cnt_T_lgc | boolean | FALSE | TRUE |

| Function Name | Dma_InvalidateSlowADCGroup | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Return Value | N/A |  |  |  |

| Function Name | Dma_SetupMtrCtrlGroups | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Return Value | N/A |  |  |  |

| Function Name | Dma_SetupFlsTstBlock | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | CRCAddr_Cnt_T_u32 | uint32 | 0 | 232 - 1 |

|  | FlsAddr_Cnt_T_u32 | uint32 | 0 | 232 - 1 |

|  | DmaFrameCount_Cnt_T_u16 | uint16 | 0 | 216 - 1 |

|  | DmaElementCount_Cnt_T_u16 | uint16 | 0 | 216 - 1 |

| Return Value | N/A |  |  |  |

| Function Name | Dma_EnableFlsTstBlock | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Return Value | N/A |  |  |  |

| Function Name | Dma_DisableFlsTstBlock | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Return Value | N/A |  |  |  |
