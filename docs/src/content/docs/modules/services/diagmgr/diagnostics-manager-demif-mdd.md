---
title: 'Diagnostics Manager DemIf MDD'
description: 'Converted design document: Diagnostics Manager DemIf MDD'
---

> **Source:** `DiagMgr/doc/Diagnostics_Manager_DemIf_MDD.docx`  
> **Module:** [DiagMgr](../../../../services/diagmgr/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module --  DEM Interface

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

### Global Functions/Macros Defined by this Module

#### Diagnostic Manager Init 1

##### Description

#### Diagnostic Manager Transition 1

##### Description

Rte_Call_DemIf_RestartDem()

Rte_Call_DemIf_SetOperationCycleState(NxtrDefaultOpCycle, NXTR_CYCLE_STATE_START)

#### Diagnostic Manager StaCtrl Shutdown

##### Description

Rte_Call_DemIf_SetOperationCycleState(NxtrDefaultOpCycle, NXTR_CYCLE_STATE_END)

Rte_Call_DemIf_DemShutdown()

CreateStorageArray(1U)

NvM_SetRamBlockStatus(NVM_BLOCK_DIAGMGR_NTCSTRG, TRUE)

NvM_SetRamBlockStatus(NVM_BLOCK_DIAGMGR_BLACKBOX, TRUE)

#### Diagnostic Manager Periodic 2

##### Description

#### Diagnostic Manager Get NTC Information

##### Description

#### Diagnostic Manager Reset NTC Status

##### Description

ResetNTCFlag_Cnt_M_u08 = ~ResetNTCFlag_Cnt_M_u08

#### Diagnostic Manager Read Storage Array

##### Description

CreateStorageArray(0U)

#### Diagnostic Manager Clear Black Box

##### Description

#### Diagnostic Manager Clear Latch Counters

##### Description

#### Update Black Box

##### Description

### Local Functions/Macros Used by this MDD only

#### Create Storage Array

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

The latch active counters will not be stepped/checked on a quick ignition cycle as the Init1 function will not be called.

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| IgnCnt_Cnt_u16 | IgnCnt_Cnt_u16 |  |

| MtrTrq_MtrNm_f32 | MtrTrq_MtrNm_f32 |  |

| VehSpd_Kph_f32 | VehSpd_Kph_f32 |  |

| HwTrq_HwNm_f32 | HwTrq_HwNm_f32 |  |

| SystemState_Mode | SystemState_Mode |  |

| Variable Name | Datatype | Resolution | Resolution | Legal Range<br/>(min) | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment<br/>{Data Type} | Software Segment<br/>{Data Type} | Software Segment<br/>{Data Type} |

| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

| DEMEventActive_Cnt_M_lgc[D_NUMOFDEMEVENTS_CNT_U08+1] | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx |

| ResetNTCFlag_Cnt_M_u08 | Diagnostics_Manager_GeneratedCfg_MDD.docx | Diagnostics_Manager_GeneratedCfg_MDD.docx | Diagnostics_Manager_GeneratedCfg_MDD.docx | Diagnostics_Manager_GeneratedCfg_MDD.docx | Diagnostics_Manager_GeneratedCfg_MDD.docx | Diagnostics_Manager_GeneratedCfg_MDD.docx | Diagnostics_Manager_GeneratedCfg_MDD.docx | Diagnostics_Manager_GeneratedCfg_MDD.docx | Diagnostics_Manager_GeneratedCfg_MDD.docx |

| LatchCounter_Cnt_u16 | uint16 | uint16 | 1 | 1 | 0 | 0 | 0 | 65535 | DIAGMGRDEMIF_START_SEC_VAR_16 |

| NTCStrgArray_Cnt_str | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx |

| NTCBlackBoxData_Cnt_str | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx | Refer to Diagnostics_Manager_Core_MDD.docx |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| Typedef struct {} NTCLatch_Str | NTC | NTCNumber | 0 | 511 |

|  | DiagSettings_Str.Threshold | Uint16 | 0 | 65535 |

|  | DiagSettings_Str.PStep | Uint16 | 0 | 65535 |

|  | DiagSettings_Str.NStep | Uint16 | 0 | 65535 |

| Constant Name |

| --- |

| t_SortedNTCs_Cnt_enum[] |

| k_FltRspTbl_Cnt_str[] |

| t_BlkBoxGrp_Ptr_u32[][] |

| t_LatchFaults_Cnt_str[] |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_EVTNOTPASSBITS_CNT_B8 | N/A | Counts | (D_TESTFAILEDBIT_CNT_B8 | D_TESTNOTCOMPLETETHISOPCYCLEBIT_CNT_B8) |

| D_AGINGCOUNTERTHRESH_CNT_U08 | N/A | Counts | 0x40 |

| Constant Name |

| --- |

| D_NUMOFDEMEVENTS_CNT_U08 |

| D_TESTFAILEDBIT_CNT_B8 |

| D_TESTNOTCOMPLETETHISOPCYCLEBIT_CNT_B8 |

| D_NTCACTIVEBITS_CNT_B8 |

| D_MAXLATCHACTIVENTCS_CNT_U08 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| T_DiagMgrNtcAppInfoMap_Cnt_Str[SIZE] |  | Refer * | AP_DIAGMGR_CONST |

| T_DiagMgrNtcInfoPtr_Cnt_Str[SIZE] |  | Refer * | AP_DIAGMGR_CONST |

|  |  |  |  |

| Function Name | DiagMgr_Init1 | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | none |  |  |  |

| Return Value | none |  |  |  |

| Function Name | DiagMgr_Trns1 | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | none |  |  |  |

| Return Value | none |  |  |  |

| Function Name | DiagMgr_StaCtrl_Shutdown | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | none |  |  |  |

| Return Value | none |  |  |  |

| Function Name | DiagMgr_Per2 | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | none |  |  |  |

| Return Value | none |  |  |  |

| Function Name | DiagMgr_SCom_GetNTCInfo | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_enum | NTCNumber | 0 | 511 |

|  | Param_Ptr_T_u08 | const uint8 pointer | 0 | FULL |

|  | Status_Ptr_T_u08 | const uint8 pointer | 0 | FULL |

|  | AgingCounter_Ptr_T_u08 | const uint8 pointer | 0 | FULL |

| Return Value | none |  |  |  |

| Function Name | DiagMgr_SCom_ResetNTCStatus | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Return Value | none |  |  |  |

| Function Name | DiagMgr_SCom_ReadStrgArray | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

|  |  |  |  |  |

| Return Value | none |  |  |  |

| Function Name | DiagMgr_SCom_ClearBlackBox | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Return Value | none |  |  |  |

| Function Name | DiagMgr_SCom_ClearLatchCounters | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |

| Return Value | none |  |  |  |

| Function Name | UpdateBlkBox | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | NTC_Cnt_T_u08 | Uint8 | 0 | FULL |

|  | Param_Cnt_T_u08 | Uint8 | 0 | FULL |

|  | BlkBoxGrpIdx_Cnt_T_u08 | Uint8 | 0 | 6 |

| Return Value | none |  |  |  |

| Function Name | CreateStorageArray | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | AgingCounterIncrement | uint8 | 0 | 1 |

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

| DiagMgr_Trns1 | RTE_AP_DIAGMGR_APPL_CODE |

| DiagMgr_Trns2 | RTE_AP_DIAGMGR_APPL_CODE |

| DiagMgr_Per2 | RTE_AP_DIAGMGR_APPL_CODE |

| DiagMgr_SCom_GetNTCInfo | RTE_AP_DIAGMGR_APPL_CODE |

| DiagMgr_Scom_ResetNTCStatus | RTE_AP_DIAGMGR_APPL_CODE |

| DiagMgr_Scom_ReadStrgArray | RTE_AP_DIAGMGR_APPL_CODE |

| DiagMgr_Scom_ClearBlackBox | RTE_AP_DIAGMGR_APPL_CODE |

| UpdateBlkBox | AP_DIAGMGR_CODE |

| CreateStorageArray | AP_DIAGMGR_CODE |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1 | Initial MDD version | 26-Mar-13 | VK |

| 2 | MDD Catch up to match to SRC Ver 5 | 24- June- 13 | NRAR |

| 3 | Added init function to support latch active diagnostic addition | 04-OCT-13 | Jared |

|  |  |  |  |
