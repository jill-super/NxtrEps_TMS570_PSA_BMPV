---
title: 'PeakCurrEst MDD'
description: 'Converted design document: PeakCurrEst MDD'
---

> **Source:** `MtrCtrl_CM/doc/PeakCurrEst_MDD.docx`  
> **Module:** [MtrCtrl_CM](../../../../asw/mtrctrl_cm/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module – PeakCurrEst

## High-Level Description

## Figures

### Component Diagram

### Variable Data Dictionary

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

LPF_SvUpdate_u16InFixKTrunc_m

LPF_OpUpdate_u16InFixKTrunc_m

LPF_SvUpdate_s16InFixKTrunc_m

LPF_OpUpdate_s16InFixKTrunc_m

FPM_FloatToFixed_m

FPM_FixedToFloat_m

Limit_m

### Data Hiding Functions

None

### Global Functions/Macros Defined by this Module

None

### Local Functions/Macros Used by this MDD only

None

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

None

### Initialization Functions

None

### Periodic Functions

#### Per: PeakCurrEst_Per1

##### Design Rationale

None

##### Program Flow Start

Rte_Call_PeakCurrEst_Per1_CP0_CheckpointReached

##### Store Module Inputs to Local copies

EstMtrCurrQax_Amp_T_f32=Rte_IRead_PeakCurrEst_Per1_MtrCurrQax_Amp_f32()

EstMtrCurrDax_Amp_T_f32=Rte_IRead_PeakCurrEst_Per1_MtrCurrDax_Amp_f32()

##### Module Design

##### Store Local copy of outputs into Module Outputs

Rte_IWrite_PeakCurrEst_Per1_EstPkCurr_AmpSq_f32(EstPkCurr_AmpSq_T_f32)

##### Program Flow End

Rte_Call_PeakCurrEst_Per1_CP1_CheckpointReached

#### Per: PeakCurrEst_Per2

##### Design Rationale

##### Program Flow Start

Rte_Call_PeakCurrEst_Per2_CP0_CheckpointReached()

##### Module Design

##### Store Local copy of outputs into Module Outputs

Rte_IWrite_PeakCurrEst_Per2_FiltEstPkCurr_AmpSq_f32(FiltEstPkCurr_AmpSq_T_f32)

##### Program Flow End

##### Rte_Call_PeakCurrEst_Per2_CP1_CheckpointReached()

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

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

## Known Issues / Limitations With Design

INLINE functions defined in GlobalMacro.h are not unit tested.

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| MtrCurrQax_Amp_f32 | MtrCurrQax_Amp_f32 | EstPkCurr_AmpSq_f32 |

| MtrCurrDax_Amp_f32 | MtrCurrDax_Amp_f32 | FiltEstPkCurr_AmpSq_f32 |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| QaxCurrFiltSV_Amp_M_u12p20 | Single Precision Float | -220 | 220 | PEAKCURREST_START_SEC_VAR_CLEARED_32 |

| DaxCurrFiltSV_Amp_M_s11p20 | Single Precision Float | -220 | 220 | PEAKCURREST_START_SEC_VAR_CLEARED_32 |

| EstPkCurr_AmpSq_M_f32 | Single Precision Float | 0 | 48400 | PEAKCURREST_START_SEC_VAR_CLEARED_32 |

| EstPkCurrFiltSV_AmpSq_M_u16p16 | Single Precision Float | 0 | 48400 | PEAKCURREST_START_SEC_VAR_CLEARED_32 |

| FiltMtrCurEst_Id_Amp_D_f32 | Single Precision Float | -220 | 220 | PEAKCURREST_START_SEC_VAR_CLEARED_32 |

| MtrCurEst_Iq_AmpSq_D_f32 | Single Precision Float | -220 | 220 | PEAKCURREST_START_SEC_VAR_CLEARED_32 |

| MtrCurEst_Id_AmpSq_D_f32 | Single Precision Float | 0 | 48400 | PEAKCURREST_START_SEC_VAR_CLEARED_32 |

| FiltMtrCurEst_Iq_Amp_D_f32 | Single Precision Float | 0 | 48400 | PEAKCURREST_START_SEC_VAR_CLEARED_32 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Constant Name |

| --- |

| k_EstPkCurr2msLPFKn_Uls_u16 |

| k_EstPkCurrSlowLoopLPFKn_Uls_u16 |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| None |  |  |  |

|  |  |  |  |

| Constant Name |

| --- |

| D_ESTPKCURRLOLMT_AMPSQ_F32 |

| D_ESTPKCURRHILMT_AMPSQ_F32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| PeakCurrEst_Per1 | 2ms |  |

| PeakCurrEst_Per2 | 100ms |  |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| PeakCurrEst_Per1 | RTE_AP_PEAKCURREST_APPL_CODE |

| PeakCurrEst_Per2 | RTE_AP_PEAKCURREST_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial Version | 5/15/2012 | KPIT-RD |

| 2 | 2.0 | Addition of checkpoints and memmap statements | 20-Nov-12 | Selva |

|  |  |  |  |  |
