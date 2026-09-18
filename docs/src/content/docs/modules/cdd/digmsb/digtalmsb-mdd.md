---
title: 'DigtalMSB MDD'
description: 'Converted design document: DigtalMSB MDD'
---

> **Source:** `DigMSB/doc/DigtalMSB_MDD.docx`  
> **Module:** [DigMSB](../../../../cdd/digmsb/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module – `

## High-Level Description

The data synchronsiation  between Motor Control ISR and 2 ms Task will be provided at the integration level. But the synchronization between 2 and 100ms is provided by the Module level variable by disabling and enabling interrupts.

Note:  Some variables are used as both input and output.  For the those outputs use the ranges from inputs.

## Figures

### Component Diagram

## Variable Data Dictionary

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

### Module Internal Variables

This section identifies the name, range and resolutions for module specific data created by this module.  If there are no range restrictions on the variable, the term “FULL” is placed into the table for legal range.

#### User defined typedef definition/declaration

This section documents any user types uniquely used for the module.

(Refer the included ref for more details of register)

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

FPM_FixedToFloat_m()

Abs_f32_m()

Rte_Call_NxtrDiagMgr_SetNTCStatus

FPM_Fix_m

DiagNStep_m

DiagPStep_m

DiagFailed_m

### Data Hiding Functions

- MSB1GetData()

- MSB1SetData()

- MSB2GetData()

- MSB2SetData()

- MSB1EnableDataTransfer()

- MSB2EnableDataTransfer()

- MSB1EnableConfigTransfer()

- MSB2EnableConfigTransfer()

### Global Functions/Macros Defined by this Module

#### Global Function #1

##### Description

##### Store Module Inputs to Local copies

##### Store Local copy of outputs into Module Outputs

DigMSB_Write_UncorrMechMtrPos1_Rev_u0p16(DigMSB_MechMtrPos1UnCorrec_Rev_M_u0p16)

DigMSB_Write_CumMechMtrPos_Rev_s15p16(DigMSB_CumMtrPos1MRF_Rev_M_s15p16)

DigMSB_Write_MechMtrPos1_Rev_u0p16(MechMtrPos1_Rev_T_u0p16)

DigMSB_Write_SysCMechMtrPos1_Rev_u0p16(MechMtrPos1_Rev_T_u0p16)

DigMSB_Write_CorrectedElecMtrPos_Rev_u0p16(CorrectedElecMtrPos_Rev_T_u0p16)

DigMSB_Write_SysCorrectedElecMtrPos_Rev_u0p16(CorrectedElecMtrPos_Rev_T_u0p16)

DigMSB_Write_MechMtrPos1TimeStamp_uSec_u32(SampleTime1_uSec_T_u32)

DigMSB_Write_MechMtrPos2TimeStamp_uSec_u32(SampleTime1_uSec_T_u32)

DigMSB_Write_RxMtrPos1ParityAccum_Cnt_u16(DigMSB_RxMtrPos1ParityAccum_Cnt_M_u16)

DigMSB_Write_Die1RxError_Cnt_u16((MSB1RxData_Cnt_T_u16[0]))

DigMSB_Write_Die1RxRevCtr_Cnt_u16((MSB1RxData_Cnt_T_u16[1]))

DigMSB_Write_Die1RxMtrPos_Cnt_u16((MSB1RxData_Cnt_T_u16[2]))

DigMSB_Write_Die2RxError_Cnt_u16((MSB2RxData_Cnt_T_u16[0]))

DigMSB_Write_Die2RxRevCtr_Cnt_u16((MSB2RxData_Cnt_T_u16[1]))

DigMSB_Write_Die2RxMtrPos_Cnt_u16((MSB2RxData_Cnt_T_u16[2]))

### Local Functions/Macros Used by this MDD only

#### Local Marco #1

#### Local Function #1

Processing:

##### Store Module Inputs to Local copies

See section below

##### Description

##### Store Local copy of outputs into Module Outputs

See section above

#### Local Function #2

##### Store Module Inputs to Local copies

See section below

##### Description

##### Store Local copy of outputs into Module Outputs

See section above

#### Local Function #3

##### Store Module Inputs to Local copies

See section below

##### Description

##### Store Local copy of outputs into Module Outputs

See section above

#### Data Hiding Macro #1

None

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init: DigMSB_Init

##### Design Rationale

ISO Fault Debounce Counters are implemented by taking midpoint of range of  twice the threshold to avoid  the  Signed implementation.

##### Initialize the Transmit data buffer with the value Module Outputs

None

##### Module Internal

## Periodic Functions

#### Per: _Per2

##### Design Rationale

FDD specifies the precision of p13 for Motor Position, Cumulative Motor Position, Aligned Cumulative Motor Position. But in the implementation p13 is converted to p16. This is done to avoid rollover math and match the output port data types.

##### Program Flow Start

Rte_Call_DigMSB_Per2_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

UncorrMechMtrPos1_Rev_T_u0p16 = Rte_IRead_DigMSB_Per2_UncorrMechMtrPos1_Rev_u0p16()

Die2RxError_Cnt_T_u16 = Rte_IRead_DigMSB_Per2_Die2RxError_Cnt_u16()

Die2RxRevCtr_Cnt_T_u16 = Rte_IRead_DigMSB_Per2_Die2RxRevCtr_Cnt_u16()

Die2RxMtrPos_Cnt_T_u16 = Rte_IRead_DigMSB_Per2_Die2RxMtrPos_Cnt_u16()

Die1RxError_Cnt_T_u16 = Rte_IRead_DigMSB_Per2_Die1RxError_Cnt_u16()

Die1RxRevCtr_Cnt_T_u16 = Rte_IRead_DigMSB_Per2_Die1RxRevCtr_Cnt_u16()

CumMechMtrPosMRF_Rev_T_f32 = Rte_IRead_DigMSB_Per2_CumMechMtrPos_Rev_f32()

RxMtrPosParityAccum_Cnt_T_u16 = Rte_IRead_DigMSB_Per2_RxMtrPosParityAccum_Cnt_u16()

AssistAssemblyPolarity_Cnt_T_s08 = Rte_IRead_DigMSB_Per2_AssistAssemblyPolarity_Cnt_s08()

MtrPosPolarity_Cnt_T_s08 =  Rte_IRead_DigMSB_Per2_MtrPosPolarity_Cnt_s08()

CorrectedElecMtrPos_Rev_T_u0p16 =  Rte_IRead_DigMSB_Per2_CorrectedElecMtrPos_Rev_u0p16()

##### Store Local copy of outputs into Module Outputs

Rte_IWrite_DigMSB_Per2_AlignedCumMechMtrPosCRF_Deg_f32(AlignedCumMechMtrPos1CRF_Deg_T_f32)

Rte_IWrite_DigMSB_Per2_AlignedCumMechMtrPosMRF_Deg_f32(AlignedCumMechMtrPos1MRF_Deg_T_f32)

Rte_IWrite_DigMSB_Per2_CumMechMtrPosCRF_Deg_f32(CumMechMtrPosCRF_Deg_T_f32)

Rte_IWrite_DigMSB_Per2_CumMechMtrPosMRF_Deg_f32(CumMechMtrPosMRF_Deg_T_f32)

Rte_IWrite_DigMSB_Per2_MechMtrPos2_Rev_u0p16(MechMtrPos2_Rev_T_u0p16)

Rte_IWrite_DigMSB_Per2_SysCCumMechMtrPosMRF_Deg_f32(CumMechMtrPosMRF_Deg_T_f32)

Rte_IWrite_DigMSB_Per2_AlignedCumMechMtrPosStatus_Cnt_u08(DigMSB_AlignedCumMechMtrPosStatus_Cnt_M_u08)

##### Rte_IWrite_DigMSB_Per2_CumMechMtrPosStatus_Cnt_u08(DigMSB_CumMechMtrPosStatus_Cnt_M_u08)

##### Program Flow End

Rte_Call_DigMSB_Per2_CP1_CheckpointReached()

#### Per: _Per3

##### Design Rationale

None

##### Store Module Inputs to Local copies

None

##### Program Flow Start

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

None

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

None

### Known Issues / Limitations With Design

INLINE functions defined in GlobalMacro.h are not unit tested.

The variables are not range limited in Motor Control ISR. If the ranges need to be limited, it should be limited at slower time loop.The ranges of Aligned Cumulative and Cumulative Motor Position values are not limited as it used in MtrVel Diagnostics.Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| UncorrMechMtrPos1_Rev_u0p16 | UncorrMechMtrPos1_Rev_u0p16 | UncorrMechMtrPos1_Rev_u0p16 |

| Die2RxError_Cnt_u16 | Die2RxError_Cnt_u16 | Die2RxError_Cnt_u16 |

| Die2RxRevCtr_Cnt_u16 | Die2RxRevCtr_Cnt_u16 | Die2RxRevCtr_Cnt_u16 |

| Die2RxMtrPos_Cnt_u16 | Die2RxMtrPos_Cnt_u16 | Die2RxMtrPos_Cnt_u16 |

| Die1RxError_Cnt_u16 | Die1RxError_Cnt_u16 | Die1RxError_Cnt_u16 |

| Die1RxRevCtr_Cnt_u16 | Die1RxRevCtr_Cnt_u16 | Die1RxRevCtr_Cnt_u16 |

| CumMechMtrPos_Rev_f32 | CumMechMtrPos_Rev_f32 | AlignedCumMechMtrPosCRF_Deg_f32 |

| RxMtrPosParityAccum_Cnt_u16 | RxMtrPosParityAccum_Cnt_u16 | CumMechMtrPosCRF_Deg_f32 |

| MtrPosPolarity_Cnt_s08 | MtrPosPolarity_Cnt_s08 | CumMechMtrPosMRF_Deg_f32 |

| EnergyModeState_Cnt_enum | EnergyModeState_Cnt_enum | MechMtrPos2_Rev_u0p16 |

| CorrectedElecMtrPos_Rev_u0p16 | CorrectedElecMtrPos_Rev_u0p16 | SysCCumMechMtrPosMRF_Deg_f32 |

| UncorrMechMtrPos1_Rev_u0p16 | UncorrMechMtrPos1_Rev_u0p16 | AlignedCumMechMtrPosStatus_Cnt_u08 |

| Die1RxError_Cnt_u16 | Die1RxError_Cnt_u16 | MechMtrPos1_Rev_u0p16 |

| Die1RxRevCtr_Cnt_u16 | Die1RxRevCtr_Cnt_u16 | SysCMechMtrPos1_Rev_u0p16 |

| Die2RxRevCtr_Cnt_u16 | Die2RxRevCtr_Cnt_u16 | SysCorrectedElecMtrPos_Rev_u0p16 |

| Die2RxMtrPos_Cnt_u16 | Die2RxMtrPos_Cnt_u16 | MechMtrPos1TimeStamp_uSec_u32 |

|  |  | MechMtrPos2TimeStamp_uSec_u32 |

|  |  | CorrectedElecMtrPos_Rev_u0p16 |

|  |  | UncorrMechMtrPos1_Rev_u0p16 |

|  |  | CumMechMtrPos_Rev_s15p16 |

|  |  | Die1RxError_Cnt_u16 |

|  |  | Die1RxRevCtr_Cnt_u16 |

|  |  | Die2RxRevCtr_Cnt_u16 |

|  |  | Die1RxMtrPos_Cnt_u16 |

|  |  | Die2RxMtrPos_Cnt_u16 |

|  |  | RxMtrPos1ParityAccum_Cnt_u16 |

|  |  |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| DigMSB_PWMGrpData_Cnt_M_u16[3] | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_AsyncConfigGrpDie1_Cnt_M_u16[3] | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_AsyncConfigGrpDie2_Cnt_M_u16[3] | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_MechMtrPos1UnCorrec_Rev_M_u0p16 | 1.52588E-05 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_RxMtrPos1ParityAccum_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die1R0ParityFault_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die1R1ParityFault_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die2R2ParityFault_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die1ErrorOkAcc_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die2ErrorOkAcc_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_MechMtrPos2UnCorrec_Rev_M_u0p16 | 1.52588E-05 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die1vsDie2TrnsCntrAcc_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_ErrorRegTCAcc_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_ErrorRegVehMaskAcc_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_MtrPosErrAcc_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_PrevMechMtrPos1_Rev_M_u0p16 | 1.52588E-05 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die2RevCntr_Cnt_M_s16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die1RevCntr_Cnt_M_s16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die1R2ParityFault_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die2R1ParityFault_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_Die2R0ParityFault_Cnt_M_u16 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_16 |

| DigMSB_AlignedCumMechMtrPos2CRF_Deg_D_f32 | Single precision float | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_32 |

| DigMSB_AlignedCumMechMtrPos2MRF_Deg_D_f32 | Single preision float | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_32 |

| DigMSB_CumMtrPos1MRF_Rev_M_s15p16 | 1.52588E-05 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_32 |

| DigMSB_AlignedCumMechMtrPos1_Rev_M_s15p16 | 1.52588E-05 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_32 |

| DigMSB_AlignedCumMechMtrPos2_Rev_M_s15p16 | 1.52588E-05 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_32 |

| DigMSB_PrevAlignedCumMechMtrPos2_Rev_M_s15p16 | 1.52588E-05 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_32 |

| DigMSB_PrevAlignedCumMechMtrPos1_Rev_M_s15p16 | 1.52588E-05 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_32 |

| DigMSB_ResetTC_Cnt_M_lgc | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_BOOLEAN |

| DigMSB_ResetIC_Cnt_M_lgc | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_BOOLEAN |

| DigMSB_Die1ErrorOkAccPassed_Cnt_M_lgc | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_BOOLEAN |

| DigMSB_Die2ErrorOkAccPassed_Cnt_M_lgc | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_BOOLEAN |

| DigMSB_EnableAsyncConfigGrp_Cnt_M_lgc | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_BOOLEAN |

| DigMSB_AlignedCumMtrPos2Init_Cnt_M_lgc | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_BOOLEAN |

| DigMSB_AlignedCumMtrPos1Init_Cnt_M_lgc | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_BOOLEAN |

| DigMSB_Die2Errorflag_Cnt_M_u08 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_8 |

| DigMSB_Die1Errorflag_Cnt_M_u08 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_8 |

| DigMSB_CumMechMtrPosStatus_Cnt_M_u08 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_8 |

| DigMSB_AlignedCumMechMtrPosStatus_Cnt_M_u08 | 1 | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_8 |

| DigMSB_Die1ErrorOk_Cnt_M_enum | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_UNSPECIFIED |

| DigMSB_Die2ErrorOk_Cnt_M_enum | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_UNSPECIFIED |

| DigMSB_Die1vsDie2TrnsCntrAcc_Cnt_M_enum | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_UNSPECIFIED |

| DigMSB_MtrPosErrAcc_Cnt_M_enum | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_UNSPECIFIED |

| DigMSB_ErrorRegTC_Cnt_M_enum | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_UNSPECIFIED |

| DigMSB_ErrorRegVehMask_Cnt_M_enum | N/A | See Data Dictionary | See Data Dictionary | DIGMSB_START_SEC_VAR_CLEARED_UNSPECIFIED |

|  |  |  |  |  |

|  |  |  |  |  |

|  |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| NTCStateType_Enum | NTCSTATE_INVALID | enum | 0u | 0u |

| NTCStateType_Enum | NTCSTATE_FAILED | enum | 1u | 1u |

| NTCStateType_Enum | NTCSTATE_PASSED | enum | 2u | 2u |

| EnergyModeStateType | NORMAL | enum | 0 | 0 |

| EnergyModeStateType | PRODUCTION | enum | 1 | 1 |

| EnergyModeStateType | TRANSPORTATION | enum | 2 | 2 |

| EnergyModeStateType | FLASH | enum | 3 | 3 |

| DigMSBEOLType | MtrPosBEMF_Rev_u0p16 | UInt16 | 0 | full |

| DigMSBEOLType | MtrPosBEMFRedundant_Rev_u0p16 | UInt16 | 0 | full |

| DigMSBEOLType | MtrPos1HarCompTbl_Rev_s2p13[3] | SInt16 | full | full |

| DigMSBEOLType | MtrPos2HarCompTbl_Rev_s2p13[3] | SInt16 | full | full |

| Calibration Constants |

| --- |

| k_Die1vsDie2TrnsCntrThresh_Deg_f32 |

| k_Die2Offset_Rev_u3p13 |

| k_MtrPos1vsMtrPos2Thresh_Rev_u3p13 |

| k_DigMSBErrorRegGenMask_Cnt_u08 |

| k_ErrorRegTCMask_Cnt_u08 |

| k_ErrorRegVehMask_Cnt_u08 |

| k_TurnsCntrOffset_Rev_f32 |

| k_Die1RPMMode_Cnt_u08 |

| k_Die2RPMMode_Cnt_u08 |

| k_DigMSBParity_Cnt_str |

| k_DigMSBTCRunTimeParity_Cnt_str |

| k_ErrorRegTCAcc_Cnt_str |

| k_MtrPos1vsMtrPos2Diag_Cnt_str |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_PIREVQUATER_REV_S15P16 | 1 | Rev | (FPM_InitFixedPoint_m( 0.25, s15p16_T)) |

| D_PIREVQUATER_REV_U16 | 1 | Rev | (FPM_InitFixedPoint_m( 0.25, u0p16_T)) |

| D_MASK16BITS_CNT_U16 | 1 | Cnt | 0xFFFFu |

| D_HALFREV_REV_U0P16 | 1 | Rev | 32768U |

| D_REVTODEG_DEG_F32 | 1 | Deg | 360.0F |

| D_PWMGRPWRD0_CNT_U16 | 1 | Cnt | 0x200U |

| D_PWMGRPWRD1_CNT_U16 | 1 | Cnt | 0U |

| D_PWMGRPWRD2_CNT_U16 | 1 | Cnt | 0x400U |

| D_ASYNCCONFIGGRPWRD0_CNT_U16 | 1 | Cnt | 0x8800U |

| D_ASYNCCONFIGGRPWRD1_CNT_U16 | 1 | Cnt | 0x800U |

| D_ASYNCCONFIGGRPWRD2_CNT_U16 | 1 | Cnt | 0x400U |

| D_INITCUMPOS_REV_S15P16 | 1 | Rev | 78643200 |

| Constant Name | Value |

| --- | --- |

| D_ONE_ULS_F32 | 1 |

| D_ZERO_ULS_F32 | 0 |

| D_NEGONE_CNT_S16 | -1 |

| D_ONE_CNT_S16 | 1 |

| D_ZERO_CNT_S16 | 0 |

| D_NEGONE_CNT_S32 | -1 |

| D_ONE_CNT_S32 | 1 |

| D_ZERO_CNT_S32 | 0 |

| D_NEGONE_CNT_S8 | -1 |

| D_ONE_CNT_S8 | 1 |

| D_ZERO_CNT_S8 | 0 |

| D_ONE_CNT_U16 | 1u |

| D_ZERO_CNT_U16 | 0u |

| D_ONE_CNT_U32 | 1u |

| D_ZERO_CNT_U32 | 0u |

| D_ONE_CNT_U8 | 1u |

| D_ZERO_CNT_U8 | 0u |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| T_PARITYTABLE_CNT_U8 | Uint8 | { 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U, 1U, 0U, 0U, 1U, 1U, 0U, 0U, 1U, 0U, 1U, 1U, 0U} | DIGMSB_START_SEC_CONST_8 |

| Function Name | DigMSB_Per1 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | None |  |  |  |  |

| Function Name | ParityCalculation_m | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | data | Uint16 | 0 | 65535 |  |

|  |  |  |  |  |  |

| Return Value | Output | Uint16 | 0 | 1 |  |

| Function Name | MtrPosProcessing | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | RxData_Cnt_T_u16 | Uint16 | 0 | 65535 |  |

|  | *DiexRx2Parity_Cnt_T_u08 | Uint8 | 0 | 1 |  |

|  |  |  |  |  |  |

| Return Value | MechMtrPos_Rev_T_u0p16 | Uint16 | 0 | 1 |  |

| Function Name | RevCntrProcessing | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | RxData_Cnt_T_u16 | Uint16 | 0 | 65535 |  |

|  | *DiexRx1Parity_Cnt_T_u08 | Uint8 | 0 | 1 |  |

| Return Value | DiexRevCntr_Cnt_T_s16 | Sint16 | -512 | 511 |  |

| Function Name | ErrorRegisterProcessing | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | RxData_Cnt_T_u16 | Uint16 | 0 | 65535 |  |

|  | DiexRx0Parity_Cnt_T_u08 | Uint8 | 0 | 1 |  |

| Return Value | DiexErrorFlag_Cnt_T_u08 | Uint8 | 0 | 31 |  |

| Data | Value |

| --- | --- |

|  |  |

|  |  |

|  |  |

|  |  |

|  |  |

|  |  |

|  |  |

|  |  |

|  |  |

|  |  |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0,2.0, | Initial Version | 12-Jun-13 | Selva |

| 2 | 3.0 | Corrected the Delta Motor Pos Calculation by replacing  0.5f  with 1f | 1-Aug-13 | Selva |

| 3 | 4.0,5.0 | Fixed Rx buffer position, Parity Calculation updated names to match standards | 8-Aug-13 | Selva |

| 6 | 6.0 | Corrected the synchronization issues between 2 and 100 ms task | 28-Aug-13 | Selva |

| 7 | 7.0 | Updated per FDD v3 | 11-Sep-13 | LWW |

| 8 | 8.0 | Anomaly 5611 correction | 12-Sep-13 | LWW |

| 9 | 9.0 | Anomaly 5640 correction, Updated “TurnsCntrValidity” state flow | 23-Sep-13 | Selva |

| 10 | 10.0 | FDD v4 update and Unit fix (anomaly 6172) | 7-April-14 | KPIT-SK |

| 11 | 11.0 | Prototype of new multiple transfer group SPI transfers (v5 Prerelease) and also A5929 fixed. | 8-April-14 | Selva |

| 12 | 12.0 | Updated for FDD v6 | 28-Apr-14 | Selva |

| 13 | 13.0 | Updated for 6811, 6831 | 30-May-14 | Selva |

| 14 | 14.0 | Updated Sections 5.1,5.3.1.2,7.1.1,7.1.2.3,6.2.1.3,6.2.1.3, 5.4.2 and 5.4.3, 5.4.4 | 19-Sep-14 | KPIT-SSK |

| 15 | 15.0 | Anomaly 6855 ,6864 correction | 8-Dec-14 | TATA-JK |

|  |  |  |  |  |
