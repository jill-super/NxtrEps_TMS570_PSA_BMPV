---
title: 'Shutdown Mechanisms MDD'
description: 'Converted design document: Shutdown Mechanisms MDD'
---

> **Source:** `ShtdnMech/doc/Shutdown_Mechanisms_MDD.docx`  
> **Module:** [ShtdnMech](../../../../asw/shtdnmech/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module –

## High-Level Description

This module handles.

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

None

### Local Functions/Macros Used by this MDD only

None

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

### Periodic Functions

#### Per: _Per1

##### Design Rationale

None

##### Program Flow Start

Rte_Call_ShtdnMech_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

Rte_Call_FetDrvReset_OP_GET(&FetDrvReset_Cnt_T_lgc)

Rte_Call_SysFault2_OP_GET(&SysFault2_Cnt_T_lgc)

Rte_Call_SysFault3_OP_GET(&SysFault3_Cnt_T_lgc)

##### Status Signals for Testing

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

Rte_Call_ShtdnMech_Per1_CP1_CheckpointReached()

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

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| None | None | None |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| ESMErrOutStat_Cnt_D_u08 | 1 | 0 | 1 | SHTDNMECH_START_SEC_VAR_CLEARED_8 |

| SysFault2Stat_Cnt_D_u08 | 8 | 0 | 8 | SHTDNMECH_START_SEC_VAR_CLEARED_8 |

| GateDrvResetStat_Cnt_D_u32 | 524288 | 0 | 524288 | SHTDNMECH_START_SEC_VAR_CLEARED_32 |

| NHETPwmStat_Cnt_D_u32 | 22282308 | 0 | 22282308 | SHTDNMECH_START_SEC_VAR_CLEARED_32 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Constant Name |

| --- |

| None |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_ESMERROUTSTAT_CNT_U08 | 1 | Counts | 0x01 |

| D_SYSFAULT2STAT_CNT_U08 | 1 | Counts | 0x08 |

| D_GATEDRVRESETSTAT_CNT_U32 | 1 | Counts | 0x00080000 |

| D_NHETPWMSTAT_CNT_U32 | 1 | Counts | 0x01540044 |

|  |  |  |  |

| Constant Name |

| --- |

| D_ZERO_CNT_U8 |

| D_ZERO_CNT_U32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Data | Value |

| --- | --- |

| None |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| ShtdnMech_Per1 | ms | ALL |

|  |  |  |

|  |  |  |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| ShtdnMech_Per1 | RTE_START_SEC_SA_SHTDNMECH_APPL_CODE |

|  |  |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial Version | 25-Jul-12 | OT |

| 2 | 2.0 | Updates to remove NHETPINDIS, removed control of SysFault3 pin (this is handled in hardware). Only control NHET Direction on entering operate state (instead of exiting disable state) as other pins are controlled by other modules and NHET pins should remain inputs in warm init. | 03-Aug-12 | LWW |

| 3 | 3.0 | Update for anomaly 3640 correction | 22-Aug-12 | LWW |

| 4 | 4.0 | Added checkpoints and memmap software segment is updated for static variables | 27-Sep-12 | Selva |

|  |  |  |  |  |
