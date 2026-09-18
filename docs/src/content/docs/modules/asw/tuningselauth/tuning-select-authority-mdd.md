---
title: 'Tuning Select Authority MDD'
description: 'Converted design document: Tuning Select Authority MDD'
---

> **Source:** `TuningSelAuth/doc/Tuning_Select_Authority_MDD.docx`  
> **Module:** [TuningSelAuth](../../../../asw/tuningselauth/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module – Tuning Select Authority

## High-Level Description

This function broadcasts an authority to allow switching between calibration subsets while driving.  It compares handwheel torque and vehicle speed to calibratable thresholds and outputs either a zero or a one.

## Figures

### Component Diagram

## Variable Data Dictionary

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

* Note: For unit testing purposes these inputs are defined  as pointers to uint16 (as opposed to pointers to tuning structures) for simplicity.

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

* Note: For unit testing purposes, these arrays of pointers are of size [3] and [3][5] respectively and are defined as pointers to uint16 (as opposed to pointers to tuning structures) for simplicity.

#### Module specific Lookup Tables Constants

## Functions/Macros used by the Sub-Modules

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules are identified below,

Abs_f32_m

LPF_OpUpdate_f32_m

LPF_KUpdate_f32_m

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

None

### Local Functions/Macros Used by this MDD only

None

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init: TuningSelAuth_Init1

##### Design Rationale

LPF_KUpdate_f32 is used to initialize the LPF filter instead of the full LPF_Init_f32 macro as an optimization since the required initial state of the filter is 0, which is the initialized value of the RAM, so there is no need to explicitly initialize the state variables in this init function.

##### Initialize Low Pass Filters

#### Periodic Functions

##### Per: TuningSelAuth_Per1

##### Design Rationale

##### Program Flow Start

##### Rte_Call_TuningSelAuth_Per1_CP0_CheckpointReached() Store Module Inputs to Local copies

See below section

##### Description

##### Store Local copy of outputs into Module Outputs

See above section

##### Program Flow End

Rte_Call_TuningSelAuth_Per1_CP1_CheckpointReached()

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Function

None

### Transition Functions

None

## Execution Requirements

### Execution Sequence of the Module

If something besides the defaults of “0” for desired tuning set and desired personality are required at poweron, Init1 must run after the init function that provides these initial values.

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

INLINE functions defined in “GlobalMacro.h” are not unit tested

The FDD indicates that this module will store the EEPROM value for tuning set, however, this implementation doesn’t provide this block.  Instead, it is assumed that some other module will contain the tuning selection block.  This was done to enable programs that don’t have multiple tuning sets to just use the default “0” without having to manage an EEPROM block.

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| HwTorque_HwNm_f32 | HwTorque_HwNm_f32 | ActiveTunPers_Cnt_u16 |

| VehicleSpeed_Kph_f32 | VehicleSpeed_Kph_f32 | ActiveTunSet_Cnt_u16 |

| DesiredTunPers_Cnt_u16 | DesiredTunPers_Cnt_u16 | TunPer_Ptr_Str * |

| DesiredTunSet_Cnt_u16 | DesiredTunSet_Cnt_u16 | TunSet_Ptr_Str * |

|  |  |  |

|  |  |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| *HwTrqLPFiltSV_HwNm_M_str | Multiple | Multiple | Multiple | TUNINGSELAUTH_START_SEC_VAR_CLEARED_UNSPECIFIED |

| K_Uls_f32 | Single Precision Float | 0.0124877435 | 0.4665119090 |  |

| SV_HwNm_f32 | Single Precision Float | -10 | 10 |  |

| PrevTunSet_Cnt_M_u16 | 1 | 0 | 100 | TUNINGSELAUTH_START_SEC_VAR_CLEARED _16 |

| PrevTunPers_Cnt_M_u16 | 1 | 0 | 100 | TUNINGSELAUTH_START_SEC_VAR_CLEARED _16 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Constant Name |

| --- |

| k_TunSelHwTrqThresh_HwNm_f32 |

| k_TunSelVehSpdThresh_Kph_f32 |

| k_TunSelHwTrqLPFKn_Hz_f32 |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_10MS_SEC_F32 | Single Precision Float | Sec | 0.010 |

| Constant Name |

| --- |

| D_TRUE_CNT_LGC |

| D_FALSE_CNT_LGC |

| T_TunSetSelectionTbl_Ptr_Str[] * |

| T_TunPersSelectionTbl_Ptr_Str[][] * |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Data | Value |

| --- | --- |

| HwTorque_HwNm_f32 | 0 |

| VehicleSpeed_Kph_f32 | 0 |

| DesiredTunPers_Cnt_u16 | 0 |

| DesiredTunSet_Cnt_u16 | 0 |

| ActiveTunPers_Cnt_u16 | 0 |

| ActiveTunSet_Cnt_u16 | 0 |

|  |  |

|  |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| TuningSelAuth_Init1 | Once at Startup | COLDINIT |

| TuningSelAuth_Per1 | 10 ms | ALL |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| TuningSelAuth _Init1 | RTE_START_SEC_AP_TUNINGSELAUTH_APPL_CODE |

| TuningSelAuth_Per1 | RTE_START_SEC_AP_TUNINGSELAUTH_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial MDD implementing FDD SF-23 v001 | 03Jul12 | VK |

| 1 | 2.0 | Updates to provide the switching of tuning sets and personalities | 03/08/12 | LWW |

| 2 | 3.0 | Added checkpoints and memmap software segment is updated for static variables | 24-Sep-12 | Selva |

| 3 | 4.0 | Updated trigger rate for Per1 | 24-Oct-12 | BWL |

|  |  |  |  |  |
