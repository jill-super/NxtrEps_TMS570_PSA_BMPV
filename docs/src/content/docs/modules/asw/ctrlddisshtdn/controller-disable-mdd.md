---
title: 'Controller Disable MDD'
description: 'Converted design document: Controller Disable MDD'
---

> **Source:** `CtrldDisShtdn/doc/Controller_Disable_MDD.docx`  
> **Module:** [CtrldDisShtdn](../../../../asw/ctrlddisshtdn/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module -- Controlled Disable Shutdown

## High-Level Description

The Controlled Disable Damping Shutdown method is used for torque sensor failures.  When the torque sensor fails, an output torque is computed based on motor velocity to reduce the amount of “handwheel kick” perceived by the driver.

## Figures

### Component Diagram

## Module Inputs and Outputs

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

## Software Module Implementation

### Initialization Functions

None

### Periodic Functions

#### Per: CntrlDisableShutdown_Per1

##### Design Rationale

This function is used to damp out handwheel “kick” in the event of a torque sensor fault (or any F2 fault).  The design is such that either when the motor velocity is low OR when a time based multiplier has expired, the system will realize the action is complete and state changes can be made (states and modes).

The design takes into account that F2 type faults could be recoverable, so the “reset” feature is built into the design

##### Program Flow Start

Rte_Call_CtrldDisShtdn_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

Local Variables :

CRFMtrVelSign_T_f32

AbsCRFMtrVel_T_MtrRadpS_f32

CntrlDamp_VelTrq_T_f32

ElapsedTime_mS_T_u16

CntrlDmpMult_Uls_T_f32

CntrlDampComp_Cnt_T_lgc

DiagStsF2Active_Cnt_T_lgc

CntrlDamp_MtrNm_T_f32

AssistAssyPolarity_Cnt_T_s08

MRFMtrTrqCmd_MtrNm_T_f32

SysState_Cnt_T_Enum  as Rte_ModeType_StaMd_Mode

SysState_Cnt_T_Enum = Rte_Mode_SystemState_Mode()

t_CtrlDmpTmrX_T_u16 [D_CNTRLDMPTMRSZ_CNT_U16] = { k_CtrlDmpTmrBkptOne_mS_f32, k_CtrlDmpTmrBkptTwo_mS_32}

t_CtrlDmpTmrY_T_u8P8 [D_CNTRLDMPTMRSZ_CNT_U16] = { FPM_InitFixedPoint_m(1.0,u8p8_T), k_CntrlDmpRampEnd_Uls_u8p8}

_MtrNm_T_f32 = Rte_IRead_CtrldDisShtdn_Per1__MtrNm_f32()

CRFMtrVel_MtrRadpS_T_f32 = Rte_Iread_CtrldDisShtdn_Per1_CRFMtrVel_MtrRadpS_f32()

DiagStatus_Cnt_T_b32 = Rte_Iread_CtrldDisShtdn_Per1_DiagStsF2Active_Cnt_lgc()

AssistAssyPolarity_Cnt_T_s08 = Rte_IRead_CtrldDisShtdn_Per1_AssistAssyPolarity_Cnt_s08()

##### Compute Damping Torque

##### Controlled Damping Factor

##### Switch Output Control

##### Store Local copy of outputs into Module Outputs

Rte_Iwrite_CtrldDisShtdn_Per1__MtrNm_f32(CRFMtrTrqCmd_MtrNm_T_f32)

Rte_Iwrite_CtrldDisShtdn_Per1_CtrldDmpStsCmp_Cnt_lgc(CntrlDampComp_Cnt_T_lgc)

Rte_IWrite_CtrldDisShtdn_Per1__MtrNm_f32(MRFMtrTrqCmd_MtrNm_T_f32)

Rte_IWrite_CtrldDisShtdn_Per1_SysC_CRFMtrTrqCmd_MtrNm_f32(CRFMtrTrqCmd_MtrNm_T_f32)

##### Program Flow End

### Rte_Call_CtrldDisShtdn_Per1_CP1_CheckpointReached()

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

None

### Local Function/Macro Definitions

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

INLINE functions in GlobalMacro.h are not unit tested

## Revision Control Log

| Module Inputs (Global Variable Name) | Module Outputs (Global Variable Name) |

| --- | --- |

| _MtrNm_f32 | _MtrNm_f32 |

| CRFMtrVel_MtrRadpS_f32 | CtrldDmpCmp_Cnt_lgc |

| DiagStsF2Active_Cnt_lgc | _MtrNm_f32 |

| AssistAssyPolarity_Cnt_s08 | SysC_CRFMtrTrqCmd |

|  |  |

| Variable Name | Resolution | (min) | (max) | Software Segment |

| --- | --- | --- | --- | --- |

| CntrlDampVelTrq_MtrNm_D_f32 | Single Precision Float | -2200 | 2200 | CTRLDDISSHTDN_START_SEC_VAR_CLEARED_32 |

| CntrlDampElpsdTime_mS_D_u16 | 1 | FULL | FULL | CTRLDDISSHTDN_START_SEC_VAR_CLEARED_16 |

| LastF2Fault_mS_M_u32 | 1 | 0 | 1000 | CTRLDDISSHTDN_START_SEC_VAR_CLEARED_32 |

| CntrlDampTrq_MtrNm_D_f32 | Single Precision Float | -5.75 | 5.75 | CTRLDDISSHTDN_START_SEC_VAR_CLEARED_32 |

| Variable Name | Typedef Name | Storage Type | Safety Critical Classification |

| --- | --- | --- | --- |

| None |  |  |  |

| Constant Name |

| --- |

| k_F2Damping_MtrNmpRadpS_f32 |

| k_CtrlDpVelThr_MtrRadpS_f32 |

| k_CntrlDmpRampEnd_Uls_u8p8 |

| k_MaxCtrlDmpLimit_MtrNm_f32 |

| k_CtrlDmpTmrBkptOne_mS_u16 |

| k_CtrlDmpTmrBkptTwo_mS_u16 |

| Constant Name | Resolution | Value |

| --- | --- | --- |

| D_CNTRLDMPTMRSZ_CNT_U16 | 1 | 2 |

| D_CTRLDMPRES_MTRNM_F32 | Single Precision Floating Point | 0.007813 |

| Constant Name |

| --- |

| D_ZERO_ULS_F32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

|  |  |  |  |

| Function Name | Task List | Calling Frequency | in which the function is called |

| --- | --- | --- | --- |

| CntrlDisableShutdown_Per1 |  | 2ms | WARMINIT, OPERATE, DISABLE |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| CntrlDisableShutdown__Per1 | RTE_START_SEC_AP_CTRLDDISSHTDN_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial release | 08Dec11 | M. Story |

| 2 | 2.0 | Correcting values in t_CtrlDmpTmrY_T_u8P8 | 19Jan12 | M. Story |

| 3 | 3.0 | Correcting values in t_CtrlDmpTmrY_T_u8P8 using FPM_InitFixedPoint_m | 19Jan12 | M. Story |

| 4 | 4.0 | Corrected misspelled variable names. | 24Jan12 | M. Story |

| 5 | 5.0 | Updates made as per FDD SF26 Ver002 | 14May12 | NRAR |

| 6 | 6.0 | Anom 3252 fix and Mode port added to make Trq zero if not in OPERATE State | 16 May 12 | NRAR |

| 7 | 7.0 | Updated to SF-26 v003 | 7-Jun-12 | OT |

| 8 | 8.0 | Added watchdog checkpoints. | 16-Sept-12 | B WL |

| 9 | 9.0 | Corrected Internal variable software segment type | 19-Sep-12 | SSK |

| 10 | 10 | Corrected for Watchdog naming error | 24-Sep-12 | Selva |

| 11 | 11 | Redundant storage of CRFMtrTrqCmd | 04-Oct-12 | NRAR |

|  |  |  |  |  |
