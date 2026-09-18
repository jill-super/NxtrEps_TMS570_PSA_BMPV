---
title: 'State Output Control MDD'
description: 'Converted design document: State Output Control MDD'
---

> **Source:** `StOpCtrl/doc/State_Output_Control_MDD.docx`  
> **Module:** [StOpCtrl](../../../../asw/stopctrl/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module – State Output Control

## High-Level Description

This function performs the ramp up and ramp down of the Torque Command.

## Figures

### Diagram – Function Data Sharing

## Variable Data Dictionary

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

(Note: Full variable names required in table.)

(Note: All global variables including End Of Line data used should be shown here)

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

(This is for lookup tables (arrays) with fixed values, same name as other tables)

### Lookup Table Definitions

## Software Module Implementation

### Initialization Functions

None

### Periodic Functions

#### Per: _Per1

##### Design Rationale

NOTE: For “starttime” calculations there is tendency for underflow and this is expected in s/w design. So for unittesting, VBA model should be implemented

such that it handles underflow and behaves like source code design.

##### Program Flow Start

##### Store Module Inputs to Local copies

OperRampRate_XpmS_T_f32 as float32

OperRampValue_Uls_T_f32 as float32

DiagRampValue_Uls_T_f32 as float32

DiagRampRate_XpmS_T_f32 as float32

DiagStsDiagRmpActive_Cnt_T_lgc as Boolean

RampSrlComSvcDft_Cnt_T_lgc as Boolean

Rate_T_f32 as float32

Target_T_f32 as float32

DiffOutputRampMult_T_f32 as float32

DiffRate_T_f32 as float32

OperRampRate_XpmS_T_f32 = Rte_IRead_StOpCtrl_Per1_OperRampRate_XpmS_f32

OperRampValue_Uls_T_f32 =Rte_Iread_StOpCtrl_Per1_OperRampValue_Uls_f32

DiagRampValue_Uls_T_f32=Rte_Iread_StOpCtrl_Per1_DiagRampValue_Uls_f32

DiagRampRate_XpmS_T_f32=Rte_Iread_StOpCtrl_Per1_DiagRampRate_XpmS_f32

DiagStsDiagRmpActive_Cnt_T_lgc = Rte_Iread_StOpCtrl_Per1_DiagStsDiagRmpActive_Cnt_lgc

RampSrlComSvcDft_Cnt_T_lgc= Rte_Iread_StOpCtrl_Per1_RampSrlComSvcDft_Cnt_lgc

##### Store Local copy of outputs into Module Outputs

Rte_Iwrite_StOpCtrl_Per1_RampDwnStatusComplete_Cnt_lgc(RampDwnStatusComplete_T_lgc)

Rte_Iwrite_StOpCtrl_Per1_OutputRampMult_Uls_f32(NewOutputRampMult_T_f32)

##### Program Flow End

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

None

### Local Function/Macro Definitions

#### RampLib

##### *Note: For ranges on structure elements check Table 3.1.1 of MDD

##### Description

Rte_Call_SystemTime_DtrmnElapsedTime_mS_u32(rampState_T_Str.StartTime_mS_u32, &ElapsedRamp_mS_T_u32)

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

(Item #1)

## Revision Control Log

| Module Inputs (Global Variable Name) | Module Outputs (Global Variable Name) |

| --- | --- |

| TrqCmd_MtrNm_f32 | FinalTrqCmd_MtrNm_f32 |

| SrlComSvcDft_Cnt_b32 | OutputRampMult_Uls_f32 |

| DiagRampRate_XpmS_32 | RampDwnStatusComplete_Cnt_lgc |

| DiagRampValue_Uls_f32 |  |

| OperRampRate_XpmS_f32 |  |

| OperRampValue_Uls_f32 |  |

| RampSrlComSvcDft_Cnt_lgc |  |

| DiagStsDiagRmpActive_Cnt_lgc |  |

| Variable Name | Resolution | (min) | (max) | Software Segment |

| --- | --- | --- | --- | --- |

| AttenFactor_Uls_M_f32 | Single precision floating point | 1.175494351e-038 | 3.402823466e+038 |  |

| ActvRampUsr_Cnt_M_u16 | 1 | 0 | 16 |  |

| PrevOutputRampMult_Uls_M_f32 | Single precision floating point | 0 | 1 | STOPCTRL_START_SEC_VAR_NOINIT_32 |

| PrevTargetRampMult_Uls_M_f32 | Single precision floating point | 0 | 1 | STOPCTRL_START_SEC_VAR_NOINIT_32 |

| PrevRate_XpmS_M_f32 | Single precision floating point | 0.0001 | 0.5 | STOPCTRL_START_SEC_VAR_NOINIT_3 |

| RampState_M_Str | RampState_T | See 3.1.1 | See 3.1.1 | STOPCTRL_START_SEC_VAR_NOINIT_UNSPECIFIED |

| Typedef Name | Element Name | User Defined Type | (min) | (max) |

| --- | --- | --- | --- | --- |

| RampState_T | StartTime_mS_u32<br/>Duration_mS_u32<br/>StartVal_Uls_f32<br/>EndVal_Uls_f32 | uint32<br/>uint32<br/>float32<br/>float32 | 0<br/>0<br/>0<br/>0 | 2^32-1<br/>2^32-1<br/>1<br/>1 |

| Constant Name |

| --- |

|  |

| Constant Name | Resolution | Value |

| --- | --- | --- |

| D_TWO_MS_U32 | 1 | 2 |

| D_MAXRAMP_XPMS_F32 | Single precision floating point | 0.5 |

| Constant Name |

| --- |

|  |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | RampLib | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | rampState_T_Str | RampState_T | * | * |

|  |  |  |  |  |

| Return Value | Output_Uls_T_f32 | Float |  |  |

| Function Name | Calling Frequency | in which the function is called |

| --- | --- | --- |

| StOpCtrl_Per1() | 2 ms | ALL States |

|  |  |  |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| StOpCtrl_Per1() | RTE_START_SEC_AP_STOPCTRL_APPL_CODE RTE_STOP_SEC_AP_STOPCTRL_APPL_CODE |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| RampLib | RTE_START_SEC_AP_STOPCTRL_APPL_CODE<br/>RTE_STOP_SEC_AP_STOPCTRL_APPL_CODE |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial release | 07-Jun-11 | SAH |

| 2 | 2.0 | FDD SF05 | 5-Jan-12 | NRAR |

| 3 | 3.0 | Value for D_MAXRAMP_XPMS_F32  is fixed | 6-Jan-12 | NRAR |

| 4 | 4.0 | DiagStsF1Active_Cnt_lgc is renamed to DiagStsDiagRmpActive_Cnt_lgc | 12-Jan-12 | NRAR |

| 5 | 4.0 | PrevRate_XpmS_M_f32 range correction | 23-Jan-12 | NRAR |

| 6 | 5.0 | Anom #3272 Ramp output vs. target fix | 13-Aug-12 | BWL |

|  |  |  |  |  |
