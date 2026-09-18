---
title: 'Nhet 1 MDD'
description: 'Converted design document: Nhet 1 MDD'
---

> **Source:** `ePWM/doc/Nhet_1_MDD.docx`  
> **Module:** [ePWM](../../../../cdd/epwm/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module – NHET

## High-Level Description

This module implements NHET .

## Figures

None

## Variable Data Dictionary

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

### Module Internal Variables

This section identifies the name, range and resolutions for module specific data created by this module.  If there are no range restrictions on the variable, the term “FULL” is placed into the table for legal range.

#### User defined typedef definition/declaration

This section documents any user types uniquely used for the module.

(Refer the included ref for more details of register)

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

HET Macros

HTU MACROS

Memcpy

### Data Hiding Functions

None

### Global Functions/Macros Defined by this Module

#### Global Functions #1 (For detailed info regarding values assigned to registers refer Reference Pdf attached below)

##### Description

### NHET:

### Local Functions/Macros Used by this MDD only

#### Local Functions #1

##### Description

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init:

##### Design Rationale

##### Module Outputs

None

##### Module Internal

None

##### Initialize NHET Direction Register

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

### Execution Rates for sub-modules called by the Subroutine

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

## Reference

Register Reference

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| HET_INIT1_PST | HET_INIT1_PST |  |

| HET_INIT0_PST | HET_INIT0_PST |  |

| Nhet_HtuDataTrq_Cnt_G_str | Nhet_HtuDataTrq_Cnt_G_str |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| Nhet_HtuDataTrq_Cnt_G_str | N/A | N/A | N/A | NHET_START_SEC_VAR_CLEARED_UNSPECIFIED |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| HtuDataTrq_Str | HtuDataTrq1_Cnt_u32 [8] | Uint32 | 0 | FULL |

|  | HtuDataTrq2_Cnt_u32 [8] | Uint32 | 0 | FULL |

| Constant Name |

| --- |

| k_SENTSyncDelay_Cnt_u32 |

| k_SENTSyncTrgMin_Cnt_u32 |

| k_SPI50UOff_Cnt_u16 |

| k_SPI1mOff_Cnt_u16 |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- |

| D_INSTTODATARATIO_CNT_U16 | 1 | Counts | 4 |

| D_DATAFLDOFFSET_CNT_U16 | 1 | Counts | 8 |

| D_BASEADDNHETRAM_CNT_U32 | 1 | Counts | 0xFF460000UL |

| D_WCAPHTUADDR1_CNT_U32 | 1 | Counts | D_BASEADDNHETRAM_CNT_U32 + (16U*pHET_T1MSGCNTST_0) + 8UL |

| D_WCAPHTUADDR2_CNT_U32 | 1 | Counts | D_BASEADDNHETRAM_CNT_U32 + (16U*pHET_T2MSGCNTST_0) + 8UL |

| D_CELEMENT_CNT_U16 | 1 | Counts | 8 |

| D_CBUFLEN_CNT_U16 | 1 | Counts | 8 |

| D_CONFIGHETREGDMA_CNT_U32 | 1 | Counts | Configurable. 0UL if no DMA needs to be enabled  and 1UL if using DMA |

| D_CFRAME_CNT_U16 | 1 | Counts | (D_CBUFLEN_CNT_U16/D_CELEMENT_CNT_U16) |

| Constant Name |

| --- |

| None |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | NHET_Init1 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | None |  |  |  |  |

| Function Name | HTU_Init | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | None |  |  |  |  |

| Data | Value |

| --- | --- |

| None |  |

| Global Function Name | Calling Frequency | Function in which the function is called |

| --- | --- | --- |

| NHET_Init1 | On Event | ECU start up |

|  |  |  |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| NHET_Init1 | #define NHET_START_SEC_CODE |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1.0 | Initial Version ( FDD 34B) |  | Selva |

| 2.0 | Updated to FDD 34B v003 | 19-Jun-13 | OT/SELVA |

| 3.0 | Removed  “NHETPINDIS” in Nhet1 | 01-Aug-13 | Selva |

| 4.0 | Updated to FDD34B v004 | 4-Apr-14 | Selva |

| 5.0 | Anomaly fix 6589 - Correct the value for the HTU MP0E register CR 11799 | 23-Apr-14 | SB |

| 6.0 | Anomaly fix 6844 - ePWM/ES34B: HTU is enabled before HTU MPU config is set up | 26-Nov-14 | VT |

|  |  |  |  |
