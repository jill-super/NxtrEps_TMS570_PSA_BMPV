---
title: 'CmMtrCurr MDD'
description: 'Converted design document: CmMtrCurr MDD'
---

> **Source:** `CmMtrCurr/doc/CmMtrCurr_MDD.docx`  
> **Module:** [CmMtrCurr](../../../../asw/cmmtrcurr/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module -- CmMtrCurr

## High-Level Description

The Current Measurement function is responsible for measuring the motor phase currents used as feedback by the Motor Control FDD. Two motor phase currents are measured using a shunt resistor and a differential amplifier circuitry, and along with the motor position are transformed into direct (D) and quadrature (Q) axes currents using the combined Clarke/Park transform

UNIT Test Notes:

Unit  test should be done with enabling one of the six predefned macro  MTRCURRPHASEBC, MTRCURRPHASECB, MTRCRRPHASECA, MTRCURRPHASEAB, MTRCURRPHASEAC, MTRCURRPHASEBA. Hence it should have six UTP results (one for each Macro enabled).

## Figures

### Component diagram

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

(This is for lookup tables (arrays) with fixed values, same name as other tables)

## Functions/Macros used by the Sub-Modules

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules are identified below,

Cosf

Sinf

Limit_m

Abs_f32_m

TableSize_m

FPM_FloatToFixed_m

FPM_FixedToFloat_m

IntplVarXY_s16_s16Xs16Y_Cnt

LPF_SvUpdate_u16InFixKTrunc_m

LPF_OpUpdate_u16InFixKTrunc_m

LPF_SvUpdate_s16InFixKTrunc_m

LPF_OpUpdate_s16InFixKTrunc_m

LPF_KUpdate_f32_m

LPF_OpUpdate_f32_m

### Data Hiding Functions

CmMtrCurr_Read_MRFMtrVel_MtrRadpS_f32

CmMtrCurr_Read_Vecu_Volt_f32

CmMtrCurr_Read_Phs1Curr_Cnt_u16

CmMtrCurr_Read_Phs2Curr_Cnt_u16

CmMtrCurr_Read_DCPhsAComp_Cnt_u16

CmMtrCurr_Read_DCPhsBComp_Cnt_u16

CmMtrCurr_Read_DCPhsCComp_Cnt_u16

CmMtrCurr_Read_MtrCurr1TempOffset_Volt_f32

CmMtrCurr_Read_MtrCurr2TempOffset_Volt_f32

CmMtrCurr_Read_MtrElecPol_Cnt_s08

CmMtrCurr_Read_MtrPosElec_Rev_u0p16

CmMtrCurr_Write_ElecPosDelayComp_Rad_f32

CmMtrCurr_Write_MtrCurrQax_Amp_f32

CmMtrCurr_Write_MtrCurrDax_Amp_f32

CmMtrCurr_Write_CorrMtrPosElec_Rev_f32

CmMtrCurr_Write_MtrCurrK1_Amps_f32

CmMtrCurr_Write_MtrCurrK2_Amps_f32

CmMtrCurr_Write_MtrCurr1_Volts_f32

CmMtrCurr_Write_MtrCurr2_Volts_f32

### Global Functions/Macros Defined by this Module

None

### Local Functions/Macros Used by this MDD only

None

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init: CmMtrCurr_Init

##### Design Rationale

None

##### Module Outputs

None

##### Module Internal

### IF ((Rte_Pim_ShCurrCal()->EOLMtrCurrVcalCmd_VoltCnts_f32) >= D_MINVCALCMD_CNT_F32)

CmMtrCurr_MtrCurr1OffDelta_VoltpVoltCnt_M_f32 = ((Rte_Pim_ShCurrCal()->EOLMtrCurr1OffsetDiff_Volts_f32) / (Rte_Pim_ShCurrCal()->EOLMtrCurrVcalCmd_VoltCnts_f32))

CmMtrCurr_MtrCurr2OffDelta_VoltpVoltCnt_M_f32 = ((Rte_Pim_ShCurrCal()->EOLMtrCurr2OffsetDiff_Volts_f32) / (Rte_Pim_ShCurrCal()->EOLMtrCurrVcalCmd_VoltCnts_f32))

### ELSE

### CmMtrCurr_MtrCurr1OffDelta_VoltpVoltCnt_M_f32 = D_ZERO_ULS_F32

### CmMtrCurr_MtrCurr2OffDelta_VoltpVoltCnt_M_f32 = D_ZERO_ULS_F32

### END

LPF_KUpdate_f32_m(k_CurrCorrErrFiltFc_Hz_f32, D_2MS_SEC_F32, &CmMtrCurr_CurrCorrDiagKSV_M_str)

### Periodic Functions

#### Per: CmMtrCurr_Per1

##### Design Rationale

None

##### Program Flow Start

Rte_Call_CmMtrCurr_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

FiltCntrlTemp_DegC_T_f32=Rte_IRead_CmMtrCurr_Per1_FiltCntrlTemp_DegC_f32()

##### Processing

##### Store Local copy of outputs into Module Outputs

Rte_Iwrite_CmMtrCurr_Per1_MtrCurr1TempOffset_Volt_f32(MtrCurr1TempOffset_Volts_T_f32)

Rte_Iwrite_CmMtrCurr_Per1_MtrCurr2TempOffset_Volt_f32(MtrCurr2TempOffset_Volts_T_f32)

##### Program Flow End

Rte_Call_CmMtrCurr_Per1_CP1_CheckpointReached()

#### Per: CmMtrCurr_Per2

##### Design Rationale

None

##### Program Flow Start

Rte_Call_CmMtrCurr_Per2_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

MtrCurrAlpha_Rev_T_f32=Rte_Iread_CmMtrCurr_Per2_MtrCurrAngle_ Rev_f32()

CorrMtrPosElec_Rev_T_f32=Rte_Iread_CmMtrCurr_Per2_CorrMtrCurrPosition_Rev_f32()

MtrCurrK1_Amps_T_f32=Rte_Iread_CmMtrCurr_Per2_MtrCurrK1_Amp_f32()

MtrCurrK2_Amps_T_f32=Rte_Iread_CmMtrCurr_Per2_MtrCurrK2_Amp_f32()

ADCMtrCurr1_Volts_T_f32=Rte_Iread_CmMtrCurr_Per2_ADCMtrCurr1_Volts_f32()

ADCMtrCurr2_Volts_T_f32=Rte_Iread_CmMtrCurr_Per2_ADCMtrCurr2_Volts_f32()

##### Processing

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

Rte_Call_CmMtrCurr_Per2_CP1_CheckpointReached()

#### Per: CmMtrCurr_Per3

##### Design Rationale

None

##### Program Flow Start

Rte_Call_CmMtrCurr_Per3_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

ADCMtrCurr1_Volts_T_f32=Rte_Iread_CmMtrCurr_Per3_ADCMtrCurr1_Volts_f32()

ADCMtrCurr2_Volts_T_f32=Rte_Iread_CmMtrCurr_Per3_ADCMtrCurr2_Volts_f32()

Vecu_Volt_T_f32=Rte_Iread_CmMtrCurr_Per3_Vecu_Volt_f32()

MtrVel_MtrRadpS_T_f32 = Rte_Iread_CmMtrCurr_Per3_MtrVel_MtrRadpS_f32()

VehSpd_Kph_T_f32= Rte_Iread_CmMtrCurr_Per3_VehSpd_Kph_f32()

VhSpdValid_Cnt_T_lgc= Rte_Iread_CmMtrCurr_Per3_VhSpdValid_Cnt_lgc()

SrlComSvcDft_Cnt_T_b32=Rte_Iread_CmMtrCurr_Per3_SrlComSvcDft_Cnt_b32()

CurroffProcessFlag_T_enum = CmMtrCurr_CurroffProcessFlag_M_enum

##### Processing

##### Store Local copy of outputs into Module Outputs

Rte_Iwrite_CmMtrCurr_Per3_ComOffset_Cnt_u16(ComOffset_Cnt_T_u16)

##### Program Flow End

Rte_Call_CmMtrCurr_Per3_CP1_CheckpointReached()

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

#### CurrDQPer1

##### Design Rationale

None

##### Program Flow Start

N/A

##### Store Module Inputs to Local Copies

CmMtrCurr_Read_MRFMtrVel_MtrRadpS_f32(&MRFMtrVel_MtrRadpS_T_f32)

CmMtrCurr_Read_Vecu_Volt_f32(&Vecu_Volt_T_f32)

CmMtrCurr_Read_Phs1Curr_Cnt_u16(&Phs1Curr_Cnt_T_u16)

CmMtrCurr_Read_Phs2Curr_Cnt_u16(&Phs2Curr_Cnt_T_u16)

CmMtrCurr_Read_MtrCurr1TempOffset_Volt_f32(&MtrCurr1TempOffset_Volt_T_f32)

CmMtrCurr_Read_MtrCurr2TempOffset_Volt_f32(&MtrCurr2TempOffset_Volt_T_f32)

CmMtrCurr_Read_MtrElecPol_Cnt_s08(&MtrElecPol_Cnt_T_s08)

CmMtrCurr_Read_MtrPosElec_Rev_u0p16(&MtrPosElec_Rev_T_u0p16)

##### Processing

##### Store Local copy of outputs into Module Outputs

CmMtrCurr_Write_ElecPosDelayComp_Rad_f32(ElecPosDelayComp_Rad_T_f32)

CmMtrCurr_Write_MtrCurrQax_Amp_f32(MtrCurrFinalQax_Amps_T_f32)

CmMtrCurr_Write_MtrCurrDax_Amp_f32(MtrCurrFinalDax_Amps_T_f32)

CmMtrCurr_Write_CorrMtrPosElec_Rev_f32(CorrMtrPosElec_Rev_T_f32)

CmMtrCurr_Write_MtrCurrK1_Amps_f32(MtrCurrK1_Amps_T_f32)

CmMtrCurr_Write_MtrCurrK2_Amps_f32(MtrCurrK2_Amps_T_f32)

CmMtrCurr_Write_MtrCurr1_Volts_f32(Phs1Curr_Volts_T_f32)

CmMtrCurr_Write_MtrCurr2_Volts_f32(Phs2Curr_Volts_T_f32)

##### Program Flow End

N/A

### Serial Communication Functions

#### Scomm: CmMtrCurrTempOffset_Scom_Get

##### Design Rationale

None

##### Program Flow Start

None

##### Store Module Inputs to Local copies

None

##### Processing

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

None

#### Scomm: CmMtrCurrTempOffset_Scom_Set

##### Design Rationale

None

##### Program Flow Start

None

##### Store Module Inputs to Local copies

None

##### Processing

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

None

#### Scomm: CmMtrCurr_Scom_CalGain

##### Design Rationale

None

##### Program Flow Start

None

##### Store Module Inputs to Local copies

Rte_Read_MtrVel_MtrRadpS_f32(&MtrVel_MtrRadpS_T_f32)

Rte_Read_VehSpd_Kph_f32(&VehSpd_Kph_T_f32)

Rte_Read_VhSpdValid_Cnt_lgc(&VhSpdValid_T_Cnt_lgc)

##### Processing

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

None

#### Scomm: CmMtrCurr_Scom_CalOffset

##### Design Rationale

None

##### Program Flow Start

None

##### Store Module Inputs to Local copies

Rte_Read_MtrVel_MtrRadpS_f32(&MtrVel_MtrRadpS_T_f32)

Rte_Read_VehSpd_Kph_f32(&VehSpd_Kph_T_f32)

Rte_Read_VhSpdValid_Cnt_lgc(&VhSpdValid_T_Cnt_lgc)

##### Processing

##### Store Local copy of outputs into Module Outputs

Rte_Write_CurrentGainSvc_Cnt_lgc(CmMtrCurr_CurrentGainSvc_Cnt_M_lgc)

##### Program Flow End

None

#### Scomm: CmMtrCurr_Scom_MtrCurrOffReadStatus

##### Design Rationale

None

##### Program Flow Start

None

##### Store Module Inputs to Local copies

None

##### Processing

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

None

#### Scomm: CmMtrCurr_Scom_ReadMtrCurrCals

##### Design Rationale

None

##### Program Flow Start

None

##### Store Module Inputs to Local copies

None

##### Processing

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

None

#### Scomm: CmMtrCurr_Scom_SetMtrCurrCals

##### Design Rationale

None

##### Program Flow Start

None

##### Store Module Inputs to Local copies

None

##### Processing

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

None

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

INLINE functions defined in GlobalMacro.h are not unit tested.

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| ADCMtrCurr1_Volt_f32 | ADCMtrCurr1_Volt_f32 | MtrCurrQax_Amps_f32 |

| ADCMtrCurr2_Volt_f32 | ADCMtrCurr2_Volt_f32 | MtrCurrDax_Amps_f32 |

| MtrVel_MtrRadpS_f32 | MtrVel_MtrRadpS_f32 | CurrentGainSvc_Cnt_lgc |

| FiltCntrlTemp_DegC_f32 | FiltCntrlTemp_DegC_f32 | ComOffset_Cnt_u16 |

| MtrCurrAngle_Rev_f32 | MtrCurrAngle_Rev_f32 | ElecPosDelayComp_Rad_f32 |

| VehSpd_Kph_f32 | VehSpd_Kph_f32 | CorrMtrCurrPosition_Rev_f32 |

| VhSpdValid_Cnt_lgc | VhSpdValid_Cnt_lgc | MtrCurrK1_Amps_f32 |

| Vecu_Volt_f32 | Vecu_Volt_f32 | MtrCurrK2_Amps_f32 |

| MtrCurr1TempOffset_Volt_f32 | MtrCurr1TempOffset_Volt_f32 | MtrCurr1_Volts_f32 |

| MtrCurr2TempOffset_Volt_f32 | MtrCurr2TempOffset_Volt_f32 | MtrCurr2_Volts_f32 |

| Phs1Curr_Cnt_u16 | Phs1Curr_Cnt_u16 | MtrCurrQax_Amps_f32 |

| Phs2Curr_Cnt_u16 | Phs2Curr_Cnt_u16 | MtrCurrDax_Amps_f32 |

| MtrElecPol_Cnt_s08 | MtrElecPol_Cnt_s08 | CurrentGainSvc_Cnt_lgc |

| DCPhsBComp_Cnt_u16 | DCPhsBComp_Cnt_u16 |  |

| DCPhsCComp_Cnt_u16 | DCPhsCComp_Cnt_u16 |  |

| DCPhsCComp_Cnt_u16 | DCPhsCComp_Cnt_u16 |  |

| DCPhsBComp_Cnt_u16 | DCPhsBComp_Cnt_u16 |  |

| DCPhsAComp_Cnt_u16 | DCPhsAComp_Cnt_u16 |  |

| DCPhsBComp_Cnt_u16 | DCPhsBComp_Cnt_u16 |  |

| DCPhsBComp_Cnt_u16 | DCPhsBComp_Cnt_u16 |  |

| DCPhsAComp_Cnt_u16 | DCPhsAComp_Cnt_u16 |  |

| DCPhsAComp_Cnt_u16 | DCPhsAComp_Cnt_u16 |  |

| DCPhsCComp_Cnt_u16 | DCPhsCComp_Cnt_u16 |  |

| DCPhsCComp_Cnt_u16 | DCPhsCComp_Cnt_u16 |  |

| DCPhsAComp_Cnt_u16 | DCPhsAComp_Cnt_u16 |  |

|  |  |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| CmMtrCurr_CorrMtrCurr1_Amp_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_CorrMtrCurr2_Amp_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_CurrVectPosition_Rev_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_VectPosCosTheta_Uls_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_VectPosSinTheta_Uls_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_CurrCorrDiag_Amp_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_FiltCurrCorrDiag_Amp_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_ CurrentGainSvc_Cnt_M_lgc | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_BOOLEAN |

| CmMtrCurr_CurrCorrDiagKSV_M_str | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_UNSPECIFIED |

| CurrCorrDiagKSV_M_str.SV_Uls_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_UNSPECIFIED |

| CurrCorrDiagKSV_M_str.K_Uls_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_UNSPECIFIED |

| CmMtrCurr_MtrCurr1LpFltrSV_Volt_M_u3p29 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr2LpFltrSV_Volt_M_u3p29 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_FiltMtrCurr1_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_FiltMtrCurr2_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr1SumHi_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr2SumHi_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr1SumLo_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr2SumLo_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr1SumZero_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr2SumZero_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_VecuSum_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr1OffsetHi_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr2OffsetHi_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr1OffsetLo_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr2OffsetLo_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr1OffsetZero_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr2OffsetZero_Volt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurrValCmd_VoltCnt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr1OffDelta_VoltpVoltCnt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr2OffDelta_VoltpVoltCnt_M_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_CurrOffAvgCounter_Cnt_M_u16 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_16 |

| CmMtrCurr_CurrOffState_Uls_M_enum | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_UNSPECIFIED |

| CmMtrCurr_CurroffProcessFlag_M_enum | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_UNSPECIFIED |

| CmMtrCurr_CurrOffTrimFlag_Cnt_M_lgc | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_BOOLEAN |

| CmMtrCurr_MtrCurr1Offset_Volt_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_MtrCurr2Offset_Volt_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_CorrMtrCurr1_Amp_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| CmMtrCurr_CorrMtrCurr2_Amp_D_f32 | See Data Dictionary | See Data Dictionary | See Data Dictionary | CMMTRCURR_START_SEC_VAR_CLEARED_32 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| CurrTempOffsetType | CurrTempOffsetX_DegC_s10p5 | CurrTempOffsetTblType | -50 | 150 |

|  | CurrOffsetY1_Volts_s4p11 | CurrTempOffsetTblType | -0.026 | 0.026 |

|  | CurrOffsetY2_Volts_s4p11 | CurrTempOffsetTblType | -0.026 | 0.026 |

| PhaseCurrCal_DataType | EOLMtrCurrVcalCmd_VoltCnts_f32 | float | 0 | 80000 |

|  | EOLPhscurr1Gain_AmpspVolt_f32 | float | 20 | 125 |

|  | EOLMtrCurr2OffsetDiff_Volts_f32 | float | 1.0 | 3.0 |

|  | EOLMtrCurr1OffsetDiff_Volts_f32 | float | 1.0 | 3.0 |

|  | EOLMtrCurr1OffsetLo_Volts_f32 | float | 1.0 | 3.0 |

|  | EOLMtrCurr2OffsetLo_Volts_f32 | float | 1.0 | 3.0 |

|  | EOLPhscurr2Gain_AmpspVolt_f32 | float | 20 | 125 |

| CurrTempOffsetTblType[16] |  | Sint16 | Full | Full |

| Constant Name |

| --- |

| k_CurrCorrErrFiltFc_Hz_f32 |

| k_CurrCorrErrThresh_Amps_f32 |

| k_MtrPosComputDelay_Sec_f32 |

| k_MtrCurrEOLMinOffset_Volts_f32 |

| k_MtrCurrEOLMaxOffset_Volts_f32 |

| k_MtrCurrEOLMinGain_AmpspVolts_f32 |

| k_MtrCurrEOLMaxGain_AmpspVolts_f32 |

| k_CurrGainNumerator_Amps_f32 |

| k_MaxCurrOffMtrVel_RadpS_f32 |

| k_CurrOffGainKn_Cnt_u16 |

| k_CurrCorrErrFiltFc_Hz_f32 |

| k_CurrCorrErrThresh_Amps_f32 |

| k_MtrPosComputDelay_Sec_f32 |

|  |

|  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_ADCREF_VOLT_F32 | Single Precision float | Volt | 5.0F |

| D_ADCFULLSCALE_CNT_U16 | 1 | Cnt | 4095U |

| D_SCALERADTOCNTS_ULS_F32 | Single Precision float | Uls | 10430.3783505F |

| D_REVWITHROUND_ULS_F32 | Single Precision float | Uls | 65536.5F |

| D_ROUND_ULS_F32 | Single Precision float | Uls | 0.5F |

|  |  |  |  |

|  |  | VoltspSec |  |

| D_CNVRTP29TOP13_CNT_U16 | 1 | Cnt | 16U |

| D_30DEGREES_CNT_U16 | 1 | Cnt | 5461U |

| D_ONEDIVSQRT3_F32 | Single Precision float | Cnt | 0.57735F |

| D_POSITIVEONE_CNT_S8 | 1 | Cnt | 1 |

| D_CURRDQMAX_AMP_F32 | Single Precision float | Amp |  |

| D_MTRCURROFFHICOMOFF_CNT_U16 | 1 | Cnt | 4000U |

| D_MTRCURROFFLOCOMOFF_CNT_U16 | 1 | Cnt | 500U |

| D_CURROFFNOOFAVG_CNT_U16 | 1 | Cnt | 64U |

| D_MTRCURROFFZEROCOMOFF_CNT_U16 | 1 | Cnt | 0U |

| D_MINVCALCMD_CNT_F32 | Single Precision float | Cnt | 17500.0F |

|  |  |  |  |

|  |  |  |  |

| Constant Name |

| --- |

| D_2PI_ULS_F32 |

| D_FALSE_CNT_LGC |

| D_VECUMIN_VOLTS_F32 |

| D_ZERO_ULS_F32 |

| D_ZERO_CNT_U16 |

| D_ZERO_CNT_U32 |

| D_MTRPOLESDIV2_CNT_U8 |

| D_2MS_SEC_F32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Data | Value |

| --- | --- |

| Rte_InitValue_Vecu_Volt_f32 | 5 |

| Function Name | CmMtrCurrTempOffset_Scom_Get | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | CurrTempOffCal | CurrTempOffsetType * |  |  |  |

| Return Value | void | NA | NA | NA |  |

| Function Name | CmMtrCurrTempOffset_Scom_Set | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | CurrTempOffCal | CurrTempOffsetType * |  |  |  |

| Return Value | void | NA | NA | NA |  |

| Function Name | CmMtrCurr_Scom_CalGain | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None | None |  |  |  |

| Return Value | RetrunValue | Std_ReturnType |  |  |  |

| Function Name | CmMtrCurr_Scom_CalOffset | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None | None |  |  |  |

| Return Value | RetrunValue | Std_ReturnType |  |  |  |

| Function Name | CmMtrCurr_Scom_MtrCurrOffReadStatus | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | CurrOffStatus | MtrCurrOffProcessFlag * |  |  |  |

| Return Value | void | NA | NA | NA |  |

| Function Name | CmMtrCurr_Scom_ReadMtrCurrCals | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | ShCurrCalPtr | PhaseCurrCal_DataType  * |  |  |  |

| Return Value | void | NA | NA | NA |  |

| Function Name | CmMtrCurr_Scom_SetMtrCurrCals | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | ShCurrCalPtr | PhaseCurrCal_DataType  * |  |  |  |

| Return Value | void | NA | NA | NA |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| CmMtrCurr_Init | On Init | Init |

| CmMtrCurr_Per1 | 100ms | All |

| CmMtrCurr_Per2 | 2ms | Operate |

| CmMtrCurr_Per3 | 2ms | Operate |

| CurrDQPer1 | 125us (MtrCtrl ISR) | All |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| CmMtrCurr_Scom_CalGain |  |

| CmMtrCurr_Scom_CalOffset |  |

| CmMtrCurr_Scom_MtrCurrOffReadStatus |  |

| CmMtrCurr_Scom_ReadMtrCurrCals |  |

| CmMtrCurr_Scom_SetMtrCurrCals |  |

| CmMtrCurrTempOffset_Scom_Get |  |

| CmMtrCurrTempOffset_Scom_Set |  |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| CmMtrCurr_Init | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| CmMtrCurr_Per1 | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| CmMtrCurr_Per2 | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| CmMtrCurr_Per3 | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| CurrDQPer1 |  |

| CmMtrCurr_Scom_CalGain | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| CmMtrCurr_Scom_CalOffset | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| CmMtrCurr_Scom_MtrCurrOffReadStatus | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| CmMtrCurr_Scom_ReadMtrCurrCals | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| CmMtrCurr_Scom_SetMtrCurrCals | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| CmMtrCurrTempOffset_Scom_Get | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| CmMtrCurrTempOffset_Scom_Set | RTE_START_SEC_SA_CMMTRCURR_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1.0 | Initial Version (FDD 01 C Ver 005) | 01-Dec-12 | Selva |

| 2.0 | Configured global read/write macros for global data (anomaly 4696) | 23-Mar-13 | OT |

| 3.0 | Fixes for Anamoly 5561 and A5566 added | 4-Sep-13 | Selva |

| 4.0 | Updated to FDD 01C Ver 006 | 07-Oct-13 | VK |

| 5.0 | Anomaly 5967 and 5873 | 06-Nov-13 | SP |

| 6.0 | Range corrections for ‘MtrCurr1OffDelta_VoltpVoltCnts_M_f32’ and ‘MtrCurr2OffDelta_VoltpVoltCnts_M_f32’ | 9-Nov-13 | SR |

| 7.0 | Changed CurrCorrDiag filtering from fixed point to floating point to achieve specified range and resolution – CR 10895 | 20-Nov-13 | KMC |

| 8.0 | Updated for FDD 01C v007 | 20-Apr-14 | Selva |

|  |  |  |  |
