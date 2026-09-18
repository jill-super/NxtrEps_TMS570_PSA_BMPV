---
title: 'Diagnostics Manager Core MDD'
description: 'Converted design document: Diagnostics Manager Core MDD'
---

> **Source:** `DiagMgr/doc/Diagnostics_Manager_Core_MDD.docx`  
> **Module:** [DiagMgr](../../../../services/diagmgr/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module -- Diagnostics Manager Core

## High-Level Description

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

Note: “ Refer *” -  Refer to Diagnostics_Manager_GeneratedCfg_MDD

Note Size and elements of Table constants varies across projects. Check project configuration files Under UTP/ Contract folder for data.

## Functions/Macros used by the Sub-Modules

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules are identified below,

TableSize_m()

### Data Hiding Functions

<None>

### Function Mapping

- DiagMgr_ReportDet(errorId) ↔  Det_ReportError(0,0,0,errorId)

### Global Functions/Macros Defined by this Module

#### Diagnostic Manager Initialization

Note: *doc in below table is Diagnostics_Manager_GeneratedCfg_MDD

##### Description

#### Diagnostic Manager Periodic Code

Note: *doc in below table is Diagnostics_Manager_GeneratedCfg_MDD

##### Description

#### Diagnostic Manager Transition Core

Note: *doc in below table is Diagnostics_Manager_GeneratedCfg_MDD

##### Description

#### Diagnostic Manager Get NTC Failed

##### Description

#### Diagnostic Manager Get NTC Active

##### Description

#### Diagnostic Manager Get NTC Status

##### Description

#### Diagnostic Manager Set NTC Status

Note: *doc in below table is Diagnostics_Manager_GeneratedCfg_MDD

##### Description

#### Diagnostic Manager Report NTC Status

Note: *doc in below table is Diagnostics_Manager_GeneratedCfg_MDD

##### Description

### Local Functions/Macros Used by this MDD only

#### Set Bits

##### Description

*Data |= BitMask

#### Clear Bits

##### Description

*Data &= ~BitMask

#### Read Bit

##### Description

IF 0 = (Data & BitMask) THEN

return FALSE

ELSE

return TRUE

ENDIF

#### Set Bits

##### Description

*Data |= BitMask

#### Read Bit

##### Description

IF 0 = (Data & BitMask) THEN

return FALSE

ELSE

return TRUE

ENDIF

#### Process Diagnostic Status

##### Description

#### Process Ramp Response

##### Description

#### Failed Check and Processing

##### Description

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

### Initialization Functions

None

### Periodic Functions

None

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

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

### Global and Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

(Item #1)

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| MEC_Cnt_enum | MEC_Cnt_enum |  |

| MfgDiagInhibit_Cnt_lgc | MfgDiagInhibit_Cnt_lgc |  |

| SystemState_Mode | SystemState_Mode |  |

| Variable Name | Datatype | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Multiplicity | Software Segment<br/>{Data Type} |

| --- | --- | --- | --- | --- | --- | --- |

| NTCStrgArray_Cnt_str | NTCStrgArray | N/A | N/A | N/A | 1:1 | DIAGMGR_START_SEC_VAR_SAVED_ZONEH_UNSPECIFIED |

| NTCBlackBoxData_Cnt_str | NTCBlkBoxData | N/A | N/A | N/A | 1:1 | DIAGMGR_START_SEC_VAR_SAVED_ZONEH_UNSPECIFIED |

| DEMEventActive_Cnt_M_lgc[D_NUMOFDEMEVENTS_CNT_U08+1] | Boolean | N/A | FALSE | TRUE | 1:1 | DIAGMGR_START_SEC_VAR_CLEARED_BOOLEAN |

| ResetNTCFlag_Cnt_M_u08 | Refer * | Refer * | Refer * | Refer * | Refer * | Refer * |

| DiagMgr_NTCInfo#_Cnt_M_str | Refer * | Refer * | Refer * | Refer * | Refer * | Refer * |

|  |  |  |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| NTCStrgArray |  | NTCStrg |  |  |

| NTCBlkBoxData |  | NTCBlkBoxType |  |  |

| typedef struct { } NTCBlkBoxType | NTC_Cnt_u08 | Uint8 | 1 | FULL |

| typedef struct { } NTCBlkBoxType | Param_Cnt_u08 | Uint8 | 0 | FULL |

| typedef struct { } NTCBlkBoxType | SystemState_Cnt_u08 | Uint8 | 0 | 4 |

| typedef struct { } NTCBlkBoxType | VehSpd_Kph_u8p0 | Uint8 | 0 | FULL |

| typedef struct { } NTCBlkBoxType | BlkBoxCfgData1 | Uint32 | 0 | FULL |

| typedef struct { } NTCBlkBoxType | BlkBoxCfgData2 | Uint32 | 0 | FULL |

| typedef struct { } NTCBlkBoxType | BlkBoxCfgData3 | Uint32 | 0 | FULL |

| typedef struct { } NTCBlkBoxType | HwTrq_HwNm_s4p11 | Sint16 | -10 | 10 |

| typedef struct { } NTCBlkBoxType | MtrTrq_MtrNm_s4p11 | Sint16 | -8.8 | 8.8 |

| typedef struct { } NTCBlkBoxType | IgnCtr_Cnt_u16 | Uint16 | 0 | FULL |

| typedef struct { } NTCStrg | NTC | NTCNumber | 0 | 511 |

| typedef struct { } NTCStrg | Status | uint8 | 0 | FULL |

| typedef struct { } NTCStrg | AgingCounter | uint8 | 0 | FULL |

| typedef struct { } NTCStrg | Status | uint8 | 0 | FULL |

| typedef struct { } NTCStrg | AgingCounter | uint8 | 0 | FULL |

|  |  |  |  |  |

|  |  |  |  |  |

|  |  |  |  |  |

| Constant Name |

| --- |

| k_FltRspTbl_Cnt_str[] |

| k_FltRmpRate_UlspmS_f32[] |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_FLTRSPNTCACTIVEBIT_CNT_B32 | N/A | Counts | 0x00800000 |

| D_FLTRSPRECOVERABLEBIT_CNT_B32 | N/A | Counts | 0x00400000 |

| D_FLTRSPHWASBSYSTMFLTBIT_CNT_B32 | N/A | Counts | 0x00200000 |

| D_FLTRSPDEFVEHSPDBIT_CNT_B32 | N/A | Counts | 0x00100000 |

| D_FLTRSPDEFTEMPBIT_CNT_B32 | N/A | Counts | 0x00080000 |

| D_FLTRSPSCOMHWANOTVALIDBIT_CNT_B32 | N/A | Counts | 0x00040000 |

| D_FLTRSPWIRDISABLEBIT_CNT_B32 | N/A | Counts | 0x00008000 |

| D_FLTRSPPWRCYCLTCHBIT_CNT_B32 | N/A | Counts | 0x00000010 |

| D_FLTRSPNTCINHIBITNOTOPERATEBIT_CNT_B32 | N/A | Counts | 0x00000020 |

| D_FLTRSPNTCINHIBITRUNBIT_CNT_B32 | N/A | Counts | 0x00000040 |

| D_FLTRSPRAMPBITS_CNT_B32 | N/A | Counts | 0x0000000F |

| D_FLTRSPBLKBOXBITS_CNT_B32 | N/A | Counts | 0x00003800 |

| D_BLKBOXBITOFFSET_CNT_U08 | N/A | Counts | 11 |

| D_RAMPNONE_CNT_U8 | 1 | Counts | 0x0F |

| D_RAMPF2_CNT_U8 | 1 | Counts | 0x0E |

| D_RAMPF1_CNT_U8 | 1 | Counts | 0x0D |

|  |  |  |  |

| D_DIAGRMPRTLOLMT_ULSPMS_F32 | Single precision float | Uls/mS | 0.0001 |

| D_DIAGRMPRTHILMT_ULSPMS_F32 | Single precision float | Uls/mS | 0.5 |

| Constant Name |

| --- |

|  |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| T_NTCMapTbl#_Cnt_enum[SIZE] | N/A | Refer * | AP_DIAGMGR_CONST |

| T_DiagMgrNtcAppInfoMap_Cnt_Str[SIZE] | N/A | Refer * | AP_DIAGMGR_CONST |

| T_DiagMgrNtcInfoPtr_Cnt_Str[SIZE] | N/A | Refer * | AP_DIAGMGR_CONST |

| Function Name | DiagMgr_Init_Core | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTCInfo_Cnt_T_str[SIZE] | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc |

|  | NumElements_Cnt_T_u08 | Refer Range of DIAGMGR_EVENTNUM_# in *doc | Refer Range of DIAGMGR_EVENTNUM_# in *doc | Refer Range of DIAGMGR_EVENTNUM_# in *doc |

|  | CurrentAppIdx_Cnt_T_u08 | Refer Range of DIAGMGR_APID_# in *doc | Refer Range of DIAGMGR_APID_# in *doc | Refer Range of DIAGMGR_APID_# in *doc |

|  | DiagMgrInitComp_Ptr_T_lgc | Refer Range of DiagMgrInitComp#_Cnt_M_lgc | Refer Range of DiagMgrInitComp#_Cnt_M_lgc | Refer Range of DiagMgrInitComp#_Cnt_M_lgc |

|  | NTCInfoQueue_Cnt_T_str[5] | Refer Range of NTCInfoQueue#_Cnt_M_str[SIZE] in *doc | Refer Range of NTCInfoQueue#_Cnt_M_str[SIZE] in *doc | Refer Range of NTCInfoQueue#_Cnt_M_str[SIZE] in *doc |

|  | NTCQueueIndex_Ptr_T_u08 | Refer Range of NTCQueueIndex#_Cnt_M_u08 in *doc | Refer Range of NTCQueueIndex#_Cnt_M_u08 in *doc | Refer Range of NTCQueueIndex#_Cnt_M_u08 in *doc |

|  | DiagSts_Cnt_T_b16[SIZE] | Refer Range of DiagSts#_Cnt_M_b16[SIZE] in *doc | Refer Range of DiagSts#_Cnt_M_b16[SIZE] in *doc | Refer Range of DiagSts#_Cnt_M_b16[SIZE] in *doc |

|  | ActiveRmpRate_UlspmS_T_f32[SIZE] | Refer Range of ActiveRmpRate#_UlspmS_M_f32[SIZE] in *doc | Refer Range of ActiveRmpRate#_UlspmS_M_f32[SIZE] in *doc | Refer Range of ActiveRmpRate#_UlspmS_M_f32[SIZE] in *doc |

|  | ActDiagSts_Ptr_T_u08 | Refer Range of ActDiagSts#_Cnt_M_u08 in *doc | Refer Range of ActDiagSts#_Cnt_M_u08 in *doc | Refer Range of ActDiagSts#_Cnt_M_u08 in *doc |

| Return Value | none |  |  |  |

| Function Name | DiagMgr_Per_Core | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTCInfo_Cnt_T_str[SIZE] | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc |

|  | NumElements_Cnt_T_u08 | Refer Range of DIAGMGR_EVENTNUM_# in *doc | Refer Range of DIAGMGR_EVENTNUM_# in *doc | Refer Range of DIAGMGR_EVENTNUM_# in *doc |

|  | DiagSts_Cnt_T_b16[SIZE] | Refer Range of DiagSts#_Cnt_M_b16[SIZE] in *doc | Refer Range of DiagSts#_Cnt_M_b16[SIZE] in *doc | Refer Range of DiagSts#_Cnt_M_b16[SIZE] in *doc |

|  | ActiveRmpRate_UlspmS_T_f32[SIZE] | Refer Range of ActiveRmpRate#_UlspmS_M_f32[SIZE] in *doc | Refer Range of ActiveRmpRate#_UlspmS_M_f32[SIZE] in *doc | Refer Range of ActiveRmpRate#_UlspmS_M_f32[SIZE] in *doc |

|  | ActDiagStsIdx_Ptr_T_u08 | Refer Range of ActDiagSts#_Cnt_M_u08 in *doc | Refer Range of ActDiagSts#_Cnt_M_u08 in *doc | Refer Range of ActDiagSts#_Cnt_M_u08 in *doc |

|  | T_NTCMapTbl_Cnt_enum[SIZE] | Refer range of T_NTCMapTbl#_Cnt_enum[SIZE] in *doc | Refer range of T_NTCMapTbl#_Cnt_enum[SIZE] in *doc | Refer range of T_NTCMapTbl#_Cnt_enum[SIZE] in *doc |

|  | PrevResetNTCFlag_Ptr_T_u08 | Refer Range of ResetNTCFlag#_Cnt_M_u08 in *doc | Refer Range of ResetNTCFlag#_Cnt_M_u08 in *doc | Refer Range of ResetNTCFlag#_Cnt_M_u08 in *doc |

| Return Value | none |  |  |  |

| Function Name | DiagMgr_Trns_Core | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTCInfo_Cnt_T_str[SIZE] | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc |

|  | NumElements_Cnt_T_u08 | Refer Range of DIAGMGR_EVENTNUM_# in *doc | Refer Range of DIAGMGR_EVENTNUM_# in *doc | Refer Range of DIAGMGR_EVENTNUM_# in *doc |

|  | T_NTCMapTbl_Cnt_enum[79] | Refer range of T_NTCMapTbl#_Cnt_enum[SIZE] in *doc | Refer range of T_NTCMapTbl#_Cnt_enum[SIZE] in *doc | Refer range of T_NTCMapTbl#_Cnt_enum[SIZE] in *doc |

| Return Value | none |  |  |  |

| Function Name | NxtrDiagMgr_GetNTCFailed_Core | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | NTCFailed_Ptr_T_lgc | const boolean pointer | False | True |

| Return Value | RetVal | Std_ReturnType | E_NOT_OK | E_OK |

| Function Name | NxtrDiagMgr_GetNTCActive_Core | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | NTCActive_Ptr_T_lgc | const boolean pointer | FALSE | TRUE |

| Return Value | RetVal | Std_ReturnType | E_NOT_OK | E_OK |

| Function Name | NxtrDiagMgr_GetNTCStatus_Core | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | Status_Ptr_T_u08 | const boolean pointer | FALSE | TRUE |

| Return Value | RetVal | Std_ReturnType | E_OK<br/>E_NOT_OK | E_OK<br/>E_NOT_OK |

| Function Name | NxtrDiagMgr_SetNTCStatus_Core | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | Param_Cnt_T_u08 | Uint8 | 0 | FULL |

|  | Status_Cnt_T_enum | NxtrDiagMgrStatus | NTC_STATUS_PASSED<br/>NTC_STATUS_FAILED<br/>NTC_STATUS_PREPASSED<br/>NTC_STATUS_PREFAILED | NTC_STATUS_PASSED<br/>NTC_STATUS_FAILED<br/>NTC_STATUS_PREPASSED<br/>NTC_STATUS_PREFAILED |

|  | NTCInfo_Cnt_T_str[79] | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc | Refer Range of DiagMgr_NTCInfo#_Cnt_M_str[SIZE] in *doc |

|  | DiagSts_Cnt_T_b16[2] | Refer Range of DiagSts#_Cnt_M_b16[SIZE] in *doc | Refer Range of DiagSts#_Cnt_M_b16[SIZE] in *doc | Refer Range of DiagSts#_Cnt_M_b16[SIZE] in *doc |

|  | ActiveRmpRate_Cnt_T_f32[2] | Refer Range of ActiveRmpRate#_UlspmS_M_f32[SIZE] in *doc | Refer Range of ActiveRmpRate#_UlspmS_M_f32[SIZE] in *doc | Refer Range of ActiveRmpRate#_UlspmS_M_f32[SIZE] in *doc |

|  | ActDiagSts_Ptr_T_u08 | Refer Range of ActDiagSts#_Cnt_M_u08 in *doc | Refer Range of ActDiagSts#_Cnt_M_u08 in *doc | Refer Range of ActDiagSts#_Cnt_M_u08 in *doc |

| Return Value | RetVal | Std_ReturnType | E_OK<br/>E_NOT_OK | E_OK<br/>E_NOT_OK |

| Function Name | NxtrDiagMgr_ReportNTCStatus_Core | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | Param_Cnt_T_u08 | Uint8 | 0 | FULL |

|  | Status_Cnt_T_enum | NxtrDiagMgrStatus | NTC_STATUS_PASSED<br/>NTC_STATUS_FAILED<br/>NTC_STATUS_PREPASSED<br/>NTC_STATUS_PREFAILED | NTC_STATUS_PASSED<br/>NTC_STATUS_FAILED<br/>NTC_STATUS_PREPASSED<br/>NTC_STATUS_PREFAILED |

|  | NTCInfoQueue_Cnt_T_str [5] | Refer Range of NTCInfoQueue#_Cnt_M_str[SIZE] in *doc | Refer Range of NTCInfoQueue#_Cnt_M_str[SIZE] in *doc | Refer Range of NTCInfoQueue#_Cnt_M_str[SIZE] in *doc |

|  | NTCQueueIndex_Ptr_T_u08 | Refer Range of NTCQueueIndex#_Cnt_M_u08 in *doc | Refer Range of NTCQueueIndex#_Cnt_M_u08 in *doc | Refer Range of NTCQueueIndex#_Cnt_M_u08 in *doc |

| Return Value |  | Std_ReturnType | E_OK | E_OK |

| Function Name | SetBits_u8 | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | Data | const uint8 pointer | 0 | 255 |

|  | BitMask | uint8 | 0 | 255 |

| Return Value | N/A |  |  |  |

| Function Name | ClrBits_u8 | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | Data | const uint8 pointer | 0 | 255 |

|  | BitMask | uint8 | 0 | 255 |

| Return Value | N/A |  |  |  |

| Function Name | ReadBit_u8 | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | Data | uint8 | 0 | 255 |

|  | BitMask | uint8 | 0 | 255 |

| Return Value | (anonymous) | boolean | FULL | FULL |

| Function Name | SetBits_u16 | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | Data | const uint16 pointer | FULL | FULL |

|  | BitMask | uint16 | FULL | FULL |

| Return Value | N/A |  |  |  |

| Function Name | ReadBit_u32 | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | Data | uint32 | 0x000000 | 0xFFFFFF |

|  | BitMask | uint32 | 0x000000 | 0xFFFFFF |

| Return Value | (anonymous) | boolean | FULL | FULL |

| Function Name | ProcessDiagSts | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | FltRsp_Cnt_T_u32 | Uint32 | 0 | FULL |

|  | DiagSts_Ptr_T_b16 | const uint16 pointer | 0 | FULL |

| Return Value | N/A |  |  |  |

| Function Name | ProcessRampResponse | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | FltRsp_Cnt_T_u32 | Uint32 | 0 | FULL |

|  | ActiveRmpRate_Ptr_T_f32 | Const float32 pointer | 0.0001 | 0.5 |

|  | DiagSts_Ptr_T_b16 | Const uint16 pointer | 0 | FULL |

| Return Value | N/A |  |  |  |

| Function Name | FailedCheckAndProcessing | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTCInfo_Ptr_T_str | const uint16 NTCInfo_Str | See section 3.1.1 | See section 3.1.1 |

|  | DiagSts_Ptr_T_b16 | const uint16 pointer | 0 | FULL |

|  | MaxRampRate_Ptr_T_f32 | Const float32 pointer | 0.0001 | 0.5 |

|  | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

| Return Value | N/A |  |  |  |

| Data | Value |

| --- | --- |

|  |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

|  |  |  |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| FailedCheckAndProcessing | AP_DIAGMGR_CODE |

| ProcessRampResponse | AP_DIAGMGR_CODE |

| ProcessDiagSts | AP_DIAGMGR_CODE |

| SetBits_u8 | AP_DIAGMGR_CODE |

| ClrBits_u8 | AP_DIAGMGR_CODE |

| ReadBit_u8 | AP_DIAGMGR_CODE |

| ReadBit_u32 | AP_DIAGMGR_CODE |

| SetBits_u16 | AP_DIAGMGR_CODE |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1 | Initial MDD version | 14-Feb-13 | VK |

| 2 | MDD catch up to match latest SRC Ver 4 | 24- June- 13 | NRAR |

|  |  |  |  |
