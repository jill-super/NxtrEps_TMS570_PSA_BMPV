---
title: 'Diagnostics Manager FailAction MDD'
description: 'Converted design document: Diagnostics Manager FailAction MDD'
---

> **Source:** `DiagMgr/doc/Diagnostics_Manager_FailAction_MDD.docx`  
> **Module:** [DiagMgr](../../../../services/diagmgr/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module --  Fail Action

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

## Functions/Macros used by the Sub-Modules

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules are identified below,

TableSize_m()

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

#### Diagnostic Manager Periodic 1

##### Description

### Local Functions/Macros Used by this MDD only

#### Read Bits

##### Description

IF  (Data & BitMask) = 0

Return (FALSE)

ELSE
	Return(TRUE)

END IF

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

|  |  | DiagStsNonRecRmpToZeroFltPres_Cnt_lgc |

|  |  | DiagStsCtrldDisRmpPres_Cnt_lgc |

|  |  | DiagStsRecRmpToZeroFltPres_Cnt_lgc |

|  |  | DiagStsHWASbSystmFltPres_Cnt_lgc |

|  |  | DiagStsDefVehSpd_Cnt_lgc |

|  |  | DiagStsDefTemp_Cnt_lgc |

|  |  | DiagStsScomHWANotValid_Cnt_lgc |

|  |  | DiagStsWIRDisable_Cnt_lgc |

|  |  | DiagRampRate_XpmS_f32 |

|  |  | DiagRampValue_Uls_f32 |

|  |  | DiagRmpToZeroActive_Cnt_lgc |

| Variable Name | Datatype | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment<br/>{Data Type} |

| --- | --- | --- | --- | --- | --- |

| DiagSts#_Cnt_M_b16[2] |  |  |  |  |  |

|  |  |  |  |  |  |

| ActiveRmpRate_UlspmS_M_f32[2] |  |  |  |  |  |

|  |  |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

|  |  |  |  |  |

| Constant Name |

| --- |

|  |

|  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

|  |  |  |  |

| Constant Name |

| --- |

| DIAGMGR_NUMAPPS |

| D_DIAGSTSNONRECRMPTOZEROBIT_CNT_B16 |

| D_DIAGSTSRECRMPTOZEROBIT_CNT_B16 |

| D_DIAGSTSCTRLDDISRMPBIT_CNT_B16 |

| D_DIAGSTSHWASBSYSTMFLTBIT_CNT_B16 |

| D_DIAGSTSDEFVEHSPDBIT_CNT_B16 |

| D_DIAGSTSDEFTEMPBIT_CNT_B16 |

| D_DIAGSTSSCOMHWANOTVALIDBIT_CNT_B16 |

| D_DIAGSTSWIRDISABLEBIT_CNT_B16 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| T_DiagMgrDiagSts_Ptr_b16[] | N/A |  | AP_DIAGMGR_CONST |

| T_DiagMgrRmpRate_Ptr_f32[] | N/A |  | AP_DIAGMGR_CONST |

|  |  |  |  |

| Function Name | DiagMgr_Per1 | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | none |  |  |  |

| Return Value | none |  |  |  |

| Function Name | ReadBit_u16 | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | Data | Uint16 | 0 | FULL |

|  | BitMask | Uint16 | 0 | FULL |

| Return Value |  | Boolean | FALSE | TRUE |

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

| DiagMgr_Per1 | AP_DIAGMGR_CODE |

| ReadBit_u16 | AP_DIAGMGR_CODE |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1 | Initial MDD version | 14-Feb-13 | VK |

|  |  |  |  |
