---
title: 'Adc2 MDD'
description: 'Converted design document: Adc2 MDD'
---

> **Source:** `Adc/doc/Adc2_MDD.docx`  
> **Module:** [Adc](../../../../ecuab/adc/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module – ADC2

## High-Level Description

The ADC2 module shall control sampling and conversion of voltages from the hardware layer into digital signals.

## Figures

### Component Diagram

## Variable Data Dictionary

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

### Module Internal Variables

This section identifies the name, range and resolutions for module specific data created by this module.  If there are no range restrictions on the variable, the term “FULL” is placed into the table for legal range.

#### User defined typedef definition/declaration

This section documents any user types uniquely used for the module.

## Constant Data Dictionary

### Calibration Constants

This section lists the calibrations used by the module.  For details on calibration constants, refer to the Data Dictionary for the application.

### Program(fixed) Constants

#### Embedded Constants

All embedded constants whose values are provided in Eng units will be evaluated to the equivalent counts by using the FPM_InitFixedPoint_m() macro within the #define statement.

##### Local

##### Global

This section lists the global constants used by the module.  For details on global constants, refer to the Data Dictionary for the application.

#### Module specific Lookup Tables Constants

## Functions/Macros used by the Sub-Modules

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules are identified below,

None

### Data Hiding Functions

None

### Global Functions/Macros Defined by this Module

#### ADC2 Init

This function is used to initialize each of the ADC2 Groups (Event, Group1, and Group2).

##### Initialize Module Internal Variables

None

##### Register Configuration

##### Start Initial Conversions

#### Start Group Conversion

This function starts a software triggered conversion of all channels of the requested Adc channel group.

##### Start Conversions

#### Enable Group Notification

This inline function reads and returns the individual channel conversion result.

##### Enable Notification Conditions

### Local Functions/Macros Used by this MDD only

#### Read Channel Conversions

This inline function reads and returns the individual channel conversion result.

##### Read Group

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

None

### Initialization Functions

None

### Periodic Functions

None

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

None

### Transition Functions

None

## Execution Requirements

### Execution Sequence of the Module

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Limitations With Design

INLINE functions defined in “GlobalMacro.h” are not unit tested

Buffer pointer initialization could hang if adc conversion did not complete.  Consider adding a timeout and possible setting of NTC 0x33 bit 1.

## Revision Control Log

| Module Inputs | Module Outputs |

| --- | --- |

| None |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| See Adc_MDD.doc for Adc subsystem types |  |  |  |  |

| Constant Name |

| --- |

| None |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_GROUPEV_CNT_U8 | 1 | Counts | 0 |

| D_GROUP1_CNT_U8 | 1 | Counts | 1 |

| D_GROUP2_CNT_U8 | 1 | Counts | 2 |

| D_NTCPARMBIT1_CNT_U8 | 1 | Counts | 2 |

| D_ADC2EVTBUFSZ_CNT_U08 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G1BUFSZ_CNT_U08 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G2BUFSZ_CNT_U08 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2EVSRC_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G1SRC_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G2SRC_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2NUMEVTCH_CNT_U08 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2EVTCH_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2NUMG1CH_CNT_U08 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G1CH_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2NUMG2CH_CNT_U08 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G2CH_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2RSLTBASEADR_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2EVINTENA_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2EVSAMPDISEN_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2EVFIFORESETCR_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2EVDMACR_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G1INTENA_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G1SAMPDISEN_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G1FIFORESETCR_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G1DMACR_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G2INTENA_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G2SAMPDISEN_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G2FIFORESETCR_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2G2DMACR_CNT_U32 | 1 | Counts | Generated in Adc2_Cfg.h |

| D_HWTRGADC2GEVT_CNT_LGC | 1 | Counts | Generated in Adc2_Cfg.h |

| D_HWTRGADC2G1_CNT_LGC | 1 | Counts | Generated in Adc2_Cfg.h |

| D_HWTRGADC2G2_CNT_LGC | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ADC2USEDMA_CNT_LGC | 1 | Counts | Generated in Adc2_Cfg.h |

| D_ISRGROUP_CNT_U8 | 1 | Counts | Generated in Adc2_Cfg.h |

| Constant Name |

| --- |

| None |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| T_Adc2GroupConfigData_Cnt_Str[3] | Adc_GroupConfigDataType | {<br/>		D_ADC2NUMEVTCH_CNT_U08,<br/>		D_ADC2EVTCH_CNT_U32,<br/>		&(((uint32*)D_ADC2RSLTBASEADR_CNT_U32)[0]),<br/>	},<br/>	{<br/>		D_ADC2NUMG1CH_CNT_U08,<br/>		D_ADC2G1CH_CNT_U32,<br/>		&(((uint32*)D_ADC2RSLTBASEADR_CNT_U32)[D_ADC2EVTBUFSZ_CNT_U08]),<br/>	},<br/>	{<br/>		D_ADC2NUMG2CH_CNT_U08,<br/>		D_ADC2G2CH_CNT_U32,<br/>		&(((uint32*)D_ADC2RSLTBASEADR_CNT_U32)[D_ADC2EVTBUFSZ_CNT_U08 + D_ADC2G1BUFSZ_CNT_U08]),<br/>	} | CONST_32 |

| Function Name | Adc2_init1 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | ConfigPtr | Adc_ConfigType* | N/A | N/A |  |

| Return Value | N/A |  |  |  |  |

| Function Name | Adc2_StartGroupConversion | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | group | uint8 | 0 | 2 |  |

| Return Value | N/A |  |  |  |  |

| Function Name | Adc2_EnableGroupNotification | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | group | uint8 | 0 | 15 |  |

| Return Value | N/A |  |  |  |  |

| Function Name | Adc2_ReadConversion | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | ConvId | uint16 | 0 | 15 |  |

| Return Value | conversion result | uint16 | 0 | 4095 | 0 |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| Adc2_Init | Once (at initialization) | STARTUP |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| N/A |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| Adc2_Init | ADC2_START_SEC_CODE |

| Adc2_StartGroupConversion | ADC2_START_SEC_CODE |

| Adc2_EnableGroupNotification | ADC2_START_SEC_CODE |

| Adc2_ReadConversion | inline |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1.0 | Initial version based on FDD 33C rev 006 | 05Nov12 | LN |

| 2.0 | Design updates to meet FDD and simplify configuration | 24APR13 | Selva |

| 3.0 | Fixed typo in flowchart | 22MAY13 | LWW |

| 4.0 | Updated for use with DMA. Moved init function scheduling requirements to integration manual. Added design limitation note about buffer pointer initialization. | 10APR14 | KMC |

|  |  |  |  |
