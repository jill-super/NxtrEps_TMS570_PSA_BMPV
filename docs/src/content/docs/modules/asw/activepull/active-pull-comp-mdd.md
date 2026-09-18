---
title: 'Active Pull Comp MDD'
description: 'Converted design document: Active Pull Comp MDD'
---

> **Source:** `ActivePull/doc/Active_Pull_Comp_MDD.docx`  
> **Module:** [ActivePull](../../../../asw/activepull/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module -- Active Pull Compensation

## High-Level Description

This module corrects for vehicle pull issues by compensation for both long and short term torque offsets.

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

The filter constants were derived from the requirements in SF-09 in conjunction with the following filter analyses.  Note that the upper frequency limits defined in the requirements for some values were not achievable.  The data dictionary reflects the limits of both the requirements and the software limitations.

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

FPM_FloatToFixed_m

FPM_FixedToFloat_m

LPF_SvUpdate_s16InFixKTrunc_m

Abs_f32_m

Min_m

Max_m

Sign_f32_m

Limit_m

IntplVarXY_u16_u16Xu16Y_Cnt

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

#### Init: ActivePull_Init1

##### Design Rationale

This initialization function is used to set values that are based solely on calibrations and constants (values which will not change over the course of an ignition cycle).  This includes preliminary gain calculations, limits, and step sizes.  It also initializes the LTComp_HwNm_M_f32 module-internal variable with the appropriate value from NvM.

##### Module Internal

LTWindUpLimit_HwNm_M_f32 = Min_m(k_TotalLimit_HwNm_f32, k_LTLimit_HwNm_f32)

STStepSize_HwNm_M_f32 = (D_STSAMPLETIME_SEC_F32 * k_STLimit_HwNm_f32) / k_STRampTime_Sec_f32

PullCompStepSize_HwNm_M_f32 = k_OutputMaxRate_HwNmpS_f32 * D_PULLCOMPSAMPLETIME_SEC_F32

### Periodic Functions

#### Per: ActivePull_Per1

##### Design Rationale

The requirements in SF-13 show a signal called Reset_Svc.  This is shown as an input flag to the function.  However, the reset service has been implemented as a service call.  In order to avoid any thread-based issues, the service sets a separate variable for each periodic (ResetPer1_Cnt_M_lgc, in this case) to TRUE.  Then, near the beginning of the execution of the periodic, this value is read.  If it has been set to true, it is immediately set to FALSE, and a local copy (ResetSvc_Cnt_T_lgc) is set to TRUE.  In this way, each periodic uses its own local copy just as the design dictates using the input signal.  The local copy will be set to true for one execution of each periodic function.

The SCom function to set the STComp is done in a similar fashion.  The Scom function sets SComSTCompSet_Cnt_M_lgc to TRUE and when ActivePull_Per1 finds this value set to TRUE, it sets it back to FALSE and uses SComSTComp_HwNm_M_f32 as the state variable (instead of STComp_HwNm_M_f32, as it normally would).  The state variable itself is never changed, but the output of the next execution of ActivePull_Per1 will reflect the new value.

##### Program Flow Start

Rte_Call_ActivePull_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

DisableLearning_Cnt_T_lgc = Rte_Iread_ActivePull_Per1_DisableLearning_Cnt_lgc()

DisableOutput_Cnt_T_lgc = Rte_Iread_ActivePull_Per1_DisableOutput_Cnt_lgc()

HandwheelAuthority_Uls_T_f32 = Rte_Iread_ActivePull_Per1_HandwheelAuthority_Uls_f32()

HandwheelPosition_HwDeg_T_f32 = Rte_Iread_ActivePull_Per1_HandwheelPosition_HwDeg_f32()

HandwheelVelocity_HwRadpS_T_f32 = Rte_Iread_ActivePull_Per1_HandwheelVelocity_HwRadpS_f32()

HwTorque_HwNm_T_f32 = Rte_Iread_ActivePull_Per1_HwTorque_HwNm_f32()

SrlComYawRate_DegpS_T_f32 = Rte_Iread_ActivePull_Per1_SrlComYawRate_DegpS_f32()

VehicleSpeedValid_Cnt_T_lgc = Rte_Iread_ActivePull_Per1_VehicleSpeedValid_Cnt_lgc()

VehicleSpeed_Kph_T_f32 = Rte_Iread_ActivePull_Per1_VehicleSpeed_Kph_f32()

LTComp_HwNm_T_f32 = LTComp_HwNm_M_f32

PrevSTComp_HwNm_T_f32 = STComp_HwNm_M_f32

##### Check for Scom Functions

##### Filter Inputs

##### Active Compensation Enable

##### Determine Enable Learning

##### Short Term Compensation Filter

##### Calculate Integrator Gains

##### Error Integrator & Active Limit

##### Store Local copy of outputs into Module Outputs

HwTrqFilt_HwNm_D_f32 = HwTrqFilt_HwNm_T_f32

YawRateFilt_DegpS_D_f32 = YawRateFilt_DegpS_T_f32

STError_HwNm_D_f32 = STError_HwNm_T_f32

STIntGain_Uls_D_f32 = STIntGain_Uls_T_f32

STReset_Cnt_D_lgc = STReset_Cnt_T_lgc

STComp_HwNm_M_f32 = STComp_HwNm_T_f32

EnableLearn_Cnt_M_lgc = EnableLearning_Cnt_T_lgc

##### Program Flow End

Rte_Call_ActivePull_Per1_CP1_CheckpointReached()

#### Per: ActivePull_Per2

##### Design Rationale

The Reset_Svc functionality is defined in section 6.3.1.1.

##### Program Flow Start

##### Rte_Call_ActivePull_Per2_CP0_CheckpointReached()Store Module Inputs to Local copies

VehicleSpeed_Kph_T_f32 = Rte_Iread_ActivePull_Per2_VehicleSpeed_Kph_f32()

DisableOutput_Cnt_T_lgc = Rte_Iread_ActivePull_Per2_DisableOutput_Cnt_lgc()

PrevPullCompCmd_HwNm_T_f32 = PullCompCmd_HwNm_M_f32

STComp_HwNm_T_f32 = STComp_HwNm_M_f32

LTComp_HwNm_T_f32 = LTComp_HwNm_M_f32

##### Check for Reset

##### Calculate Active Compensation

##### Store Local copy of outputs into Module Outputs

PullCompCmd_HwNm_M_f32 = PullCompCmd_HwNm_T_f32

Rte_Iwrite_ActivePull_Per2_PullCompCmd_MtrNm_f32(PullCompCmd_MtrNm_T_f32)

##### Program Flow End

#### Rte_Call_ActivePull_Per2_CP1_CheckpointReached()Per: ActivePull_Per3

##### Design Rationale

The Reset_Svc and state variable functionality are defined in section 6.3.1.1.  Note that the Scom functions will have no effect until the next execution of ActivePull_Per3, which could result in a propagation delay of up to 100 ms.

##### Program Flow Start

##### Rte_Call_ActivePull_Per3_CP0_CheckpointReached()Store Module Inputs to Local copies

VehSpd_Kph_T_f32 = Rte_IRead_ActivePull_Per3_VehicleSpeed_Kph_f32()

HwTorque_HwNm_T_f32 = Rte_Iread_ActivePull_Per3_HwTorque_HwNm_f32()

EnableLearning_Cnt_T_lgc = EnableLearn_Cnt_M_lgc

STComp_HwNm_T_f32 = STComp_HwNm_M_f32

PrevLTComp_HwNm_T_f32 = LTComp_HwNm_M_f32

##### Check for Scom Functions

##### Long Term Compensation Filter

##### Error Integrator

##### Store Local copy of outputs into Module Outputs

LTError_HwNm_D_f32 = LTError_HwNm_T_f32

LTComp_HwNm_M_f32 = LTComp_HwNm_T_f32

##### Program Flow End

Rte_Call_ActivePull_Per3_CP1_CheckpointReached()

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

#### Scom: ActivePull_Scom_Reset

##### Design Rationale

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

##### Reset Service

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

N/A

#### Scom: ActivePull_Scom_SetLTComp

##### Design Rationale

This function helps to fulfill the requirement that the “Engineering interface tool shall provide ability to set state variable to desired value”.  The state variable itself will not be updated until the next time ActivePull_Per3 is run, but the NvM value is updated immediately.

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

None

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

N/A

#### Scom: ActivePull_Scom_SetSTComp

##### Design Rationale

This function helps to fulfill the requirement that the “Engineering interface tool shall provide ability to set state variable to desired value”.  The state variable itself will not be updated until the next time ActivePull_Per1 is run.

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

None

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

N/A

#### Scom: ActivePull_Scom_ReadParam

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

None

##### Read Data

*PullCompCmd_HwNm_f32 = PullCompCmd_HwNm_M_f32

*STComp_HwNm_f32 = STComp_HwNm_M_f32

*LTComp_HwNm_f32 = LTComp_HwNm_M_f32

*EnableLearn_Cnt_lgc = EnableLearn_Cnt_M_lgc

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

N/A

### Transition Functions

#### Trns: ActivePull_Trns1

##### Design Rationale

This function is run when entering the OPERATE state.  The LTComp NvM block is set to write on shutdown (as ActivePull_Per3 will be updating the NvM block), and the timers associated with ActivePull_Per1 are initialized.

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

None

##### Initialization

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

N/A

## Execution Requirements

### Execution Sequence of the Module

ActivePull_Per1 and Per2 are run at 2ms intervals, while Per3 is run at a 100ms interval.  However, while Per2 is run in all operation states, Per1 and Per3 are only run in the OPERATE state.  ActivePull_Trns1 is run upon entering the OPERATE state.

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

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| HwTorque_HwNm_f32 | HwTorque_HwNm_f32 | PullCompCmd_MtrNm_f32 |

| HandwheelPosition_HwDeg_f32 | HandwheelPosition_HwDeg_f32 |  |

| HandwheelAuthority_Uls_f32 | HandwheelAuthority_Uls_f32 |  |

| VehicleSpeed_Kph_f32 | VehicleSpeed_Kph_f32 |  |

| VehicleSpeedValid_Cnt_lgc | VehicleSpeedValid_Cnt_lgc |  |

| HandwheelVelocity_HwRadpS_f32 | HandwheelVelocity_HwRadpS_f32 |  |

| SrlComYawRate_DegpS_f32 | SrlComYawRate_DegpS_f32 |  |

| DisableLearning_Cnt_lgc | DisableLearning_Cnt_lgc |  |

| DisableOutput_Cnt_lgc | DisableOutput_Cnt_lgc |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| DecGain_Uls_M_f32 | Single Precision Float | 0.0000135 | 0.00054 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| IncGain_Uls_M_f32 | Single Precision Float | 0.0000135 | 0.00054 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| LTIntGain_Uls_M_f32 | Single Precision Float | 0.00001875 | 0.00045 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| LTWindUpLimit_HwNm_M_f32 | Single Precision Float | 0 | 4 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| STStepSize_HwNm_M_f32 | Single Precision Float | 0 | 20000 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| PullCompStepSize_HwNm_M_f32 | Single Precision Float | 0 | 0.2 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| ResetPer1_Cnt_M_lgc | n/a | FALSE | TRUE | ACTIVEPULL_START_SEC_VAR_CLEARED_BOOLEAN |

| ResetPer2_Cnt_M_lgc | n/a | FALSE | TRUE | ACTIVEPULL_START_SEC_VAR_CLEARED_BOOLEAN |

| ResetPer3_Cnt_M_lgc | n/a | FALSE | TRUE | ACTIVEPULL_START_SEC_VAR_CLEARED_BOOLEAN |

| HwTorqueSV_HwNm_M_Str | LPF32KSV_Str | N/A | N/A | ACTIVEPULL_START_SEC_VAR_CLEARED_UNSPECIFIED |

| HwTorqueSV_HwNm_M_Str.K_Uls_f32 | Float32 | 0.001255848 | 0.715390457 |  |

| HwTorqueSV_HwNm_M_Str.SV_Uls_f32 | Float32 | -10 | 10 |  |

| SrlComYawRateSV_DegpS_M_Str | LPF32KSV_Str | N/A | N/A | ACTIVEPULL_START_SEC_VAR_CLEARED_UNSPECIFIED |

| SrlComYawRateSV_DegpS_M_Str.K_Uls_f32 | Float32 | 0.001255848 | 0.715390457 |  |

| SrlComYawRateSV_DegpS_M_Str.SV_Uls_f32 | Float32 | -128 | 127.9375 |  |

| EnableTime_mS_M_u32 | 1 | 0 | 4294967295 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| EnableLearn_Cnt_M_lgc | n/a | FALSE | TRUE | ACTIVEPULL_START_SEC_VAR_CLEARED_BOOLEAN |

| HwTorqueSTSV_HwNm_M_Str | LPF32KSV_Str | N/A | N/A | ACTIVEPULL_START_SEC_VAR_CLEARED_UNSPECIFIED |

| HwTorqueSTSV_HwNm_M_Str.K_Uls_f32 | Float32 | 0.001255848 | 0.715390457 |  |

| HwTorqueSTSV_HwNm_M_Str.SV_Uls_f32 | Float32 | -10 | 10 |  |

| STComp_HwNm_M_f32 | Single Precision Float | -4 | 4 |  |

| STOppSignTime_mS_M_u32 | 1 | 0 | 4294967295 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| PullCompCmd_HwNm_M_f32 | Single Precision Float | -8.8 | 8.8 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| LTComp_HwNm_M_f32 | Single Precision Float | -4 | 4 | ACTIVEPULL_START_SEC_VAR_SAVED_ZONEH_32 |

| HwTorqueLTSV_HwNm_M_Str | LPF32KSV_Str | N/A | N/A | ACTIVEPULL_START_SEC_VAR_CLEARED_UNSPECIFIED |

| HwTorqueLTSV_HwNm_M_Str.K_Uls_f32 | Float32 | 0.006263487 | 1 |  |

| HwTorqueLTSV_HwNm_M_Str.SV_Uls_f32 | Float32 | -14 | 14 |  |

| SComLTComp_HwNm_M_f32 | Single Precision Float | -4 | 4 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| SComLTCompSet_Cnt_M_lgc | n/a | FALSE | TRUE | ACTIVEPULL_START_SEC_VAR_CLEARED_BOOLEAN |

| SComSTComp_HwNm_M_f32 | Single Precision Float | -4 | 4 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| SComSTCompSet_Cnt_M_lgc | n/a | FALSE | TRUE | ACTIVEPULL_START_SEC_VAR_CLEARED_BOOLEAN |

| PrevLTLearnTime_Min_M_u16 | 1 | 0 | 120 | ACTIVEPULL_START_SEC_VAR_CLEARED_16 |

| PrevSTLearnTimeInc_Sec_M_u12p4 | 0.0625 | 0 | 200 | ACTIVEPULL_START_SEC_VAR_CLEARED_16 |

| PrevSTLearnTimeDec_Sec_M_u12p4 | 0.0625 | 0 | 200 | ACTIVEPULL_START_SEC_VAR_CLEARED_16 |

| HwTrqFilt_HwNm_D_f32 | Single Precision Float | -10 | 10 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| YawRateFilt_DegpS_D_f32 | Single Precision Float | -128 | 127.9375 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| STError_HwNm_D_f32 | Single Precision Float | -10 | 10 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| STIntGain_Uls_D_f32 | Single Precision Float | 0.0000135 | 0.00054 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| STReset_Cnt_D_lgc | n/a | FALSE | TRUE | ACTIVEPULL_START_SEC_VAR_CLEARED_BOOLEAN |

| LTError_HwNm_D_f32 | Single Precision Float | -14 | 14 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| PrevVehSpd_Kph_M_f32 | Single Precision Float | 0 | 511 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| VehSpdRate_KphpS_M_f32 | Single Precision Float | -5110 | 5110 | ACTIVEPULL_START_SEC_VAR_CLEARED_32 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Constant Name |

| --- |

| k_YawRateFilt_Hz_f32 |

| k_HwTrqFilt_Hz_f32 |

| k_STResetHwTrq_HwNm_f32 |

| k_STResetHwPos_HwDeg_f32 |

| k_STResetYawRate_DegpS_f32 |

| k_EnableHwTrqMax_HwNm_f32 |

| k_EnableHwPosMax_HwDeg_f32 |

| k_EnableHwAuthMin_Uls_f32 |

| k_EnableHwVelMax_DegpS_f32 |

| k_EnableVehSpdRateMax_KphpS_f32 |

| k_EnableVehSpdMin_Kph_f32 |

| k_EnableVehSpdMax_Kph_f32 |

| k_EnableYawRateMax_DegpS_f32 |

| k_EnableTime_mS_u32 |

| k_STLimit_HwNm_f32 |

| k_STLearnTimeInc_Sec_f32 |

| k_STLearnTimeDec_Sec_f32 |

| k_STOppSignTime_mS_u32 |

| k_STRampTime_Sec_f32 |

| k_STIntInputLimit_HwNm_f32 |

| k_STFilt_Hz_f32 |

| k_FiltDeadband_HwNm_f32 |

| k_LTLimit_HwNm_f32 |

| k_LTLearnTime_Min_f32 |

| k_LTFilt_Hz_f32 |

| k_LTIntInputLimit_HwNm_f32 |

| k_TotalLimit_HwNm_f32 |

| k_HwNmToMtrNm_Uls_f32 |

| t_VehSpdScaleTblX_Kph_u9p7[4] |

| t_VehSpdScaleTblY_Uls_u2p14[4] |

| k_OutputMaxRate_HwNmpS_f32 |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_MINTOSEC_SECPMIN_F32 | Single Precision Float | SecPerMin | 60 |

| D_STINTSCALER_ULS_F32 | Single Precision Float | Unitless | 1.35 |

| D_STSAMPLETIME_SEC_F32 | Single Precision Float | Seconds | 0.002 |

| D_LTINTSCALER_ULS_F32 | Single Precision Float | Unitless | 1.35 |

| D_LTSAMPLETIME_SEC_F32 | Single Precision Float | Seconds | 0.1 |

| D_PULLCOMPSAMPLETIME_SEC_F32 | Single Precision Float | Seconds | 0.002 |

| Constant Name |

| --- |

| D_FALSE_CNT_LGC |

| D_180OVRPI_ULS_F32 |

| D_2MS_SEC_F32 |

| D_ZERO_ULS_F32 |

| D_MTRTRQCMDLOLMT_MTRNM_F32 |

| D_MTRTRQCMDHILMT_MTRNM_F32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Data | Value |

| --- | --- |

| Rte_InitValue_DisableLearning_Cnt_lgc | FALSE |

| Rte_InitValue_DisableOutput_Cnt_lgc | FALSE |

| Rte_InitValue_HandwheelAuthority_Uls_f32 | 0 |

| Rte_InitValue_HandwheelPosition_HwDeg_f32 | 0 |

| Rte_InitValue_HandwheelVelocity_HwRadpS_f32 | 0 |

| Rte_InitValue_HwTorque_HwNm_f32 | 0 |

| Rte_InitValue_PullCompCmd_MtrNm_f32 | 0 |

| Rte_InitValue_SrlComYawRate_DegpS_f32 | 0 |

| Rte_InitValue_VehicleSpeed_Kph_f32 | 0 |

| Rte_InitValue_VehicleSpeedRate_KphpS_f32 | 0 |

| Rte_InitValue_VehicleSpeedValid_Cnt_lgc | FALSE |

|  |  | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

| Return Value | None |  |  |  |  |

|  |  | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | LTComp_HwNm_f32 | float32 | -10 | 10 |  |

| Return Value | None |  |  |  |  |

|  |  | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | STComp_HwNm_f32 | float32 | -10 | 10 |  |

| Return Value | None |  |  |  |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| ActivePull_Init1 | On Event (once) | On Entering WARMINIT |

| ActivePull_Per1 | 2 ms | OPERATE |

| ActivePull_Per2 | 2 ms | All |

| ActivePull_Per3 | 100 ms | OPERATE |

| ActivePull_Trns1 | On Event | On Entering OPERATE |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| ActivePull_Scom_Reset |  |

| ActivePull_Scom_SetLTComp |  |

| ActivePull_Scom_SetSTComp |  |

| ActivePull_Scom_ReadParam |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| ActivePull_Init1 | RTE_START_SEC_AP_ACTIVEPULL_APPL_CODE |

| ActivePull_Per1 | RTE_START_SEC_AP_ACTIVEPULL_APPL_CODE |

| ActivePull_Per2 | RTE_START_SEC_AP_ACTIVEPULL_APPL_CODE |

| ActivePull_Per3 | RTE_START_SEC_AP_ACTIVEPULL_APPL_CODE |

| ActivePull_Trns1 | RTE_START_SEC_AP_ACTIVEPULL_APPL_CODE |

| ActivePull_Scom_Reset | RTE_START_SEC_AP_ACTIVEPULL_APPL_CODE |

| ActivePull_Scom_SetLTComp | RTE_START_SEC_AP_ACTIVEPULL_APPL_CODE |

| ActivePull_Scom_SetSTComp | RTE_START_SEC_AP_ACTIVEPULL_APPL_CODE |

| ActivePull_Scom_ReadParam | RTE_START_SEC_AP_ACTIVEPULL_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial MDD | 01Aug11 | LWW |

| 2 | 2.0 | Updated to SF-13 rev 001 (started from scratch) | 02-Apr-12 | OT |

| 3 | 3.0 | Fixed buffered reads in Reset Scom function (changed to direct reads) | 18-Apr-12 | OT |

| 4 | 4.0 | Removed PIM from Scom and made LT learned variable to a typH. Added support for FDAD Common manufacturing srvc DID | 22-Apr-12 | VK |

| 5 | 5.0 | Updates to meet SF-13 rev 002 | 26-June-12 | VK |

| 6 | 6.0 | Corrected module internal variable ranges | 29-June-12 | VK |

| 7 | 7.0 | 1) Removed VehSpdRate global input and made necessary changes in Per1<br/>2) Added VehicleSpeedRate logic in Per3 -Ver 003 updates<br/>3) Changed LPF from fixed to float | 23-July-12 | NRAR |

| 8 | 8.0 | Inserted safe watchdog checkpoints | 15-Sept-12 | BWL |

| 9 | 9.0 | Corrected  static variable to MDD format | 18-sep-12 | SSK |

| 10 | 10.0 | Updated calibration table Y datatype to u2p14 for anomaly correction, removed condition checks on SCom function | 20 Oct 12 | LWW |

| 11 | 11.0 | Anomaly 5379 fixed. | 07-Aug-13 | SP |

|  |  |  |  |  |
