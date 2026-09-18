---
title: 'StabilityCompensation MDD'
description: 'Converted design document: StabilityCompensation MDD'
---

> **Source:** `StabilityComp/doc/StabilityCompensation_MDD.docx`  
> **Module:** [StabilityComp](../../../../asw/stabilitycomp/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module -- Stability Compensation

## High-Level Description

This function provides in-vehicle stability of EPS behavior. To maximize steering feel, the function blends between two different tunings based on vehicle speed and low frequency handwheel torque. Because system gains may get multiplied by various scale factors, either from serial communications or from other software functions, this function provides a second blending feature.

Some vehicle programs require a secondary, or "systematic", calculation of stability compensation followed by a correlation check. The systematic calculations usually must reside in a separate Memory Partition Unit (MPU), and switching between MPUs negatively impacts system throughput. This model is designed using the best-known implementation at this time.

## Figures

### Component Diagram

### Variable Data Dictionary

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

### Module Internal Variables

This section identifies the name, range and resolutions for module specific data created by this module.  If there are no range restrictions on the variable, the term “FULL” is placed into the table for legal range.

* See unit testing notes in section 2.3.1 for range considerations of Notch Filter

#### Notch filter Unit testing considerations

Since the notch filter implementation used in this module is dynamic in nature, absolute ranges are difficult to determine without pre-defined knowledge on the combination of coefficient values (A1, A2, B0, B1, B2).  Because of this, the systems group ran simulations on 10 different combinations of coefficients (2 with defined default calibrations, 8 considered extreme cases of notch filters) and logged the ranges of the filter state variables and outputs during a frequency sweep.  The ranges given throughout this module were taken as the worst case results of all of the given test cases.

To provide useful cases for unit testing, the boundary checks tested during unit testing should be altered to test the state variable minimum and maximum for each of the 10 test cases with the given coefficients set to the values given in that test case.  In the case where the default values of the coefficients are used in a vector, the unit tester should not test the corresponding state variables with values over the range defined for that set of coefficients.  See attached simulation results.

#### User defined typedef definition/declaration

This section documents any user types uniquely used for the module.

## Constant Data Dictionary

### Calibration Constants

This section lists the calibrations used by the module.  For details on calibration constants, refer to the Data Dictionary for the application.

### Program (fixed) Constants

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

FPM_FloatToFixed_m

Limit_m

NF_Init_f32

FPM_FixedToFloat_m

BilinearXYM_u16_u16Xu16YM_Cnt

IntplVarXY_u16_u16Xu16Y_Cnt

Blend_f32

Abs_f32_m

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

None

### Local Functions/Macros Used by this MDD only

#### ApplyStabilityComp

##### * See unit testing notes in section 2.3.1 for range considerations of Notch Filter

##### Description

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init: StabilityComp_Init1

##### Design Rationale

None

### Periodic Functions

#### Per: StabilityComp_Per1

##### Design Rationale

##### Program Flow Start

Rte_Call_StabilityComp_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

N/A

##### Store Local copy of outputs into Module Outputs

##### Rte_IWrite_StabilityComp_Per1_AssistCmd_MtrNm_f32(AssistCmd_MtrNm_T_f32)Program Flow End

Rte_Call_StabilityComp_Per1_CP1_CheckpointReached()

### Fault Recovery Functions

### Shutdown Functions

### Interrupt Functions

### Serial Communication Functions

## Execution Requirements

### Execution Sequence of the Module

(Describe in words relevant details about the execution sequence of the different sub modules.)

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

INLINE functions defined in GlobalMacro.h are not unit tested

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| AssistDDFactor_Uls_f32 | AssistDDFactor_Uls_f32 | AssistCmd_MtrNm_f32 |

| SysAssistCmd_MtrNm_f32 | SysAssistCmd_MtrNm_f32 |  |

| HwTorque_HwNm_f32 | HwTorque_HwNm_f32 |  |

| VehicleSpeed_Kph_f32 | VehicleSpeed_Kph_f32 |  |

| CombinedAssist_MtrNm_f32 | CombinedAssist_MtrNm_f32 |  |

| AsstFWActive_Uls_f32 | AsstFWActive_Uls_f32 |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| StCmpAsstFctrCmpBlnd_Uls_D_f32 | Single Precision Float | 0 | 1 | STABILITYCOMP_START_SEC_VAR_CLEARED_32 |

| StCmp12Blend_Uls_D_f32 | Single Precision Float | 0 | 1 | STABILITYCOMP_START_SEC_VAR_CLEARED_32 |

| StCmp34Blend_Uls_D_f32 | Single Precision Float | 0 | 1 | STABILITYCOMP_START_SEC_VAR_CLEARED_32 |

| StCmp02Blend_Uls_D_f32 | Single Precision Float | 0 | 1 | STABILITYCOMP_START_SEC_VAR_CLEARED_32 |

| StCmp04Blend_Uls_D_f32 | Single Precision Float | 0 | 1 | STABILITYCOMP_START_SEC_VAR_CLEARED_32 |

| StCmp1Out_MtrNm_D_f32 | Single Precision Float | -2312 | 2312 | STABILITYCOMP_START_SEC_VAR_CLEARED_32 |

| StCmp2Out_MtrNm_D_f32 | Single Precision Float | -2312 | 2312 | STABILITYCOMP_START_SEC_VAR_CLEARED_32 |

| StCmp3Out_MtrNm_D_f32 | Single Precision Float | -2312 | 2312 | STABILITYCOMP_START_SEC_VAR_CLEARED_32 |

| StCmp4Out_MtrNm_D_f32 | Single Precision Float | -2312 | 2312 | STABILITYCOMP_START_SEC_VAR_CLEARED_32 |

| AssistCmdSV_MtrNm_M_f32 | Single Precision Float | -8.8 | 8.8 | STABILITYCOMP_START_SEC_VAR_CLEARED_32 |

| HwTrqSV_HwNm_M_Str | N/A | N/A | N/A | STABILITYCOMP_START_SEC_VAR_CLEARED_UNSPECIFIED |

| HwTrqSV_HwNm_M_Str.K_Uls_f32 | Single Precision Floating Point | 0.000125 | 0.4666 |  |

| HwTrqSV_HwNm_M_Str.SV_Uls_f32 | Single Precision Floating Point | 0 | 10 |  |

| CombAstNFSV_Cnt_M_Str* | N/A | N/A | N/A | STABILITYCOMP_START_SEC_VAR_CLEARED_UNSPECIFIED |

| CombAstNFSV_Cnt_M_Str[].SV1_Uls_f32 | Single Precision Floating Point | -2077 | 2077 |  |

| CombAstNFSV_Cnt_M_Str[].SV2_Uls_f32 | Single Precision Floating Point | -1981 | 1981 |  |

| CombAstNFSV_Cnt_M_Str[].Out_Uls_f32 | Single Precision Floating Point | -2312 | 2312 |  |

| CombAstNFSV_Cnt_M_Str[].KPtr_Cnt_Str->A1_Uls_f32 | Single Precision Floating Point | -2 | 0 |  |

| CombAstNFSV_Cnt_M_Str[].KPtr_Cnt_Str->A2_Uls_f32 | Single Precision Floating Point | -1 | 1 |  |

| CombAstNFSV_Cnt_M_Str[].KPtr_Cnt_Str->B0_Uls_f32 | Single Precision Floating Point | 0 | 2300 |  |

| CombAstNFSV_Cnt_M_Str[].KPtr_Cnt_Str->B1_Uls_f32 | Single Precision Floating Point | -4500 | 0 |  |

| CombAstNFSV_Cnt_M_Str[].KPtr_Cnt_Str->B2_Uls_f32 | Single Precision Floating Point | -4 | 2300 |  |

| StabCompOverThresh_Cnt_D_lgc | Boolean | 0 | 1 | STABILITYCOMP_START_SEC_VAR_CLEARED_BOOLEAN |

| StCmpPNStatus_Cnt_M_lgc | Boolean | 0 | 1 | STABILITYCOMP_START_SEC_VAR_CLEARED_BOOLEAN |

| StCmpPNAccum_Cnt_M_u16 | uint16 | 0 | 5000 | STABILITYCOMP_START_SEC_VAR_CLEARED_16 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Constant Name |

| --- |

| t_StCmpADDFBlendX_Uls_u2p14[ ] |

| t_StCmpADDFBlendY_Uls_u2p14[ ] |

| t_StCmpBlendSpdBS_Kph_u9p7[ ] |

| t_StCmpBlend12Trq_HwNm_u8p8[ ] |

| t2_StCmpBlend12TblY_Uls_u2p14[ ][ ] |

| t2_StCmpBlend02TblY_Uls_u2p14[ ][ ] |

| t_StCmpBlend34Trq_HwNm_u8p8[ ] |

| t2_StCmpBlend34TblY_Uls_u2p14[ ][ ] |

| t2_StCmpBlend04TblY_Uls_u2p14[ ][ ] |

| t_StCmpNFK_Str[ ] |

| t_StCmpNFK_Str[ ].A1_Uls_f32 |

| t_StCmpNFK_Str[ ].A2_Uls_f32 |

| t_StCmpNFK_Str[ ].B0_Uls_f32 |

| t_StCmpNFK_Str[ ].B1_Uls_f32 |

| t_StCmpNFK_Str[ ].B2_Uls_f32 |

| k_StCmpHwTrqLPFKn_Hz_f32 |

| k_StCmpSysCorrThresh_MtrNm_f32 |

| k_StCmpCrosChkEnbl_Uls_lgc |

| k_StCmpStabCmpPstep_Cnt_u16 |

| k_StCmpStabCmpNstep_Cnt_u16 |

| k_StCmpStabCmpPNThresh_Cnt_u16 |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_COMPINLIMIT_MTRNM_F32 | Single Precision Floating Point | MtrNm | 10.275 |

| D_NUMNOTCHFILT_CNT_U08 | UINT08 | Cnt | (TableSize_m(t_StCmpNFK_Str)) |

| D_NUMNFBLENDS_CNT_U08 | UINT08 | Cnt | 4 |

| D_ASSISTINIT_MTRNM_F32 | Single Precision Floating Point | MtrNm | 0 |

| D_COMPBLND12IDX_CNT_U08 | UINT08 | Cnt | 0 |

| D_COMPBLND34IDX_CNT_U08 | UINT08 | Cnt | 1 |

| D_COMPBLND02IDX_CNT_U08 | UINT08 | Cnt | 2 |

| D_COMPBLND04IDX_CNT_U08 | UINT08 | Cnt | 3 |

| D_ASSTSCLMT_MTRNM_F32 | Single Precision Floating Point | MtrNm | 8.8 |

| Constant Name |

| --- |

| D_ZERO_ULS_F32 |

| D_2MS_SEC_F32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | ApplyStabilityComp | ApplyStabilityComp | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- | --- |

| Arguments Passed | CombinedAssist_MtrNm_T_f32 | CombinedAssist_MtrNm_T_f32 | float32 | -10.275 | 10.275 |  |

|  | FiltSVPtr_Uls_T_Str* | FiltSVPtr_Uls_T_Str* | Pointer to NotchFiltSV_Str |  |  |  |

|  |  | .SV1_Uls_f32 | float32 | -2077 | 2077 | 0.000489 |

|  |  | .SV2_Uls_f32 | float32 | -1981 | 1981 | 0.000489 |

|  |  | .Out_Uls_f32 | float32 | -2312 | 2312 | 0.000489 |

|  |  | .KPtr_Cnt_Str->A1_Uls_f32 | float32 | -2 | 0 | 0.00005 |

|  |  | .KPtr_Cnt_Str->A2_Uls_f32 | float32 | -1 | 1 | 0.00005 |

|  |  | .KPtr_Cnt_Str->B0_Uls_f32 | float32 | 0 | 2300 | 0.00005 |

|  |  | .KPtr_Cnt_Str->B1_Uls_f32 | float32 | -4500 | 0 | 0.00005 |

|  |  | .KPtr_Cnt_Str->B2_Uls_f32 | float32 | -4 | 2300 | 0.00005 |

|  | CompBlnd_Uls_T_f32 | CompBlnd_Uls_T_f32 | Pointer to float32 | 0 | 1 |  |

|  | ADDFBlend_Uls_T_f32 | ADDFBlend_Uls_T_f32 | float32 | 0 | 2 |  |

|  | WriteDisplayVars_Cnt_T_lgc | WriteDisplayVars_Cnt_T_lgc | boolean | FALSE | TRUE |  |

| Return Value | FilteredOutput_MtrNm_T_f32 | FilteredOutput_MtrNm_T_f32 | float32 | -8.8 | 8.8 | 4.89E-04 |

| Data | Value |

| --- | --- |

| AssistDDFactor_Uls_f32 | 1 |

| HwTorque_HwNm_f32 | 0 |

| CombinedAssist_MtrNm_f32 | 0 |

| AsstFWActive_Uls_f32 | 0 |

| VehicleSpeed_Kph_f32 | 0 |

| AssistCmd_MtrNm_f32 | 0 |

| SysAssistCmd_MtrNm_T_f32 | 0 |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| StabilityComp_Per1 | 2ms | ALL STATES |

| StabilityComp_Init1 | STARTUP | COLD INIT |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| <None> |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| StabilityComp_Per1 |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| ApplyStabilityComp |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial MDD | 30NOV11 | VK |

| 2 | 2.0 | Anomaly 2852 Added limits to assist and baseassist outputs | 02Feb12 | M. Story |

| 3 | 3 | Updated to SF-29 rev 3 | 02-May-12 | OT |

| 4 | 4 | Added checkpoints and memmap software segment is updated for static variables | 24-Sep-12 | Selva |

| 5 | 5 | Updated to SF-29 rev 5<br/>Addition of LPF of handwheel torque to the compensator blend tables.<br/>Added functionality to allow compensators 2 and 4 to blend to zero | 15Oct12 | LN |

| 6 | 6 | Corrected Macro size of D_NUMNFBLENDS_CNT_U08 to 4 | 11Feb13 | Selva |

| 7 | 7 | Updated to SF-29 rev 006 | 27 Feb 13 | SP |

| 8 | 8 | Anom 4609- Fixed correct function call for FaultInjection call | 02 April 13 | NRAR |

| 9 | 9 | Anomaly 4791 fix | 11 Apr 13 | SP |

| 10 | 10 | Updated to SF-29 rev 007 | 13 Apr 13 | SP |

| 11 | 11 | Range updates and notes about unit testing the notch filter.  Corrected NTC name. | 30 Apr 13 | LWW |

| 12 | 12 | Range updates on HwTrq filter SV.  Added tolerance for pointer values on local function. | 06 June 13 | LWW |

|  |  |  |  |  |
