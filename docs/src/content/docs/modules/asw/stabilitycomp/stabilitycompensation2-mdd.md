---
title: 'StabilityCompensation2 MDD'
description: 'Converted design document: StabilityCompensation2 MDD'
---

> **Source:** `StabilityComp/doc/StabilityCompensation2_MDD.docx`  
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

#### ApplyStabilityComp2

##### * See unit testing notes in section 2.3.1 for range considerations of Notch Filter

##### Description

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init: StabilityComp2_Init1

##### Design Rationale

None

### Periodic Functions

#### Per: StabilityComp_Per1

##### Design Rationale

##### Program Flow Start

Rte_Call_StabilityComp2_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

AssistDDFactor_Uls_T_f32 = Rte_IRead_StabilityComp2_Per1_AssistDDFactor_Uls_f32();

AsstFWActive_Uls_T_f32 = Rte_IRead_StabilityComp2_Per1_AsstFWActive_Uls_f32();

CombinedAssist_MtrNm_T_f32 = Rte_IRead_StabilityComp2_Per1_CombinedAssist_MtrNm_f32();

HwTorque_HwNm_T_f32 = Rte_IRead_StabilityComp2_Per1_HwTorque_HwNm_f32();

VehicleSpeed_Kph_T_f32 = Rte_IRead_StabilityComp2_Per1_VehicleSpeed_Kph_f32();

##### Store Local copy of outputs into Module Outputs

Rte_IWrite_StabilityComp2_Per1_SysAssistCmd_MtrNm_f32(SysAssistCmd_MtrNm_T_f32);

##### Program Flow End

Rte_Call_StabilityComp2_Per1_CP1_CheckpointReached()

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

| AssistDDFactor_Uls_f32 | AssistDDFactor_Uls_f32 | SysAssistCmd_MtrNm_f32 |

| HwTorque_HwNm_f32 | HwTorque_HwNm_f32 |  |

| VehicleSpeed_Kph_f32 | VehicleSpeed_Kph_f32 |  |

| CombinedAssist_MtrNm_f32 | CombinedAssist_MtrNm_f32 |  |

| AsstFWActive_Uls_f32 | AsstFWActive_Uls_f32 |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| StCmp1Out2_MtrNm_D_f32 | Single Precision Float | -2312 | 2312 | STABILITYCOMP2_START_SEC_VAR_CLEARED_32 |

| StCmp2Out2_MtrNm_D_f32 | Single Precision Float | -2312 | 2312 | STABILITYCOMP2_START_SEC_VAR_CLEARED_32 |

| StCmp3Out2_MtrNm_D_f32 | Single Precision Float | -2312 | 2312 | STABILITYCOMP2_START_SEC_VAR_CLEARED_32 |

| StCmp4Out2_MtrNm_D_f32 | Single Precision Float | -2312 | 2312 | STABILITYCOMP2_START_SEC_VAR_CLEARED_32 |

| HwTorqueSV_HwNm_M_f32 | Single Precision Float | -10 | 10 | STABILITYCOMP2_START_SEC_VAR_CLEARED_32 |

| VehicleSpeedSV_Kph_M_f32 | Single Precision Float | 0 | 511.9921875 | STABILITYCOMP2_START_SEC_VAR_CLEARED_32 |

| AssistDDFactorSV_Uls_M_f32 | Single Precision Float | 1 | 2 | STABILITYCOMP2_START_SEC_VAR_CLEARED_32 |

| CombAstNFSV2_Cnt_M_Str* | N/A | N/A | N/A | STABILITYCOMP2_START_SEC_VAR_CLEARED_UNSPECIFIED |

| CombAstNFSV2_Cnt_M_Str[].SV1_Uls_f32 | Single Precision Floating Point | -2077 | 2077 |  |

| CombAstNFSV2_Cnt_M_Str[].SV2_Uls_f32 | Single Precision Floating Point | -1981 | 1981 |  |

| CombAstNFSV2_Cnt_M_Str[].Out_Uls_f32 | Single Precision Floating Point | -2312 | 2312 |  |

| CombAstNFSV2_Cnt_M_Str[].KPtr_Cnt_Str->A1_Uls_f32 | Single Precision Floating Point | -2 | 0 |  |

