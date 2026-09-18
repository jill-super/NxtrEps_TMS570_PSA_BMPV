---
title: 'DigPhsReasDiag MDD'
description: 'Converted design document: DigPhsReasDiag MDD'
---

> **Source:** `SVDiag/doc/DigPhsReasDiag_MDD.docx`  
> **Module:** [SVDiag](../../../../cdd/svdiag/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module --

## High-Level Description

This module compares the commanded duty cycle to each phase with the feedback from the NHET module.  The values are compared, compensated with a previously defined fixed value, filtered, and compared against a valid threshold.

## Figures

### Component Diagram

### Diagram – Function Data Sharing

No Shared Data.

## Variable Data Dictionary

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

### Module Internal Variables

This section identifies the name, range and resolutions for module specific data created by this module.  If there are no range restrictions on the variable, the term “FULL” is placed into the table for legal range.

#### User defined typedef definition/declaration

This section documents any user types uniquely used for the module.

## Constant Data Dictionary

### Calibration Constants

This section lists the calibrations used by the module.  For details on calibration constants, refer to the Data Dictionary for the application.

The time constant for the filter is analyzed in the following filter analysis workbook:

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

Limit_m

FPM_Fix_m

LPF_SvUpdate_s16InFixKTrunc_m

LPF_OpUpdate_s16InFixKTrunc_m

Max_m

Min_M

Abs_s16_m

Abs_f16_m

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

None

### Local Functions/Macros Used by this MDD only

#### Local Function #1

##### Description

#### Generates the phase offset
Local Function #2

##### Description

Converts Var_Cnt_T_u16 to Unit16 with range of 0 to 1 and precision of 2-16. It coverts Electrical degree(Count) to Rev

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### DigPhsReasDiag_Init

### Periodic Functions

#### Per: DigPhsReasDiag_ Per1

##### Design Rationale

The ParamBits_Cnt_T_u08 variable used in this function, which is passed when calling NxtrDiagMgr_SetNTCStatus,  is set according to the following table (derived from the DTC Outline Structure document):

##### Program Flow Start

Rte_Call_DigPhsReasDiag_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

MeasuredOnTime_Cnt_T_u32[D_PHASEA_CNT_U16] = Rte_IRead_DigPhsReasDiag_Per1_MeasuredOnTimeA_Cnt_u32();

MeasuredOnTime_Cnt_T_u32[D_PHASEB_CNT_U16] = Rte_Iread_DigPhsReasDiag_Per1_MeasuredOnTimeB_Cnt_u32();

MeasuredOnTime_Cnt_T_u32[D_PHASEC_CNT_U16] = Rte_Iread_DigPhsReasDiag_Per1_MeasuredOnTimeC_Cnt_u32();

ExpectedOnTime_Cnt_T_u32[D_PHASEA_CNT_U16] = Rte_Iread_DigPhsReasDiag_Per1_ExpectedOnTimeA_Cnt_u32();

ExpectedOnTime_Cnt_T_u32[D_PHASEB_CNT_U16] = Rte_Iread_DigPhsReasDiag_Per1_ExpectedOnTimeB_Cnt_u32();

ExpectedOnTime_Cnt_T_u32[D_PHASEC_CNT_U16] = Rte_Iread_DigPhsReasDiag_Per1_ExpectedOnTimeC_Cnt_u32();

LRPRMtrPosCaptured_Rev_T_f32=Rte_IRead_DigPhsReasDiag_Per1_LRPRCorrectedMtrPosCaptured_Rev_f32();

LRPRPhaseadvanceCaptured_Cnt_T_s16 =Rte_IRead_DigPhsReasDiag_Per1_LRPRPhaseadvanceCaptured_Cnt_s16();

LRPRModIdx_Uls_T_f32 = Rte_IRead_DigPhsReasDiag_Per1_LRPRModulationIndexCaptured_Uls_f32();

MotorVelMRFUnfilt_MtrRadpS_T_f32 = Rte_IRead_DigPhsReasDiag_Per1_MotorVelMRFUnfiltered_MtrRadpS_f32();

MtrElecMechPolarity_Cnt_T_s08=Rte_IRead_DigPhsReasDiag_Per1_ElecMechPolarity_Cnt_s08();

PDActivateTest_Cnt_T_lgc = Rte_IRead_DigPhsReasDiag_Per1_PDActivateTest_Cnt_lgc();

##### Subfunction Execution

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

Rte_Call_DigPhsReasDiag_Per1_CP1_CheckpointReached()

#### Per: DigPhsReasDiag_Trans1

##### Design Rationale

Reset the HighRes Phase Reasonableness and LowRes Phase Reasonableness delay counter to 0 upon entering in Operate mode

##### Program Flow Start

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

INLINE functions defined in globalmacro.h are not unit tested

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| ExpectedOnTimeA_Cnt_u32 | ExpectedOnTimeA_Cnt_u32 |  |

| ExpectedOnTimeB_Cnt_u32 | ExpectedOnTimeB_Cnt_u32 |  |

| ExpectedOnTimeC_Cnt_u32 | ExpectedOnTimeC_Cnt_u32 |  |

| MeasuredOnTimeA_Cnt_u32 | MeasuredOnTimeA_Cnt_u32 |  |

| MeasuredOnTimeB_Cnt_u32 | MeasuredOnTimeB_Cnt_u32 |  |

| MeasuredOnTimeC_Cnt_u32 | MeasuredOnTimeC_Cnt_u32 |  |

| LRPRCorrectedMtrPosCaptured_rev_u0p16 | LRPRCorrectedMtrPosCaptured_rev_u0p16 |  |

| LRPRPhaseadvanceCaptured_Cnt_s16 | LRPRPhaseadvanceCaptured_Cnt_s16 |  |

| LRPRModulationIndexCaptured_Uls_f32 | LRPRModulationIndexCaptured_Uls_f32 |  |

| MotorVelMRFUnfiltered_MtrRadpS_f32 | MotorVelMRFUnfiltered_MtrRadpS_f32 |  |

| ElecMechPolarity_Cnt_s08 | ElecMechPolarity_Cnt_s08 |  |

| PDActivateTest_Cnt_lgc | PDActivateTest_Cnt_lgc |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| FilterSV_Cnt_M_s18p13[3] | 2-13 | -210000 | 210000 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_32 |

| PrevLRPRHighSector_Cnt_M_lgc | N/A | FALSE | TRUE | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_BOOLEAN |

| LRPRHighSector_Cnt_M_lgc | N/A | FALSE | TRUE | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_BOOLEAN |

| PrevLRPRLowSector_Cnt_M_lgc | N/A | FALSE | TRUE | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_BOOLEAN |

| LRPRLowSector_Cnt_M_lgc | N/A | FALSE | TRUE | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_BOOLEAN |

| LRPRAdjModldAComp_Cnt_M_f32 | Single precision float | 0 | 1 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_FLOAT32 |

| PrevLRPRAdjModldComp_Cnt_M_f32 | Single precision float | 0 | 1 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_32 |

| PrevLRPRPhsAdvComp_Cnt_M_u16 | 1 | 0 | 6144 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_16 |

| LRPRPhsAdvComp_Cnt_M_u16 | 1 | 0 | 6144 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_16 |

| PhaseOffset_Rev_M_u0p16 | 2-16 | 0 | 1 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_16 |

| LowPhReasErrorAcc_Cnt_M_u16 | 1 | 0 | 1000 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_16 |

| HighResPhsReasDisable_M_u8 | 1 | 0 | 100 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_8 |

| LowResPhsReasDisable_M_u8 | 1 | 0 | 100 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_8 |

| MaxNrCommOffVltg_Cnt_M_f32 | Single precision float | 0 | 86400 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_FLOAT32 |

| LRPRHighLimit_Cnt_D_f32[3] | Single precision float | 0 | 160000 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_FLOAT32 |

| LRPRLowLimit_Cnt_D_f32[3] | Single precision float | 0 | 160000 | DIGPHSREASDIAG_START_SEC_VAR_CLEARED_FLOAT32 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

|  |  |  |  |  |

| Constant Name |

| --- |

| k_PhsReasErrorTerm_Cnt_s16 |

| k_ErrorFiltKn_Cnt_u16 |

| k_ErrorThresh_Cnt_u32 |

| k_PhsReasEnableThresh_Cnt_u32 |

| k_LRPRMtrVelDiagEnable_MtrRadpS_T_f32 |

| k_LowResPhsReas_Cnt_str |

| k_LowResPhsReasMinTol_Uls_f32 |

| k_LowResPhsReasMaxTol_Uls_f32 |

| t_CommOffsetTblY_Cnt_u16 |

| k_LRPRCommOffsetMargin_Uls_f32 |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_ERRORLIMIT_CNT_S32 | 8 | Counts | 262136 |

| D_PHASEA_CNT_U16 | 1 | Counts | 0 |

| D_PHASEB_CNT_U16 | 1 | Counts | 1 |

| D_PHASEC_CNT_U16 | 1 | Counts | 2 |

| D_RESETDIGDIAGACTIVE_CNT_U08 | 1 | Counts | 0x00U |

| D_LRPHSREASLOOPRATE_CNT_F32 | 1 | Counts | 0.002F |

| D_ERRORLIMIT_CNT_S32 | 1 | Counts | 262136L/*2^18-8==262136*/ |

| D_PHASEA_CNT_U16 | 1 | Counts | 0U |

| D_PHASEB_CNT_U16 | 1 | Counts | 1U |

| D_PHASEC_CNT_U16 | 1 | Counts | 2U |

| D_NHETFREQUENCY_HZ_F32 | Single precision float | Counts | 80000000.0F |

| D_NHETCTSPERLRPRLOOP_CNT_F32 | Single precision float | Counts | (D_NHETFREQUENCY_HZ_F32*D_LRPHSREASLOOPRATE_CNT_F32) |

| D_MAXPWMFREQ_HZ_U32 | Single precision float | Counts | 18000 |

| D_MAXNRCOMMOFFVLTG_CNT_F32 | Single precision float | Counts | (D_LRPHSREASLOOPRATE_CNT_F32*D_MAXPWMFREQ_CNT_F32*t_CommOffsetTblY_Cnt_u16[0]) |

| D_PHSADVCNTSPERREV_CNT_U16 | 1 | Counts | 6144U |

| D_PHSADVCNTS180DEG_CNT_U16 | 1 | Counts | 3072U/*(D_PHSADVCNTSPERREV_CNT_S16/2U)*/ |

| D_PHSPOSADVCNTS90DEG_CNT_U16 | 1 | Counts | 1536U/*(D_PHSADVCNTSPERREV_CNT_S16/4U)*/ |

| D_PHSNEGADVCNTS90DEG_CNT_S16 | 1 | Counts | -1536/*(-D_PHSADVCNTSPERREV_CNT_S16/4U)*/ |

| D_0DEG_REV_U0P16 | 1 | rev | (FPM_InitFixedPoint_m(0.0,u0p16_T)) |

| D_30DEG_REV_U0P16 | 1 | rev | (FPM_InitFixedPoint_m(0.0833333333,u0p16_T)) |

| D_60DEG_REV_U0P16 | 1 | rev | (FPM_InitFixedPoint_m(0.1666666666,u0p16_T)) |

| D_240DEG_REV_U0P16 | 1 | rev | (FPM_InitFixedPoint_m(0.6666666666,u0p16_T)) |

| D_120DEG_REV_U0P16 | 1 | rev | (FPM_InitFixedPoint_m(0.3333333333,u0p16_T)) |

| D_180DEG_REV_U0P16 | 1 | rev | (FPM_InitFixedPoint_m(0.5,u0p16_T)) |

| D_PHASEAOFFSETNRM_REV_U0P16 | 2-16 | rev | D_0DEG_REV_U0P16 |

| D_PHASEBOFFSETNRM_REV_U0P16 | 2-16 | rev | ((uint16)(D_PHASEAOFFSETNRM_REV_U0P16-D_120DEG_REV_U0P16)) |

| D_PHASECOFFSETNRM_REV_U0P16 | 2-16 | rev | (D_PHASEAOFFSETNRM_REV_U0P16+D_120DEG_REV_U0P16) |

| D_PHASEAOFFSETINV_REV_U0P16 | 2-16 | rev | D_60DEG_REV_U0P16 |

| D_PHASEBOFFSETINV_REV_U0P16 | 2-16 | rev | (D_PHASEAOFFSETINV_REV_U0P16+D_120DEG_REV_U0P16) |

| D_PHASECOFFSETINV_REV_U0P16 | 2-16 | rev | ((uint16)(D_PHASEAOFFSETINV_REV_U0P16-D_120DEG_REV_U0P16)) |

| D_REVPCNT_ULS_U0P32 | 1 | Uls | 699051UL/*(FPM_InitFixedPoint_m(1/D_PACNTSPREV_ULS_U16P0,u0p32_T))*/ |

| D_PACNTSPREV_ULS_U16P0 | 1 | Uls | 6144U |

| D_SCALER16_CNT_U16 | 1 | cnt | 16U |

| D_35DEG_REV_U0P16 | 1 | rev | (FPM_InitFixedPoint_m(0.0972222222,u0p16_T)) |

| D_205DEG_REV_U0P16 | 1 | rev | (FPM_InitFixedPoint_m(0.5972222222,u0p16_T)) |

| D_245DEG_REV_U0P16 | 1 | rev | (FPM_InitFixedPoint_m(0.6805555555,u0p16_T)) |

| D_355DEG_REV_U0P16 | 1 | rev | (FPM_InitFixedPoint_m(0.9861111111,u0p16_T)) |

| D_POSITIVEONE_CNT_S8 | 1 | cnt | 1 |

| Constant Name |

| --- |

| <None> |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | PhaseGroundTabLookupoffset | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | MtrElecMechPol_Cnt_s8 | Sint8 | -1 | 1 |  |

|  |  |  |  |  |  |

| Return Value | None |  |  |  |  |

| Function Name | Read_CountToRev | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | Var_Cnt_T_u16 | Unit16 | 0 | 6144 |  |

|  |  |  |  |  |  |

| Return Value | CountToRev_Rev_T_u16 | Unit16 | 0 | 1 |  |

| Data | Value |

| --- | --- |

| Rte_InitValue_ExpectedOnTimeA_Cnt_u32 | 0 |

| Rte_InitValue_ExpectedOnTimeB_Cnt_u32 | 0 |

| Rte_InitValue_ExpectedOnTimeC_Cnt_u32 | 0 |

| Rte_InitValue_MeasuredOnTimeA_Cnt_u32 | 0 |

| Rte_InitValue_MeasuredOnTimeB_Cnt_u32 | 0 |

| Rte_InitValue_MeasuredOnTimeC_Cnt_u32 | 0 |

| Rte_InitValue_LRPRCorrectedMtrPosCaptured_Rev_f32 |  |

| Rte_InitValue_LRPRModulationIndexCaptured_Uls_f32 | 0 |

| Rte_InitValue_LRPRPhaseadvanceCaptured_Cnt_s16 | 0 |

| Rte_InitValue_MotorVelMRFUnfiltered_MtrRadpS_f32 |  |

| Rte_InitValue_MtrElecMechPolarity_Cnt_s08 | 0 |

| Rte_ InitValue_ PDActivateTest_Cnt_lgc | 0 |

| Bit 0 | Phase A: measured less than expected |

| --- | --- |

| Bit 1 | Phase A: measured greater than expected |

| Bit 2 | Phase B: measured less than expected |

| Bit 3 | Phase B: measured greater than expected |

| Bit 4 | Phase C: measured less than expected |

| Bit 5 | Phase C: measured greater than expected |

| Bit6 | Systematic diagnostics LRPR Active |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| DigPhsReasDiag_Per1 | 2 ms | Operate |

| DigPhsReasDiag_Trans1 | Upon Transition | Upon entering in Operate |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| <None> |  |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial Version | 25-Jan-12 | OT |

| 2 | 2.0 | Changed Input Names to Match FDD | 27-Jan-12 | OT |

| 3 | 3.0 | Updated Operation states to show only runs in Operate | 27Jan12 | SMW |

| 4 | 4.0 | Updated to latest FDD changes (rev 002-G), consolidated common processing | 31-Jan-12 | OT |

| 5 | 5 | Added checkpoints and memmap software segment is updated for static variables | 26-Sep-12 | Selva |

| 6 | 6 | Updated for Changes for LRPR | 26 Oct 12 | Selva |

| 7 | 7.0 | Updated to FDD V007 | 15 Mar 13 | SP |

| 8 | 8 | Anamoly 4968,4953 changes | 7-May-13 | Selva |

| 9 | 9 | Anamoly 5000 changes | 13-May-13 | Selva |

| 10 | 10 | Fixing Ranges and Data type for unit test results | 16-May-13 | Selva |

| 11 | 11 | Added Cal “k_LRPRCommOffsetMargin_Uls_f32” for FDD v4 | 26-Jun-13 | Selva |

| 12 | 12 | Corrected anomaly 5174 | 30-Jul-13 | VT |

| 13 | 13 | Update range per unit test results | 12-Aug-13 | VT |

|  |  |  |  |  |
