---
title: 'GCCDiag MDD'
description: 'Converted design document: GCCDiag MDD'
---

> **Source:** `SF46_GCCDiag_Implementation/doc/GCCDiag_MDD.docx`  
> **Module:** [SF46_GCCDiag_Implementation](../../../../asw/sf46_gccdiag_implementation/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module – Gross Cross Check Diagnostic

## High-Level Description

This module computes the Gross Cross Check Diagnostics.  It takes the handwheel torque,vehicle speed ,Motor Nm to diagnose .

## Figures

### Component Diagram

## Variable Data Dictionary

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

### Module Internal Variables

This section identifies the name, range and resolutions for module specific data created by this module.  If there are no range restrictions on the variable, the term “FULL” is placed into the table for legal range.

#### User defined typedef definition/declaration

This section documents any user types uniquely used for the module.

### Module Display Variables

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

(This is for lookup tables (arrays) with fixed values, same name as other tables)

## Functions/Macros used by the Sub-Modules

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules are identified below,

FPM_FloatToFixed_m()

- FPM_FixedToFloat_m

BilinearXMYM_u16_s16XMu16YM_Cnt ()

LPF_Init_f32_m()

LPF_OpUpdate_f32_m ()

LPF_KUpdate_f32_m()

Tablesize_m()

DiagPStep_m()

DiagNStep_m()

DiagFailed_m()

### Data Hiding Functions

Rte_Call_NxtrDiagMgr_SetNTCStatus()

### Global Functions/Macros Defined by this Module

None

### Local Functions/Macros Used by this MDD only

None

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init: GCCDiag_Init1

##### Design Rationale

The two filters need the initialization of filter constants only and the state variables are initialized to zero by MemMap section.

##### Module Outputs

None

##### Module Internal

LPF_KUpdate_f32_m(D_FILTERFRQ_HZ_F32, D_2MS_SEC_F32, &GCCDiag_HwTrqLPF_M_str);

LPF_KUpdate_f32_m(D_FILTERFRQ_HZ_F32, D_2MS_SEC_F32, &GCCDiag_MtrTrqLPF_M_str);

### Periodic Functions

#### Per: GCCDiag_Per1

##### Design Rationale

The Code has been optimized to remove the Inverter for the variable MtrCmdOk_T_lgc , the functionality is same as FDD.

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

/* Read the Inputs to the Temporary Variables */

HwTorque_HwNm_T_f32 = Rte_IRead_GCCDiag_Per1_HwTorque_HwNm_f32();

VehicleSpeed_Kph_T_f32 = Rte_IRead_GCCDiag_Per1_VehicleSpeed_Kph_f32();

MRFMtrTrqCmdScl_MtrNm_T_f32 = Rte_IRead_GCCDiag_Per1_MRFMtrTrqCmdScl_MtrNm_f32();

DftGrossCCDiag_Cnt_T_lgc = Rte_IRead_GCCDiag_Per1_DftGrossCCDiag_Cnt_lgc();

/* Fault Injection for the HwTrq,MtrTrq and VehSpd */

#if (STD_ON == BC_GCCDIAG_FAULTINJECTIONPOINT)

Rte_Call_FltInjection_SCom_FltInjection(&HwTorque_HwNm_T_f32, FLTINJ_GCCDIAG_HWTRQ);

Rte_Call_FltInjection_SCom_FltInjection(&VehicleSpeed_Kph_T_f32, FLTINJ_GCCDIAG_VEHSPD);

Rte_Call_FltInjection_SCom_FltInjection(&MRFMtrTrqCmdScl_MtrNm_T_f32, FLTINJ_GCCDIAG_MTRTRQ);

#endif

##### Gross Cross Check Diagnostics

##### Store Local copy of outputs into Module Outputs

##### Program Flow End

N/A

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

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

- INLINE functions defined in globalmacro.h are not unit tested

Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| HwTorque_HwNm_f32 | HwTorque_HwNm_f32 |  |

| DftGrossCCDiag_Cnt_lgc | DftGrossCCDiag_Cnt_lgc |  |

| MRFMtrTrqCmdScl_MtrNm_f32 | MRFMtrTrqCmdScl_MtrNm_f32 |  |

| VehicleSpeed_Kph_f32 | VehicleSpeed_Kph_f32 |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| GCCDiag_HwTrqLPF_M_str | See Data Dictionary | See Data Dictionary | See Data Dictionary | GCCDIAG_START_SEC_VAR_CLEARED_UNSPECIFIED |

| GCCDiag_MtrTrqLPF_M_str | See Data Dictionary | See Data Dictionary | See Data Dictionary | GCCDIAG_START_SEC_VAR_CLEARED_UNSPECIFIED |

| GCCDiag_PNAccumulator_Cnt_M_u16 | See Data Dictionary | See Data Dictionary | See Data Dictionary | GCCDIAG_START_SEC_VAR_CLEARED_16 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Variable Name | Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- | --- |

| GCCDiag_PNAccumulator_Cnt_D_u16 | See Data Dictionary | See Data Dictionary | See Data Dictionary | GCCDIAG_START_SEC_VAR_CLEARED_16 |  |

| Constant Name |

| --- |

| k_GCC_PNSettings_str |

| t_GCC_VehSpd_Kph_u9p7 |

| t2_GCC_UprBoundX_HwNm_s4p11 |

| t2_GCC_UprBoundY_MtrNm_u4p12 |

|  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_FILTERFRQ_HZ_F32 | Single precision floating point | Hetrz | 1 |

| Constant Name |

| --- |

| D_NEGONE_CNT_S16 |

| D_2MS_SEC_F32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Data | Value |

| --- | --- |

| None |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| GCCDiag_Init1() | Once (at initialization) | COLD INIT |

| GCCDiag_Per1() | 2 ms | ALL |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| GCCDiag_Init1() | RTE_AP_GCCDIAG_APPL_CODE |

| GCCDiag_Per1() | RTE_AP_GCCDIAG_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1.0 | Initial Version per SF46 Gross Cross Check Diagnostics | 26-Aug-14 | VS |