| CombAstNFSV2_Cnt_M_Str[].KPtr_Cnt_Str->A2_Uls_f32 | Single Precision Floating Point | -1 | 1 |  |

| CombAstNFSV2_Cnt_M_Str[].KPtr_Cnt_Str->B0_Uls_f32 | Single Precision Floating Point | 0 | 2300 |  |

| CombAstNFSV2_Cnt_M_Str[].KPtr_Cnt_Str->B1_Uls_f32 | Single Precision Floating Point | -4500 | 0 |  |

| CombAstNFSV2_Cnt_M_Str[].KPtr_Cnt_Str->B2_Uls_f32 | Single Precision Floating Point | -4 | 2300 |  |

| HwTrqSV2_HwNm_M_Str | N/A | N/A | N/A | STABILITYCOMP_START_SEC_VAR_CLEARED_UNSPECIFIED |

| HwTrqSV2_HwNm_M_Str.K_Uls_f32 | Single Precision Floating Point | 0.000125 | 0.4666 |  |

| HwTrqSV2_HwNm_M_Str.SV_Uls_f32 | Single Precision Floating Point | 0 | 10 |  |

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

|  |

|  |

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

| Function Name | ApplyStabilityComp2 | ApplyStabilityComp2 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- | --- |

| Arguments Passed | Assist_MtrNm_T_f32 | Assist_MtrNm_T_f32 | float32 | -10.275 | 10.275 |  |

|  | FiltSVPtr_Uls_T_Str* | FiltSVPtr_Uls_T_Str* | Pointer to NotchFiltSV_Str |  |  |  |

|  |  | .SV1_Uls_f32 | float32 | -2077 | 2077 | 0.000489 |

|  |  | .SV2_Uls_f32 | float32 | -1981 | 1981 | 0.000489 |

|  |  | .Out_Uls_f32 | float32 | -2312 | 2312 | 0.000489 |

|  |  | .KPtr_Cnt_Str->A1_Uls_f32 | float32 | -2 | 0 | 0.00005 |

|  |  | .KPtr_Cnt_Str->A2_Uls_f32 | float32 | -1 | 1 | 0.00005 |

|  |  | .KPtr_Cnt_Str->B0_Uls_f32 | float32 | 0 | 2300 | 0.00005 |

|  |  | .KPtr_Cnt_Str->B1_Uls_f32 | float32 | -4500 | 0 | 0.00005 |

|  |  | .KPtr_Cnt_Str->B2_Uls_f32 | float32 | -4 | 2300 | 0.00005 |

|  | CompBlnd_Uls_T_u2p14 | CompBlnd_Uls_T_u2p14 | Pointer to uint16 | 0 | 1 |  |

|  | ADDFBlend_Uls_T_u2p14 | ADDFBlend_Uls_T_u2p14 | uint16 | 0 | 1 |  |

|  | WriteDisplayVars_Cnt_T_lgc | WriteDisplayVars_Cnt_T_lgc | boolean | FALSE | TRUE |  |

| Return Value | FilteredOutput_MtrNm_T_s4p11 | FilteredOutput_MtrNm_T_s4p11 | sint16 (s4p11_T) | -8.8 | 8.8 | 4.89E-04 |

| Data | Value |

| --- | --- |

| AssistDDFactor_Uls_f32 | 1 |

| HwTorque_HwNm_f32 | 0 |

| CombinedAssist_MtrNm_f32 | 0 |

| AsstFWActive_Uls_f32 | 0 |

| VehicleSpeed_Kph_f32 | 0 |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| StabilityComp2_Per1 | 2ms | ALL STATES |

| StabilityComp2_Init1 | STARTUP | COLD INIT |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| <None> |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| StabilityComp2_Per1 |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| ApplyStabilityComp2 |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial MDD | 27 Feb 2013 | SP |

| 2 | 2.0 | Anomaly 4719 fixes | 05 Apr 2013 | SP |

| 4 | 4.0 | Anomaly 4886 Updates.  Range updates and notes about unit testing the notch filter. | 27 Apr 2013 | LWW |

| 5 | 5.0 | Range updates on HwTrq filter SV.  Added tolerance for pointer values on local function. | 06 June 2013 | LWW |

|  |  |  |  |  |
