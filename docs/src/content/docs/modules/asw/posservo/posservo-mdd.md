---
title: 'PosServo MDD'
description: 'Converted design document: PosServo MDD'
---

> **Source:** `PosServo/doc/PosServo_MDD.docx`  
> **Module:** [PosServo](../../../../asw/posservo/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module -- Position Tracking Servo

## High-Level Description

This module provides the ability for the EPS system to track a position input command.

## Figures

### Component Diagram

## Variable Data Dictionary

### Module Internal Variables

#### User defined typedef definition/declaration

## Constant Data Dictionary

### Calibration Constants

### Program(fixed) Constants

#### Embedded Constants

##### Local

##### Global

#### Module specific Lookup Tables Constants

## Functions/Macros used by the Sub-Modules

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules are identified below,

FPM_InitFixedPoint_m

TableSize_m

FPM_FloatToFixed_m

FPM_FixedToFloat_m

LPF_KUpdate_f32_m

LPF_OpUpdate_f32_m

Abs_s16_m

Limit_m

Sign_s16_m

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

None

### Local Functions/Macros Used by this MDD only

#### Filter the Desired Handwheel Angle

##### Description

#### Transition Control

##### Description

#### PID Control

##### Description

#### Output Torque

##### Description

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

### Initialization Functions

#### Init: PosServo_Init1

##### Design Rationale

None

##### Module Outputs

None

##### Module Internal

LPF_KUpdate_f32_m(k_PrkAstHwaLPFKn_Hz_f32, D_2MS_SEC_F32, &FiltHwPosKSV_M_str)

LPF_KUpdate_f32_m(k_PrkAstHwTrqLPFKn_Hz_f32, D_2MS_SEC_F32, &FiltHwTrqKSV_M_str)

LPF_KUpdate_f32_m(k_PrkAstDTermKn_Hz_f32, D_2MS_SEC_F32, &DTermKSV_M_str)

### Periodic Functions

#### Per: _Per1

##### Design Rationale

None

##### Program Flow Start

Rte_Call_PosServo_Per1_CP0_CheckpointReached

##### Store Module Inputs to Local copies

HwPos_HwDeg_T_f32 = Rte_IRead_PosServo_Per1_HandwheelPosition_HwDeg_f32()

VehSpd_Kph_T_f32 = Rte_Iread_PosServo_Per1_VehicleSpeed_Kph_f32()

VehSpd_Kph_T_u9p7 = FPM_FloatToFixed_m(VehSpd_Kph_T_f32, u9p7_T)

Active_Cnt_T_lgc = Rte_Iread_PosServo_Per1_PosSrvoEnable_Cnt_lgc()

TrgtHwAngle_HwDeg_T_f32 = Rte_IRead_PosServo_Per1_PosSrvoHwAngle_HwDeg_f32()

##### Handle Subfunctions

TransitionControl(Active_Cnt_T_lgc, &SmoothEnable_Uls_T_f32, &ReturnScale_Uls_T_f32,

&RampComplete_Cnt_T_lgc)

HwPosRateLimit_HwDegpSec_T_u12p4 = IntplVarXY_u16_u16Xu16Y_Cnt(

t_PrkAstVehSpdBS_Kph_u9p7,

t_HwaRateLimit_HwDegpSec_u12p4,

TableSize_m(t_PrkAstVehSpdBS_Kph_u9p7),

VehSpd_Kph_T_u9p7)

HwPosLimit_HwDeg_T_f32 = FPM_FixedToFloat_m(HwPosRateLimit_HwDegpSec_T_u12p4, u12p4_T) * D_2MS_SEC_F32

if( Active_Cnt_T_lgc == TRUE)

{

LimitedHwPos_HwDeg_T_f32 = Limit_m(TrgtHwAngle_HwDeg_T_f32, (PrevLimitedHwPos_HwDeg_M_f32 - HwPosLimit_HwDeg_T_f32), (PrevLimitedHwPos_HwDeg_M_f32 + HwPosLimit_HwDeg_T_f32));

}

else

{

LimitedHwPos_HwDeg_T_f32 = Limit_m(HwPos_HwDeg_T_f32, (PrevLimitedHwPos_HwDeg_M_f32 - HwPosLimit_HwDeg_T_f32), (PrevLimitedHwPos_HwDeg_M_f32 + HwPosLimit_HwDeg_T_f32));

}

PrevLimitedHwPos_HwDeg_M_f32 = LimitedHwPos_HwDeg_T_f32

TrgtAngle_HwDeg_T_f32 = FilterDesiredAngle(Active_Cnt_T_lgc, RampComplete_Cnt_T_lgc,

LimitedHwPos_HwDeg_T_f32)

PrkAstCmd_MtrNm_T_f32 = PIDControl(Active_Cnt_T_lgc, RampComplete_Cnt_T_lgc,

HwPos_HwDeg_T_f32, TrgtAngle_HwDeg_T_f32,

VehSpd_Kph_T_u9p7)

PosSrvoCmd_MtrNm_T_f32 = OutputTorque(PrkAstCmd_MtrNm_T_f32, SmoothEnable_Uls_T_f32,

VehSpd_Kph_T_u9p7)

##### Store Local copy of outputs into Module Outputs

PosSrvoRampComplete_Cnt_D_lgc = RampComplete_Cnt_T_lgc

PosSrvoHWATargFilt_HwDeg_D_f32 = TrgtAngle_HwDeg_T_f32

PosSrvoPIDCmd_MtrNm_D_f32 = PrkAstCmd_MtrNm_T_f32

Rte_Iwrite_PosServo_Per1_PosSrvoCmd_MtrNm_f32 (PosSrvoCmd_MtrNm_T_f32)

Rte_Iwrite_PosServo_Per1_PosSrvoReturnSclFct_Uls_f32(ReturnScale_Uls_T_f32)

Rte_Iwrite_PosServo_Per1_PosSrvoSmoothEnable_Uls_f32(SmoothEnable_Uls_T_f32)

##### Program Flow End

Rte_Call_PosServo_Per1_CP1_CheckpointReached

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

(Describe in words relevant details about the execution sequence of the different sub modules.)

### Execution Rates for sub-modules called by the Scheduler

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

### Local Functions

## Known Issues / Limitations With Design

INLINE functions defined in globalmacro.h are not unit tested

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| HandwheelPosition_HwDeg_f32 | HandwheelPosition_HwDeg_f32 | PosSrvoCmd_MtrNm_f32 |

| VehicleSpeed_Kph_f32 | VehicleSpeed_Kph_f32 | PosSrvoReturnSclFct_Uls_f32 |

| PosSrvoEnable_Cnt_lgc | PosSrvoEnable_Cnt_lgc | PosSrvoSmoothEnable_Uls_f32 |

| PosSrvoHwAngle_HwDeg_f32 | PosSrvoHwAngle_HwDeg_f32 |  |

| HwTorque_HwNm_f32 | HwTorque_HwNm_f32 |  |

| MotorVelCRF_MtrRadpS_f32 | MotorVelCRF_MtrRadpS_f32 |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| FiltHwPosKSV_M_str | LPF32KSV_Str |  |  | POSSERVO_START_SEC_VAR_CLEARED_UNSPECIFIED |

| FiltHwPosKSV_M_str.SV_Uls_f32 | Single Precision Floating Point | -900.0 | 900.0 |  |

| FiltHwPosKSV_M_str.K_Uls_f32 | Single Precision Floating Point | 0.0012558 | 0.2222323 |  |

| FiltHwTrqKSV_M_str | LPF32KSV_Str |  |  | POSSERVO_START_SEC_VAR_CLEARED_UNSPECIFIED |

| FiltHwTrqKSV_M_str.SV_Uls_f32 | Single Precision Floating Point | -10.0 | 10.0 |  |

| FiltHwTrqKSV_M_str.K_Uls_f32 | Single Precision Floating Point | 0.0012558 | 0.2222323 |  |

| PrkAstRampSV_Uls_M_f32 | Single Precision Floating Point | 0.0 | 1.0 | POSSERVO_START_SEC_VAR_CLEARED_32 |

| ITermSV_HwDeg_M_s27p4 | 2^-4 | -72089600 | 72089600 | POSSERVO_START_SEC_VAR_CLEARED_32 |

| DTermKSV_M_str | LPF32KSV_Str |  |  | POSSERVO_START_SEC_VAR_CLEARED_UNSPECIFIED |

| DTermKSV_M_str.SV_Uls_f32 | Single Precision Floating Point | -8.8 | 8.8 |  |

| DTermKSV_M_str.K_Uls_f32 | Single Precision Floating Point | 0.0124877 | 0.7153905 |  |

| PrevCmdError_HwDeg_M_s11p4 | 2^-4 | -1800.0 | 1800.0 | POSSERVO_START_SEC_VAR_CLEARED_16 |

| PosSrvoRampComplete_Cnt_D_lgc | n/a | FALSE | TRUE | POSSERVO_START_SEC_VAR_CLEARED_BOOLEAN |

| PosSrvoHWATargFilt_HwDeg_D_f32 | Single Precision Floating Point | -900 | 900 | POSSERVO_START_SEC_VAR_CLEARED_32 |

| PosSrvoPIDCmd_MtrNm_D_f32 | Single Precision Floating Point | -8.8 | 8.8 | POSSERVO_START_SEC_VAR_CLEARED_32 |

| PosServo_PTerm_MtrNm_D_s24p7 | 2^-7 | -8.8 | 8.8 | POSSERVO_START_SEC_VAR_CLEARED_32 |

| PosServo_ITerm_MtrNm_D_s8p7 | 2^-7 | -8.8 | 8.8 | POSSERVO_START_SEC_VAR_CLEARED_16 |

| PosServo_DTerm_MtrNm_D_s8p7 | 2^-7 | -8.8 | 8.8 | POSSERVO_START_SEC_VAR_CLEARED_16 |

| PrevLimitedHwPos_HwDeg_M_f32 | Single Precision Floating Point | -900 | 900 | POSSERVO_START_SEC_VAR_CLEARED_32 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| <None> |  |  |  |  |

| Constant Name |

| --- |

| t_PrkAstDGainY_MtrNmmSpHwDeg_u7p9[] |

| t_PrkAstDisableRateX_HwNm_u11p5[] |

| t_PrkAstDisableRateY_pSec_u12p4[] |

|  |

|  |

|  |

| k_PrkAstDTermKn_Cnt_u16 |

| k_PrkAstEnableRate_pSec_f32 |

| t_PrkAstIGainY_MtrNmpHwDegS_u2p14[] |

| t_PrkAstITermAWLmtY_MtrNm_u9p7[] |

| t_PrkAstPGainX_HwDeg_u12p4[] |

| t2_PrkAstPGainY_MtrNm_u9p7[][] |

| k_PrkAstPIDLimit_MtrNm_u9p7 |

| t_PrkAstSmoothX_Uls_u6p10[] |

| t_PrkAstSmoothY_Uls_u6p10[] |

| t_PrkAstVehSpdBS_Kph_u9p7[] |

| k_PrkAstHwaLPFKn_Cnt_u16 |

| k_PrkAstHwTrqLPFKn_Cnt_u16 |

| t_PosSrvoMaxCmdX_Kph_u9p7[] |

| t_PosSrvoMaxCmdY_MtrNm_u5p11[] |

| t_HwaRateLimit_HwDegpSec_u12p4[] |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_CONVERT_MSPLOOP_F32 | Single Precision Floating Point | mS / loop | 2.0 |

| D_PRKASTLOOPRATE_SEC_F32 | Single Precision Floating Point | Seconds | 0.002 |

| D_RECEXECRATE_PSEC_U21P11 | 2^-11 | 1 / Seconds | 500.0 |

| D_POSSERVOMINRAMP_ULS_F32 | Single Precision Floating Point | Unitless | 0.0 |

| D_POSSERVOMAXRAMP_ULS_F32 | Single Precision Floating Point | Unitless | 1.0 |

| D_RAMPCOMPLETE_ULS_U6P10 | 2^-10 | Unitelss | 0.0 |

| D_DTERMMIN_MTRNM_F32 | Single Precision Floating Point | MtrNm | -255.0 |

| D_DTERMMAX_MTRNM_F32 | Single Precision Floating Point | MtrNm | 255.0 |

| Constant Name |

| --- |

| D_2MS_SEC_F32 |

|  |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | FilterDesiredAngle | Type | Min | Max | UT Tolerance |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | Active_T_lgc | boolean | FULL | FULL |  |

|  | RampComplete_T_lgc | boolean | FULL | FULL |  |

|  | HwPos_T_f32 | float32 | -900.0 | 900.0 |  |

| Return Value | TrgtHwAngle_HwDeg_T_f32 | float32 | -900.0 | 900.0 | 6.25E-02 |

| Function Name | TransitionControl | Type | Min | Max | UT Tolerance |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | Active_T_lgc | boolean | FULL | FULL |  |

|  | pSmoothEnable_T_f32 | float32 pointer | 0.0 | 1.0 |  |

|  | pReturnScl_T_f32 | float32 pointer | 0.0 | 1.0 |  |

|  | pRampComplete_T_lgc | boolean pointer | FULL | FULL |  |

| Return Value | N/A |  |  |  |  |

| Function Name | PIDControl | Type | Min | Max | UT Tolerance |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | Active_T_lgc | boolean | FULL | FULL |  |

|  | RampComplete_T_lgc | boolean | FULL | FULL |  |

|  | HwPos_T_f32 | float32 | -900.0 | 900.0 |  |

|  | DesiredHwAngle_T_f32 | float32 | -900.0 | 900.0 |  |

|  | VehSpd_T_u9p7 | uint16 | 0.0 | 511.9921875 |  |

| Return Value | TmpPrkAssist_MtrNm_T_f32 | float32 | -8.8 | 8.8 | 7.81E-03 |

| Function Name | OutputTorque | Type | Min | Max | UT Tolerance |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | PrkAstCmd_T_f32 | float32 | -8.8 | 8.8 |  |

|  | SmoothEnable_T_f32 | float32 | 0.0 | 1.0 |  |

|  | VehSpd_T_u9p7 | uint16 | 0.0 | 511.9921875 |  |

| Return Value | PrkAstCmd_MtrNm_T_f32 | float32 | -8.8 | 8.8 | 2.38E-08 |

| Data | Value |

| --- | --- |

| Rte_InitValue_HandwheelPosition_HwDeg_f32 | 0 |

| Rte_InitValue_HwTorque_HwNm_f32 | 0 |

| Rte_InitValue_MotorVelCRF_MtrRadpS_f32 | 0 |

| Rte_InitValue_PosSrvoCmd_MtrNm_f32 | 0 |

| Rte_InitValue_PosSrvoEnable_Cnt_lgc | FALSE |

| Rte_InitValue_PosSrvoHwAngle_HwDeg_f32 | 0 |

| Rte_InitValue_PosSrvoReturnSclFct_Uls_f32 | 1 |

| Rte_InitValue_PosSrvoSmoothEnable_Uls_f32 | 0 |

| Rte_InitValue_VehicleSpeed_Kph_f32 | 0 |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| PosServo_Init1 | On Event | On Init |

| PosServo_Per1 | 2 ms | WARM INIT, OPERATE, DISABLE |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| <None> |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| PosServo_Init1 | RTE_START_SEC_AP_POSSERVO_APPL_CODE |

| PosServo_Per1 | RTE_START_SEC_AP_POSSERVO_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

| FilterDesiredAngle | RTE_START_SEC_AP_POSSERVO_APPL_CODE |

| TransitionControl | RTE_START_SEC_AP_POSSERVO_APPL_CODE |

| PIDControl | RTE_START_SEC_AP_POSSERVO_APPL_CODE |

| OutputTorque | RTE_START_SEC_AP_POSSERVO_APPL_CODE |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1 | Initial version | 07-Jun-11 | YY |

| 2 | 2 | Corrected anomaly 2371 to prevent potential overflow of intermediate D-Term calculation. | 16-Jun-11 | YY |

| 3 | 3 | Initial version for PosServo CBD | 16-Dec-11 | VK |

| 4 | 4 | Changed VehSpd_T_u12p4 to u9p7 and changed the precision for the table associated. | 09-Jan-12 | VK |

| 5 | 5 | Changed the range for hand wheel position to be +/-900 throughout and updated the software segment | 02-02-12 | VK |

| 6 | 6 | Updated to SF-20 v002 | 01-Aug-12 | OT |

| 7 | 7 | Fixed UTP Issue (typecasting bilinear interpolation overflow) | 08-Aug-12 | OT |

| 8 | 8 | Fixed more UTP issues (fixed point math overflow) | 10-Aug-12 | OT |

| 9 | 9 | Updated to SF-20 v003 | 29-Aug-12 | KJS |

| 10 | 10.0 | Added checkpoints and memmap software segment is updated for static variables | 21-Sep-12 | Selva |

| 11 | 11 | UTP corrections to MDD | 19-Oct-12 | KJS |

| 12 | 12 | UTP corrections to MDD | 19-Oct-12 | KJS |

| 13 | 13 | Updated to SF v004 | 15-Mar-13 | SP |

|  |  |  |  |  |
