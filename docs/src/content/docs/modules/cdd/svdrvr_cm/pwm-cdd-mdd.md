---
title: 'PWM CDD MDD'
description: 'Converted design document: PWM CDD MDD'
---

> **Source:** `SVDrvr_CM/doc/PWM_CDD_MDD.docx`  
> **Module:** [SVDrvr_CM](../../../../cdd/svdrvr_cm/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module –

## High-Level Description

Non-AUTOSAR PWM driver required to perform EPS motor control PWM profiles.

## Figures

### Component Diagram

This diagram shows all data that is shared between functions within the module.

No data sharing

#### Diagram – Function (Per1)

None (For more refer  section 6)

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

The library functions / Macros that are called by the various sub modules are identified below,

FPM_FloatToFixed_m()

FPM_FixedToFloat_m()

Limit_m()

Max_m()

Min_m()

CDD_Read_PhaseAdvanceFinal_Rev_u0p16()

### Data Hiding Functions

None

### Global Functions/Macros Defined by this Module

#### Global Function #1

##### Description

Applies the offsets needed for MtrElecMech Polarity Setting

#### Global Function #2

##### Description

### Local Functions/Macros Used by this MDD only

Local Macros  are defined in PWMCDD_Cfg.h file as the return values/calculation of return values are more project specific

#### Local Function #1

##### Description

Generates the next PWM Period

#### Local Function #3

##### Description

Calculates ModIndx for each phase

#### Local Macro #1

##### Description

Converts phase advance final from count units to rev units. (Units type conversion)

#### Local Macro #2

##### Description

Reads the Motor position global variable and assign it to “CorrectedMtrPos_Rev_T_u0p16”

#### Local Macro #3

##### Description

Reads the Commutation offset and assign it global variable and assign it to “CommOffset_Cnt_T_u16”

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init: _Init

##### Design Rationale

None

##### Module Outputs

None

##### Module Internal

### Periodic Functions

#### Per: _Per1

##### Design Rationale

None

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

None

##### Processing of function

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

N/A

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

#### SCom: ModuleName_Scom_

##### Design Rationale

None

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

None

##### Processing of function

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

N/A

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

INLINE functions defined in GlobalMacro.h are not unit tested.

## Revision Control Log

\

| Module Inputs (Global Variable Name) | Module Outputs (Global Variable Name) |

| --- | --- |

| CDD_PhaseAdvFinal_Cnt_G_u16[2] |  |

| CDD_CommOffset_Cnt_G_u16[2] | CDD_PWMDutyCycleASum_Cnt_G_u32[2] |

| CDD_MtrPosElec_Rev_G_u0p16[2] | CDD_PWMDutyCycleBSum_Cnt_G_u32[2] |

| CDD_PwmDisable_Cnt_G_lgc[2] | CDD_PWMDutyCycleCSum_Cnt_G_u32[2] |

|  | CDD_PWMPeriodSum_Cnt_G_u32[2] |

|  | CDD_PhsReasA_Cnt_G_u16[2] |

| CDD_ModIdxFinal_Uls_G_u16p16[2] | CDD_PhsReasB_Cnt_G_u16[2] |

| CDD_CDDDataAccessBfr_Cnt_G_u16 | CDD_PhsReasC_Cnt_G_u16[2] |

| CDD_AppDataFwdPthAccessBfr_Cnt_G_u16 | CDD_DCPhsComp_Cnt_G_u16[3] |

| CDD_AppDataFbkPthAccessBfr_Cnt_G_u16 | CDD_PWMPeriod_Cnt_G_u16 |

| Variable Name | Resolution | (min) | (max) | Software Segment |

| --- | --- | --- | --- | --- |

| CDD_SeedPWMDither_Cnt_M_u16 | 1 | 0 | 65535 | PWMCDD_START_SEC_VAR_CLEARED_16 |

| CDD_DitherFlt1SV_Cnt_M_u16 | 1 | 0 | 65535 | PWMCDD_START_SEC_VAR_CLEARED_16 |

| CDD_DitherFlt2SV_Cnt_M_u16 | 1 | 0 | 65535 | PWMCDD_START_SEC_VAR_CLEARED_16 |

| CDD_PhaseOffset_Rev_M_u0p16[3] | 2^-16 | 0 | 0.99998 | PWMCDD_START_SEC_VAR_CLEARED_16 |

|  |  |  |  |  |

| PrevDCPhsAComp_Cnt_M_u16p0 | 1 | 0 | 7150 | PWMCDD_START_SEC_VAR_CLEARED_16 |

| PrevDCPhsBComp_Cnt_M_u16p0 | 1 | 0 | 7150 | PWMCDD_START_SEC_VAR_CLEARED_16 |

| PrevDCPhsCComp_Cnt_M_u16p0 | 1 | 0 | 7150 | PWMCDD_START_SEC_VAR_CLEARED_16 |

| DCPhsAComp_Cnt_M_u16p0 | 1 | 0 | 7150 | PWMCDD_START_SEC_VAR_CLEARED_16 |

| DCPhsBComp_Cnt_M_u16p0 | 1 | 0 | 7150 | PWMCDD_START_SEC_VAR_CLEARED_16 |

| DCPhsCComp_Cnt_M_u16p0 | 1 | 0 | 7150 | PWMCDD_START_SEC_VAR_CLEARED_16 |

| PrevPWMPeriod_Cnt_M_u16 | 1 | 2950 | 7150 | PWMCDD_START_SEC_VAR_CLEARED_16 |

| PWMPeriod_Cnt_M_u16 | 1 | 2950 | 7150 | PWMCDD_START_SEC_VAR_CLEARED_16 |

|  |  |  |  |  |

|  |  |  |  |  |

|  |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Constant Name |

| --- |

|  |

|  |

| k_DitherLPFKn_Cnt_u16 |

|  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| d_NhetFreq_Hz_Cnt_u16 | 1 | u16 | 75000000UL |

|  |  |  |  |

| d_HalfPrec16_Cnt_u16 | 1 | u16 | 32768UL |

| d_Scaler1_Cnt_u16 | 1 | u16 | 1U |

|  |  |  |  |

| d_Scaler16_Cnt_u16 | 1 | u16 | 16U |

| d_SeedInitial_Cnt_u16 | 1 | u16 | 10U |

| d_SeedMultiplier_Cnt_u16 | 1 | u16 | 57U |

| d_SeedOffset_Cnt_u16 | 1 | u16 | 1U |

|  |  |  |  |

|  |  |  |  |

| d_PWMFreqDither_Hz_u16 | 1 | u16 | 2000U |

|  |  |  |  |

|  |  |  |  |

|  |  |  |  |

|  |  |  |  |

| d_FilterKdBits_Cnt_U16 | 1 | u16 | 5U |

| d_MaxModIdx_Uls_u0p16 | 2-16 | u0p16 | (FPM_InitFixedPoint_m(0.9999847412109375,u0p16_T)) |

| d_MinModIdx_Uls_u0p16 | 2-16 | u0p16 | (FPM_InitFixedPoint_m(0.0,u0p16_T)) |

| d_120Deg_Rev_u0p16 | 2-16 | u0p16 | (FPM_InitFixedPoint_m(0.3333333333,u0p16_T)) |

| d_0Deg_Rev_u0p16 | 2-16 | u0p16 | (FPM_InitFixedPoint_m(0.0,u0p16_T)) |

| d_30Deg_Rev_u0p16 | 2-16 | u0p16 | (FPM_InitFixedPoint_m(0.0833333333,u0p16_T)) |

| d_60Deg_Rev_u0p16 | 2-16 | u0p16 | (FPM_InitFixedPoint_m(0.1666666666,u0p16_T)) |

| d_240Deg_Rev_u0p16 | 2-16 | u0p16 | (FPM_InitFixedPoint_m(0.6666666666,u0p16_T)) |

| d_180Deg_Rev_u0p16 | 2-16 | u0p16 | (FPM_InitFixedPoint_m(0.5,u0p16_T)) |

| d_PhaseAOffsetNrm_Rev_u0p16 | 2-16 | u0p16 | d_0Deg_Rev_u0p16 |

| d_PhaseBOffsetNrm_Rev_u0p16 | 2-16 | u0p16 | ((uint16)(d_PhaseAOffsetNrm_Rev_u0p16-d_120Deg_Rev_u0p16)) |

| d_PhaseCOffsetNrm_Rev_u0p16 | 2-16 | u0p16 | (d_PhaseAOffsetNrm_Rev_u0p16+d_120Deg_Rev_u0p16) |

| d_PhaseAOffsetInv_Rev_u0p16 | 2-16 | u0p16 | d_60Deg_Rev_u0p16 |

| d_PhaseBOffsetInv_Rev_u0p16 | 2-16 | u0p16 | (d_PhaseAOffsetInv_Rev_u0p16+d_120Deg_Rev_u0p16) |

| d_PhaseCOffsetInv_Rev_u0p16 | 2-16 | u0p16 | ((uint16)(d_PhaseAOffsetInv_Rev_u0p16-d_120Deg_Rev_u0p16)) |

| d_RevpCnt_Uls_u0p32 | 2-32 | u0p32 | 699051UL/*(FPM_InitFixedPoint_m(1/d_PACntspRev_Uls_u16p0,u0p32_T))*/ |

| d_PACntspRev_Uls_u16p0 | 1 | u16p0 | 6144U |

| d_SinePhsToGndTblSize_Cnt_u16 | 1 | u16 | 2049U |

| d_MSBMask_Cnt_u16 | 1 | u16 | 0x8000U |

| D_POSITIVEONE_CNT_S8 | 1 | s8 | 1 |

| D_PHSAIDX_CNT_U16 | 1 | u16 | 0U |

| D_PHSBIDX_CNT_ U16 | 1 | u16 | 1U |

| D_PHSCIDX_CNT_ U16 | 1 | u16 | 2U |

| Constant Name |

| --- |

|  |

|  |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| t_S_SinePhsToGndTbl_Cnt_u0p16[2049] | 2-16 |  | None |

| Function Name | CDD_ApplyPWMMtrElecMechPol | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | MtrElecMechPol_Cnt_s8 | Sint 8 | -1 | 1 |  |

|  |  |  |  |  |  |

| Return Value | CDD_PhaseOffset_Rev_M_u0p16 | Uint16 | 0 | 0.999987 |  |

| Function Name | CDDPorts_ClearPhsReasSum | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | DataAccessBfr_Cnt_T_u16 | Uint16 | 0 | 1 |  |

| Return Value | CDD_PWMDutyCycleASum_Cnt_G_u32 | Uint32 | 0 | 200000 | N/A |

|  | CDD_PWMDutyCycleBSum_Cnt_G_u32 | Uint32 | 0 | 200000 | N/A |

|  | CDD_PWMDutyCycleCSum_Cnt_G_u32 | Uint32 | 0 | 200000 | N/A |

|  | CDD_PWMPeriodSum_Cnt_G_u32 | Uint32 | 0 | 200000 | N/A |

| Function Name | PwmPeriodDither_u16 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | PWMPeriod_Cnt_T_u16 | Unit16 | 0 | 65535 |  |

| Function Name | ModIndxPhase_u0p16 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | PhaseIndex_Rev_T_u0p16 | Uint16 | 0 | 0.999987 |  |

|  |  |  |  |  |  |

| Return Value | ModIdxPhs_Cnt_T_u0p16 | Uint16 | 0 | 0.999987 |  |

| Function Name | CDD_Read_PhaseAdvanceFinal_Rev_u0p16 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | &PhaseAdvFinal_Rev_T_u0p16 | U0p16 | 0 | 1 |  |

|  |  |  |  |  |  |

| Return Value | none |  |  |  |  |

| Function Name | CDD_Read_CorrectedMtrPos_Rev_u0p16 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | & CorrectedMtrPos_Rev_T_u0p16 | U0p16 | 0 | 0.999984741 |  |

|  |  |  |  |  |  |

| Return Value | none |  |  |  |  |

| Function Name | CDD_Read_CommOffset_Cnt_u16 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | &CommOffset_Cnt_T_u16 | U16 | 0 | 65535 |  |

|  |  |  |  |  |  |

| Return Value | none |  |  |  |  |

| Data | Value |

| --- | --- |

| None |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| PwmCdd_Init | Once | EcuStartup |

| PwmCdd_Per1 | Motor control ISR | All states |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial Version | 17 Oct 2012 | Selva |

| 2 | 2.0 | Nhet specific names are changed to common names and project specific variables assignment are moved to configuration Macros to keep PWMCdd same across projects | 15-Feb-12 | Selva |

| 3 | 3.0 | Changed the Buffer index of CDD_ModIdxFinal_Uls_G_u16p16 from "CDD_AppDataFwdPthAccessBfr_Cnt_G_u16" to "CDD_CDDDataAccessBfr_Cnt_G_u16" | 19-Apr-13 | Selva |

| 4 | 4.0 | Updated for ranges for UTP | 1-July-13 | Selva |

| 5 | 5.0 | Deleted Dead time compensation and corrected the DCPhase calculation | 1-Nov -13 | Selva |

|  |  |  |  |  |
