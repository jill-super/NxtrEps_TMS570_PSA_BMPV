---
title: 'Assist Firewall MDD'
description: 'Converted design document: Assist Firewall MDD'
---

> **Source:** `AssistFirewall/doc/Assist_Firewall_MDD.docx`  
> **Module:** [AssistFirewall](../../../../asw/assistfirewall/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module --

## High-Level Description

This module limits the output from the Assist module according to safety requirements.

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

LPF_KUpdate_f32_m

LPF_OpUpdate_f32_m

HPF_KUpdate_f32_m

HPF_OpUpdate_f32_m

BilinearXMYM_s16_s16XMs16YM_Cnt

TableSize_m

FPM_FloatToFixed_m

FPM_FixedToFloat_m

- DiagPStep_m

- DiagNStep_m

- Rte_Call_NxtrDiagMgr_SetNTCStatus

### Data Hiding Functions

None

### Global Functions/Macros Defined by this Module

None

### Local Functions/Macros Used by this MDD only

None

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init: _Init1

##### Design Rationale

An initialization function is required to initialize K for each of the filters.

##### Module Outputs

None

##### Module Internal

None

##### Initialize Filters

### Periodic Functions

#### Per: _Per1

##### Design Rationale

None

##### Program Flow Start

##### Rte_Call_AssistFirewall_Per1_CP0_CheckpointReached()Store Module Inputs to Local copies

BaseAssistCmd_MtrNm_T_f32 = Rte_IRead_AssistFirewall_Per1_BaseAssistCmd_MtrNm_f32()

HighFreqAssist_MtrNm_T_f32 = Rte_IRead_AssistFirewall_Per1_HighFreqAssist_MtrNm_f32()

HwTorque_HwNm_T_f32 = Rte_IRead_AssistFirewall_Per1_HwTorque_HwNm_f32()

HysteresisComp_MtrNm_T_f32 = Rte_IRead_AssistFirewall_Per1_HysteresisComp_MtrNm_f32()

VehicleSpeed_Kph_T_f32 = Rte_IRead_AssistFirewall_Per1_VehicleSpeed_Kph_f32()

AsstFWPstepNstep_Cnt_T_str.PStep = k_AsstFWPstep_Cnt_u16

AsstFWPstepNstep_Cnt_T_str.NStep = k_AsstFWNstep_Cnt_u16

AsstFWPstepNstep_Cnt_T_str.Threshold = t_AsstFWPstepNstepThresh_Cnt_u16[1]

AbsHwTrq_HwNm_T_u8p8 = FPM_FloatToFixed_m(Abs_f32_m(HwTorque_HwNm_T_f32), u8p8_T)

##### Sum and Filter Inputs

##### Determine Saturation Bounds and Perform Limiting

##### Determine Active State and Output

##### Store Local copy of outputs into Module Outputs

AsstFWUprBound_MtrNm_D_f32 = UprBound_MtrNm_T_f32

AsstFWLwrBound_MtrNm_D_f32 = LwrBound_MtrNm_T_f32

AsstFWUprBoundFilt_MtrNm_D_f32 = UprBoundFilt_MtrNm_T_f32

AsstFWLwrBoundFilt_MtrNm_D_f32 = LwrBoundFilt_MtrNm_T_f32

AsstFWSumInput_MtrNm_D_f32 = SumInput_MtrNm_T_f32

AsstFWLowFreqInput_MtrNm_D_f32 = LowFreqInput_MtrNm_T_f32

AsstFWLowFreqLimited_MtrNm_D_f32 = LowFreqLimited_MtrNm_T_f32

AsstFWActiveRaw_Uls_D_f32  = AsstFWActiveRaw_Uls_T_f32

Rte_IWrite_AssistFirewall_Per1_CombinedAssist_MtrNm_f32(CombAsstSV_MtrNm_M_f32)

Rte_IWrite_AssistFirewall_Per1_AsstFirewallActive_Uls_f32(AsstFWActive_Uls_T_f32)

##### Program Flow End

Rte_Call_AssistFirewall_Per1_CP1_CheckpointReached()

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

## Execution Requirements

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

INLINE functions in GlobalMacro.h are not unit tested.

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| BaseAssistCmd_MtrNm_f32 | BaseAssistCmd_MtrNm_f32 | AsstFirewallActive_Uls_f32 |

| HighFreqAssist_MtrNm_f32 | HighFreqAssist_MtrNm_f32 | CombinedAssist_MtrNm_f32 |

| HwTorque_HwNm_f32 | HwTorque_HwNm_f32 |  |

| HysteresisComp_MtrNm_f32 | HysteresisComp_MtrNm_f32 |  |

| VehicleSpeed_Kph_f32 | VehicleSpeed_Kph_f32 |  |

|  |  |  |

|  |  |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| UprBoundKSV_M_str |  |  |  | ASSISTFIREWALL_START_SEC_VAR_CLEARED_UNSPECIFIED |

| LwrBoundKSV_M_str |  |  |  | ASSISTFIREWALL_START_SEC_VAR_CLEARED_UNSPECIFIED |

| HiFreqKSV_M_str |  |  |  | ASSISTFIREWALL_START_SEC_VAR_CLEARED_UNSPECIFIED |

| ActiveKSV_M_str |  |  |  | ASSISTFIREWALL_START_SEC_VAR_CLEARED_UNSPECIFIED |

| ActiveRawAcc_Cnt_M_u16 | 1 | FULL | FULL | ASSISTFIREWALL_START_SEC_VAR_CLEARED_16 |

| PNCountStatus_Cnt_M_lgc | n/a | FALSE | TRUE | ASSISTFIREWALL_START_SEC_VAR_CLEARED_ BOOLEAN |

| AsstFWUprBound_MtrNm_D_f32 | Single Precision Floating Point | -8.8 | 8.8 | ASSISTFIREWALL_START_SEC_VAR_CLEARED_32 |

| AsstFWLwrBound_MtrNm_D_f32 | Single Precision Floating Point | -8.8 | 8.8 | ASSISTFIREWALL_START_SEC_VAR_CLEARED_32 |

| AsstFWSumInput_MtrNm_D_f32 | Single Precision Floating Point | -26.4 | 26.4 | ASSISTFIREWALL_START_SEC_VAR_CLEARED_32 |

| AsstFWLowFreqInput_MtrNm_D_f32 | Single Precision Floating Point | -26.4 | 26.4 | ASSISTFIREWALL_START_SEC_VAR_CLEARED_32 |

| AsstFWLowFreqLimited_MtrNm_D_f32 | Single Precision Floating Point | -8.8 | 8.8 | ASSISTFIREWALL_START_SEC_VAR_CLEARED_32 |

| AsstFWActiveRaw_Uls_D_f32 | Single Precision Floating Point | 0 | 1 | ASSISTFIREWALL_START_SEC_VAR_CLEARED_32 |

| AsstFWUprBoundFilt_MtrNm_D_f32 | Single Precision Floating Point | -8.8 | 8.8 | ASSISTFIREWALL_START_SEC_VAR_CLEARED_32 |

| AsstFWLwrBoundFilt_MtrNm_D_f32 | Single Precision Floating Point | -8.8 | 8.8 | ASSISTFIREWALL_START_SEC_VAR_CLEARED_32 |

| CombAsstSV_MtrNm_M_f32 | Single Precision Floating Point | -8.8 | 8.8 | ASSISTFIREWALL_START_SEC_VAR_CLEARED_32 |

| AsstFWOverBound_Cnt_D_lgc | n/a | FALSE | TRUE | ASSISTFIREWALL_START_SEC_VAR_CLEARED_BOOLEAN |

| AsstReducedPerfSV_Cnt_M_lgc | n/a | FALSE | TRUE | ASSISTFIREWALL_START_SEC_VAR_CLEARED_ BOOLEAN |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Constant Name |

| --- |

| k_AsstFWInpLimitHysComp_MtrNm_f32 |

| k_AsstFWInpLimitHFA_MtrNm_f32 |

| k_AsstFWInpLimitBaseAsst_MtrNm_f32 |

| k_AsstFWFiltKn_Hz_f32 |

| k_AsstFWFWActiveLPF_Hz_f32 |

| t__Kph_u9p7[12] |

| t2_AsstFWUprBoundX_HwNm_s4p11[12][11] |

| t2_AsstFWUprBoundY_MtrNm_s4p11[12][11] |

|  |

|  |

| k_AsstFWPstep_Cnt_u16 |

| k_AsstFWNstep_Cnt_u16 |

| t_AsstFWPstepNstepThresh_Cnt_u16[2] |

| t_AsstFWDefltAssistX_HwNm_u8p8[20] |

| t_AsstFWDefltAssistY_MtrNm_s4p11[20] |

| k_RestoreThresh_MtrNm_f32 |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| None |  |  |  |

| Constant Name |

| --- |

| D_ONE_ULS_F32 |

| D_ZERO_ULS_F32 |

| D_2MS_SEC_F32 |

| BC_ASSISTFIREWALL_FAULTINJECTIONPOINT |

| STD_ON |

| FLTINJ_ASSTFIREWALL |

| D_MTRTRQCMDLOLMT_MTRNM_F32 |

| D_MTRTRQCMDHILMT_MTRNM_F32 |

| D_NEGONE_CNT_S16 |

|  |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Data | Value |

| --- | --- |

| Rte_InitValue_AsstFirewallActive_Uls_f32 | 0 |

| Rte_InitValue_BaseAssistCmd_MtrNm_f32 | 0 |

| Rte_InitValue_CombinedAssist_MtrNm_f32 | 0 |

| Rte_InitValue_HighFreqAssist_MtrNm_f32 | 0 |

| Rte_InitValue_HwTorque_HwNm_f32 | 0 |

| Rte_InitValue_HysteresisComp_MtrNm_f32 | 0 |

| Rte_InitValue_VehicleSpeed_Kph_f32 | 0 |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| AssistFirewall_Init1 | On Event | On Init |

| AssistFirewall_Per1 | 2 ms | ALL |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| <None> |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| AssistFirewall_Init1 | RTE_START_SEC_AP_ASSISTFIREWALL_APPL_CODE |

| AssistFirewall_Per1 | RTE_START_SEC_AP_ASSISTFIREWALL_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial Version | 24-Apr-12 | OT |

| 2 | 2.0 | Fixed conflicting calibration names | 10-May-12 | OT |

| 3 | 3.0 | Added fault injection point | 18-May-12 | OT |

| 4 | 4.0 | Updated to SF-34 v002, fixed conflicting display variable names | 31-May-12 | OT |

| 5 | 5.0 | Updated to SF-34 v003 | 08-Jun-12 | OT |

| 6 | 6.0 | Fixed threshold assignment anomaly | 11-Jun-12 | OT |

| 7 | 7.0 | Updated to SF-34 v004 | 20-Jun-12 | OT |

| 8 | 8.0 | Updated to SF-34 Ver 005 and Ver 006 | 1-Aug-12 | NRAR |

| 9 | 9.0 | Inserted safe watchdog checkpoints | 15-Sept-12 | BWL |

| 10 | 10.0 | Corrected Unspecified  variable name  to “Boolean” | 18 –Sep-12 | SSK |

| 11 | 11.0 | Updates to meet SF-34 v007 | 01-Feb-13 | VK |

| 12 | 12.0 | MDD/ Src mismatch updates | 22-Feb-13 | VK |

|  |  |  |  |  |
