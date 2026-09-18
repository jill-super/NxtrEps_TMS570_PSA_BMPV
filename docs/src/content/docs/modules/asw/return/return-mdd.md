---
title: 'Return MDD'
description: 'Converted design document: Return MDD'
---

> **Source:** `Return/doc/Return_MDD.docx`  
> **Module:** [Return](../../../../asw/return/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module  -- Return

## High-Level Description

This function uses the Absolute Hand Wheel position, Hand Wheel Torque, Hand Wheel Velocity and Vehicle Speed to derive the desired Return Torque command.

## Figures

None

#### Diagram – _L5_Per

This diagram describes the functional characteristics and data flow of a given function.

## Module Inputs and Outputs

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

(Note: Full variable names required in table.)

(Note: All global variables including End Of Line data used should be shown here)

### Module Internal Variables

This section identifies the name, range and resolutions for module specific data created by this module.  If there are no range restrictions on the variable, the term “FULL” is placed into the table for legal range.

(Note: If no module specific variables are used by the design, place the text “None” in the first Variable Name cell in the table)

#### User defined typedef definition/declaration

This section documents any user types uniquely used for the module.

## Constant Data Dictionary

### Calibration Constants

This section lists the calibrations used by the module.  For details on calibration constants, refer to the Data Dictionary for the application.

(Note: If no calibrations are used by the design, place the text “None” in the first location in the table)

### Program(fixed) Constants

#### Embedded Constants

All embedded constants whose values are provided in Eng units will be evaluated to the equivalent counts by using the FPM_InitFixedPoint_m() macro within the #define statement.

##### Local

##### Note: RtnLoopTime depends on the rate of the periodic function.

##### Global

This section lists the global constants used by the module.  For details on global constants, refer to the Data Dictionary for the application.

#### Module specific Lookup Tables Constants

(This is for lookup tables (arrays) with fixed values, same name as other tables)

## Software Module Implementation

### Initialization Functions

#### Init: _L5_Init()

##### Design Rationale

None

##### Module Outputs

None

##### Module Internal

None

### Periodic Functions

#### Per: _L5_Per

##### Design Rationale

None

##### Program Flow Start

Rte_Call_Return_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

HwVel_HwRadpS_T_f32 = Rte_IRead_Return_Per1_HandwheelVel_HwRadpS_f32 ()

FinHwPosAuth_Uls_T_f32 = Rte_IRead_Return_Per1_HandwheelAuthority_Uls_f32 ()

FinHwPos_HwDeg_T_f32 = Rte_IRead_Return_Per1_HandwheelPosition_HwDeg_f32 ()

HwTrq_HwNm_T_f32 = Rte_IRead_Return_Per1_HwTorque_HwNm_f32 ()

DrvDynSclFct_Uls_T_f32 = Rte_IRead_Return_Per1_ReturnDDFactor_Uls_f32()

PrkAstSclFct_Uls_T_f32 = Rte_IRead_Return_Per1_PAReturnSclFct_Uls_f32 ()

AssistMechTempEst_T_DegC_f32 = Rte_IRead_Return_Per1_AssistMechTempEst_DegC_f32()

ReturnOffset_HwDeg_T_f32 = Rte_IRead_Return_Per1_ReturnOffset_HwDeg_f32()

VehSpd_Kph_T_f32 = Rte_IRead_Return_Per1_VehSpd_Kph_f32 ()

DiagStsHwPosDis_Cnt_T_lgc = Rte_IRead_Return_Per1_ DiagStsHwPosDis_Cnt_lgc ()

VehSpd_Kph_T_u9p7 = FPM_FloatToFixed_m(VehSpd_Kph_T_f32, u9p7_T)FinHwPosAuth_Uls_T_u8p8 = FPM_FloatToFixed_m(FinHwPosAuth_Uls_T_f32, u8p8_T)

FinHwPos_HwDeg_T_s11p4 = FPM_FloatToFixed_m(FinHwPos_HwDeg_T_f32, s11p4_T)

HwTrq_HwNm_T_s7p8 = FPM_FloatToFixed_m(HwTrq_HwNm_T_f32, s7p8_T)

HwVel_HwRadpS_T_s6p9 = FPM_FloatToFixed_m(HwVel_HwRadpS_T_f32, s6p9_T)

AssistMechTempEst_DegC_T_s11p4 = FPM_FloatToFixed_m(AssistMechTempEst_DegC_f32, s11p4_T)

Local Variables:

HwVel_HwRadpS_T_f32

FinHwPosAuth_Uls_T_f32

FinHwPos_HwDeg_T_f32

HwTrq_HwNm_T_f32

VehSpd_Kph_T_f32

VehSpd_Kph_T_u9p7

FinHwPos_HwDeg_T_s11p4

HwTrq_HwNm_T_s7p8

HwVel_HwRadpS_T_s6p9

HwPosReturnCmd_MtrNm_T_u5p11

HwPosReturnCmd_MtrNm_T_f32

HwTrqReturnScl_Uls_T_u8p8

HwTrqReturnScl_Uls_T_f32

HwVelReturnScl_Uls_T_u8p8

HwVelReturnScl_Uls_T_f32

ReturnCmd_MtrNm_T_f32

DrvDynSclFct_Uls_T_f32

PrkAstSclFct_Uls_T_f32

AssistMechTempEst_T_DegC_f32

ReturnOffset_HwDeg_T_f32

FinHwPosAuth_Uls_T_u8p8

AssistMechTempEst_DegC_T_s11p4

TempReturnScl_Uls_T_u8p8

TempReturnScl_Uls_f32

ScaledReturn_MtrNm_f32

HandWheelAthScl_Pct_T_u10p6

CrntHandWheelAthScl_Uls_f32

OffsetDiff_HwDeg_T_u9p7

OffsetDiff_HwDeg_T_u10p6

HandWheelAthScl_Uls_T_u10p6

DiagStsHwPosDis_Cnt_T_lgc

EOLRtnRange_MtrNm_T_f32

HwPosReturnCmd_MtrNm_T_f32

CurrentOffset_HwDeg_T_s11p4

HandWheelAthScl_Uls_T_f32

##### Determine Return Command

###### Input Conditioning

###### Hand Wheel Position Return Command

The return command is determined as a function of Hand Wheel Position and Vehicle Speed.

###### Hand Wheel Torque Return Multiplier

The return command is scaled between 0 and 100 percent as a function of Hand Wheel Torque and Vehicle Speed.

###### Hand Wheel Velocity Return Multiplier

The return command is scaled between 0 and 100 percent as a function of Hand Wheel Velocity and Vehicle Speed.

###### Calculate Temperature Dependant Return Multiplier

###### Return Scale

###### Calculate Return Torque

##### Store Local copy of outputs into Module Outputs

Rte_IWrite_Return_Per1_ReturnCmd_MtrNm_f32(ReturnCmd_MtrNm_T_f32)

HwPosReturnCmd_MtrNm_D_f32 = HwPosReturnCmd_MtrNm_T_f32

HwTrqReturnScl_Uls_D_f32 = HwTrqReturnScl_Uls_T_f32

HwVelReturnScl_Uls_D_f32 = HwVelReturnScl_Uls_T_f32

TempReturnScl_Uls_D_f32 = TempReturnScl_Uls_f32

##### Program Flow End

Rte_Call_Return_Per1_CP1_CheckpointReached()

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

None

## Revision Control Log

| Module Inputs (Global Variable Name) | Module Outputs (Global Variable Name) |

| --- | --- |

| HandwheelVel_HwRadpS_f32 | ReturnCmd_MtrNm_f32 |

| HandwheelAuthority_Uls_f32 |  |

| HandwheelPosition_HwDeg_f32 |  |

| HwTorque_HwNm_f32 |  |

| VehicleSpeed_Kph_f32 |  |

| SrlComSvcDft_Cnt_b32 |  |

| ReturnDDFactor_Uls_f32 |  |

| PAReturnSclFct_Uls_f32 |  |

| Return Offset_HwDeg_f32 |  |

| AssistMechTempEst_DegC_f32 |  |

|  |  |

| Variable Name | Resolution | (min) | (max) | Software Segment |

| --- | --- | --- | --- | --- |

| CurrentOffset_HwDeg_M_f32 | Single Precision Float | 0 | 20 | RETURN_START_SEC_VAR_CLEARED_32 |

| CrntHandWheelAthScl_Uls_M_f32 | Single Precision Float | 0 | 1 | RETURN_START_SEC_VAR_CLEARED_32 |

| HwPosReturnCmd _MtrNm_D_f32 | Single Precision Float | 0 | 0.5 | RETURN_START_SEC_VAR_CLEARED_32 |

| HwTrqReturnScl_Uls _D_f32 | Single Precision Float | 0 | 1 | RETURN_START_SEC_VAR_CLEARED_32 |

| HwVelReturnScl_Uls _D_f32 | Single Precision Float | 0 | 50 | RETURN_START_SEC_VAR_CLEARED_32 |

| TempReturnScl_Uls_D_f32 | Single Precision Float | 0 | 10 | RETURN_START_SEC_VAR_CLEARED_32 |

| AbsHwPosReturn_HwDeg_D_u12p4 | 0.0625 | 0 | 1640 | RETURN_START_SEC_VAR_CLEARED_16 |

| SgnHwPosReturn_HwDeg_D_f32 | Single Precision Float | -1 | 1 | RETURN_START_SEC_VAR_CLEARED_32 |

| RtrnBasicReturn_MtrNm_D_f32 | SinglePrecisionFloating point | -10 | 10 | RETURN_START_SEC_VAR_CLEARED_32 |

| Variable Name | Typedef Name | Storage Type | Safety Critical Classification |

| --- | --- | --- | --- |

| None |  |  |  |

| Constant Name |

| --- |

| t_ReturnVSpdTblBS_Kph_u9p7 |

| t2_ReturnPosTblXM_HwDeg_u12p4 |

| t2_ReturnPosTblYM_MtrNm_u5p11 |

| t2_ReturnSclTrqTblXM_HwNm_T_u8p8 |

| t2_ReturnSclTrqTblYM_Uls_u8p8 |

| t2_ReturnSclVelTblXM_HwRadpS_T_u7p9 |

| t2_ReturnSclVelTblYM_Uls_u8p8 |

| k_RtnOffsetSlew_HwDegpS_f32 |

| k_RtnOffsetRange_HWDeg_f32 |

| t_ReturnTempScaleXTbl_DegC_s11p4 |

| t_ReturnTempScaleSclYTbl_Uls_u8p8 |

| t_HWAuthRetScl_X_Uls_u8p8 |

| t_HWAuth RetScl_Y_Uls_u9p7 |

| k_RtnHWAuthSlew_UlspS_f32 |

| k_RtnLimit_MtrNm_f32 |

| Constant Name | Resolution | Value |

| --- | --- | --- |

|  |  |  |

|  |  |  |

| Constant Name |

| --- |

| BC_RETURN_FAULTINJECTIONPOINT |

| STD_ON |

| FLTINJ_RETURN |

| D_2MS_SEC_F32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

|  |  |  |  |

| Function Name | Task List | Calling Frequency | in which the function is called |

| --- | --- | --- | --- |

| _L5_Per() |  | 2ms | All |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| _L5_Per() | RTE_AP_RETURN_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial release | 16MAY11 | SAH |

| 2 | 2 | Apply scale factors from driving-dynamics and parking-assist. Replace computed handwheel velocity with global input. | 01-Jun-11 | YY |

| 3 | 3 | Updated for FDD #SF-02 | 17_Nov_11 | M. Story |

| 4 | 4 | Fixed Macro Names | 29 Nov11 | M. Story |

| 5 | 5 | Version 5 did not get checked in properly – so changes were lost and are in version 6 | 03Dec2011 | SMW |

| 6 | 6 | Updated calibration sign for temperature (need to be signed) and also update global input reads to match latest component template | 05Dec11 | SMW |

| 8 | 8 | Updated Globals based on UTP issue | 07Dec11 | M. Story |

| 9 | 9 | Corrected display variable assignments | 21Dec11 | M. Story |

| 10 | 10 | Changed ReturnRange to float32 from Uint16 | 04PR12 | M. Story |

| 11 | 11 | Added FLTINJ and some updates as per SF02 Ver004 | 10May12 | NRAR |

| 12 | 12 | Anom 3317 fix for RateLimiter scaling issue | 16 May 12 | NRAR |

| 13 | 13 | Move EOLRtnRange_MtrNm_f32 from EEPROM to flash, adding k_RtnLimit_MtrNm_f32CR5873 | 20July12 | BDO |

| 14 | 14 | Added checkpoints and memmap software segment is updated for static variables | 23-Sep-2012 | Selva |

| 15 | 15 | Corrected anomaly 4893 | 27-Apr-13 | KJS |

|  |  |  |  |  |
