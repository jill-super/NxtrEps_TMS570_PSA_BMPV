---
title: 'Diagnostics Manager GeneratedCfg MDD'
description: 'Converted design document: Diagnostics Manager GeneratedCfg MDD'
---

> **Source:** `DiagMgr/doc/Diagnostics_Manager_GeneratedCfg_MDD.docx`  
> **Module:** [DiagMgr](../../../../services/diagmgr/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module --  Core

## High-Level Description

## Figures

### Component Diagram

## Variable Data Dictionary

### Module Internal Variables

Note: *Refer: Size varies across projects. Check Configuration files under UTP/Contract folder

#### User defined typedef definition/declaration

## Constant Data Dictionary

### Calibration Constants

### Program(fixed) Constants

#### Embedded Constants

##### Local

##### Global

#### Note **: Global const values varies across projects. Check configuration files under UTP/Contract folder. “#” denotes application number.

#### Module specific Lookup Tables Constants

**NOTE : Elements and Size of table are different across different projects and applications. Check Configuration files under UTP/Contract folder

## Functions/Macros used by the Sub-Modules

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules are identified below,

TableSize_m()

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

#### Diagnostic Manager Initialization

##### Description

#### Diagnostic Manager Periodic Code

##### Description

#### Diagnostic Manager Transition Core

##### Description

#### Diagnostic Manager Get NTC Failed

##### Description

#### Diagnostic Manager Get NTC Active

##### Description

#### Diagnostic Manager Get NTC Status

##### Description

#### Diagnostic Manager Set NTC Status

##### Description

#### Diagnostic Manager Report NTC Status

##### Description

### Local Functions/Macros Used by this MDD only

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

|  |  |  |

| Variable Name | Datatype | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment<br/>{Data Type} |

| --- | --- | --- | --- | --- | --- |

| ResetNTCFlag_Cnt_M_u08 | Uint8 | 1 | 0<br/>FF | 0<br/>FF | DIAGMGR#_START_SEC_VAR_CLEARED_8 |

| NTCQueueIndex#_Cnt_M_u08 | Uint8 | 1 | Range depends on size of NTCInfoQueue#_Cnt_M_Str[SIZE]<br/>Refer * | Range depends on size of NTCInfoQueue#_Cnt_M_Str[SIZE]<br/>Refer * | DIAGMGR#_START_SEC_VAR_CLEARED_UNSPECIFIED |

| DiagMgrInitComp#_Cnt_M_lgc | Boolean | NA | False | True | DIAGMGR#_START_SEC_VAR_CLEARED_Unspecified |

| DiagMgr_NTCInfo#_Cnt_M_str[SIZE] | NTCInfo_Str | NA | See section 3.1.1 | See section 3.1.1 | DIAGMGR#_START_SEC_VAR_CLEARED_Unspecified |

| NTCInfoQueue#_Cnt_M_str[SIZE] | NTCInfoQueue_Str | NA | See section 3.1.1 | See section 3.1.1 | DIAGMGR#_START_SEC_VAR_CLEARED_Unspecified |

| ActDiagSts#_Cnt_M_u08 | Uint8 | 1 | 0 | 1 | DIAGMGR#_START_SEC_VAR_CLEARED_8 |

| ResetNTCFlag#_Cnt_M_u08 | Uint8 | 1 | 0<br/>FF | 0<br/>FF | DIAGMGR#_START_SEC_VAR_CLEARED_8 |

| DiagSts#_Cnt_M_b16[SIZE] | Uint16 | 1 | 0 | FULL | DIAGMGR#_START_SEC_VAR_CLEARED_Unspecified |

| ActiveRmpRate#_UlspmS_M_f32[SIZE] | Float32 | Single Precision float | 0.0001 | 0.5 | DIAGMGR#_START_SEC_VAR_CLEARED_32 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

|  |  |  |  |  |

|  |  |  |  |  |

| typedef struct { } NTCInfo_Str | Param | uint8 | 0 | FULL |

| typedef struct { } NTCInfo_Str | Status | uint8 | 0 | FULL |

| typedef struct { } NTCInfo_Str | AgingCounter | uint8 | 0 | 64 |

| typedef struct { } NTCInfoQueue_Str | NTC | NTCNumber | 0 | 511 |

|  | Param | Uint8 | 0 | FULL |

|  | Status | NxtrDiagMgrStatus | 0 | 255 |

| Constant Name |

| --- |

| k_FltRspTbl_Cnt_str[] |

| k_FltRmpRate_UlspmS_f32[] |

| Constant Name |

| --- |

| ** DIAGMGR_NUMAPPS |

| ** DIAGMGR_EVENTNUM_# |

| ** DIAGMGR_APID_# |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| T_NTCMapTbl#_Cnt_enum[SIZE] | N/A | { ** } | AP_DIAGMGR_CONST |

| T_DiagMgrNtcInfoPtr_Cnt_Str[SIZE] | N/A | ** {&DiagMgr_NTCInfo#_Cnt_M_str[0], #,<br/>} | AP_DIAGMGR_CONST |

| T_DiagMgrNtcAppInfoMap_Cnt_Str[SIZE] | N/A | ** {{ &DiagMgr_NTCInfo#_Cnt_M_str[0], #},<br/>…<br/>} | AP_DIAGMGR_CONST |

| Function Name | DiagMgr#_Init | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Multiplicity |  |  |  |  |

| Return Value | None |  |  |  |

| Function Name | DiagMgr#_Per | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Multiplicity |  |  |  |  |

| Return Value | none |  |  |  |

| Function Name | DiagMgr#_Trns | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Multiplicity |  |  |  |  |

| Return Value | none |  |  |  |

| Function Name | NxtrDiagMgr#_GetNTCFailed | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | NTCFailed_Ptr_T_lgc | const boolean pointer | False | True |

| Multiplicity |  |  |  |  |

| Return Value | RetVal | Std_ReturnType | E_OK | E_OK |

| Function Name | NxtrDiagMgr#_GetNTCActive_Core | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | NTCActive_Ptr_T_lgc | const boolean pointer | FALSE | TRUE |

| Multiplicity |  |  |  |  |

| Return Value | RetVal | Std_ReturnType | E_OK | E_OK |

| Function Name | NxtrDiagMgr#_GetNTCStatus | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | Status_Ptr_T_u08 | const boolean pointer | FALSE | TRUE |

| Multiplicity |  |  |  |  |

| Return Value | RetVal | Std_ReturnType | E_OK | E_OK |

| Function Name | NxtrDiagMgr#_SetNTCStatus | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | Param_Cnt_T_u08 | Uint8 | 0 | FULL |

|  | Status_Cnt_T_enum | NxtrDiagMgrStatus | NTC_STATUS_PASSED<br/>NTC_STATUS_FAILED<br/>NTC_STATUS_PREPASSED<br/>NTC_STATUS_PREFAILED | NTC_STATUS_PASSED<br/>NTC_STATUS_FAILED<br/>NTC_STATUS_PREPASSED<br/>NTC_STATUS_PREFAILED |

| Multiplicity |  |  |  |  |

| Return Value | RetVal | Std_ReturnType | E_OK<br/>E_NOT_OK | E_OK<br/>E_NOT_OK |

| Function Name | NxtrDiagMgr#_ReportNTCStatus | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | Param_Cnt_T_u08 | Uint8 | 0 | FULL |

|  | Status_Cnt_T_enum | NxtrDiagMgrStatus | NTC_STATUS_PASSED<br/>NTC_STATUS_FAILED<br/>NTC_STATUS_PREPASSED<br/>NTC_STATUS_PREFAILED | NTC_STATUS_PASSED<br/>NTC_STATUS_FAILED<br/>NTC_STATUS_PREPASSED<br/>NTC_STATUS_PREFAILED |

| Multiplicity |  |  |  |  |

| Return Value | RetVal | Std_ReturnType | E_OK | E_OK |

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

| DiagMgr#_Init | RTE_AP_DIAGMGR_APPL_CODE |

| DiagMgr#_Per | RTE_AP_DIAGMGR_APPL_CODE |

| DiagMgr#_Trns | RTE_AP_DIAGMGR_APPL_CODE |

| NxtrDiagMgr#_GetNTCFailed | RTE_AP_DIAGMGR_APPL_CODE |

| NxtrDiagMgr#_GetNTCActive | RTE_AP_DIAGMGR_APPL_CODE |

| NxtrDiagMgr#_GetNTCStatus | RTE_AP_DIAGMGR_APPL_CODE |

| NxtrDiagMgr#_SetNTCStatus | RTE_AP_DIAGMGR_APPL_CODE |

| NxtrDiagMgr#_ReportNTCStatus | RTE_AP_DIAGMGR_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1 | Initial MDD version | 25-June-13 | NRAR |
