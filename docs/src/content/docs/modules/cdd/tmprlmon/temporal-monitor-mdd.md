---
title: 'Temporal Monitor MDD'
description: 'Converted design document: Temporal Monitor MDD'
---

> **Source:** `TmprlMon/doc/Temporal_Monitor_MDD.docx`  
> **Module:** [TmprlMon](../../../../cdd/tmprlmon/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module --

## High-Level Description

This module helps ensure valid execution time for the forward path.  It generates the rising edge of the monitor signal used by an external processor to determine execution time, performs an initialization routine for the external TMF processor, and performs run time diagnostics for the TMF processor.

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

<None>

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

None

### Local Functions/Macros Used by this MDD only

None

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

None

### Periodic Functions

#### Per: _Per1

##### Design Rationale

This function generates the rising edge of the WdMonitor signal.  It must be mapped in the forward path after the ADC sampling, and before the rest of the forward path calculations.

The FDD requires that a lookup should be performed based on the current TMF state to determine whether to set the WdMonitor signal to a high state.  Then, if this is true, the signal is set high.  Otherwise, it is not set.

Instead, the WdMonitor signal is set to the lookup value itself.  This way, when the WdMonitor signal is enabled, it will be set high (and set low when disabled).  Functionally, this fulfills the FDD requirements (with the assumption that TmprlMon_Per1 and TmprlMon_Per2 are the only functions that affect the state of the WdMonitor signal).

##### Program Flow Start

Rte_Call_TmprlMon_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

None

##### Set WdMonitor High (depending on state)

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

Rte_Call_TmprlMon_Per1_CP1_CheckpointReached()

#### Per: _Per2

##### Design Rationale

The WdMonitor signal is not set at the end of this function (as specified in the FDD).  This is per the design specified in TmprlMon_Per1 (see section  for more information).

##### Program Flow Start

##### Rte_Call_TmprlMon_Per2_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

TMFTestStart_Cnt_T_lgc = Rte_IRead_TmprlMon_Per2_TMFTestStart_Cnt_lgc()

TmprlMonSt_Cnt_T_enum = TmprlMonSt_Cnt_M_enum

Rte_Call_FetDrvCntl_OP_GET(&FetDrvCntlFdbk_Cnt_T_lgc)

Rte_Call_PwrSwitchEn_OP_GET(&PwrSwitchEnFdbk_Cnt_T_lgc)

##### Temporal Monitor Control Circuit Fault

##### Release WARMINIT Request when OPERATE State is Reached

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

Rte_Call_TmprlMon_Per3_CP1_CheckpointReached()

#### Per: _Per3

##### Design Rationale

None

##### Program Flow Start

Rte_Call_TmprlMon_Per3_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

Rte_Call_SysFault2_OP_GET(&SysFault2_Cnt_T_lgc)

Rte_Call_SysFault3_OP_GET(&SysFault3_Cnt_T_lgc)

Rte_Call_PwrSwitchEn_OP_GET(&PwrSwitchEn_Cnt_T_lgc)

Rte_Call_FetDrvCntl_OP_GET(&FetDrvCntl_Cnt_T_lgc)

##### TMF Run Time Control Circuit Fault

##### Store Local copy of outputs into Module Outputs

None

##### Program Flow End

Rte_Call_TmprlMon_Per3_CP1_CheckpointReached()

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

None

### Transition Functions

#### Trns: _Trns1

##### Design Rationale

This function is run upon entering the WARMINIT state.  This is done (as opposed to an initialization function) because of the possibility of entering the DISABLE state before the TMF initialization process is complete.

##### Reset Values

#### Trns: _Trns2

##### Design Rationale

This function is run upon entering the DISABLE state.

## Execution Requirements

### Execution Sequence of the Module

The TmprlMon_Per1 function is executed at the beginning of the forward path (after ADC calculations).  TmprlMon2_Per1 is executed at the end of the forward path.  This will provide a “pulse” on WdMonitor for the duration of the forward path calculations.  TmprlMon_Per2 is run outside of the forward path, in order to advance the TMF initialization process.  TmprlMon_Per3 is run at 8ms intervals, and is only run during the system OPERATE and DISABLE states.  In this way, TmprlMon_Per3 should only be run once the TMF initialization is complete (as the completion of this process is a prerequisite to leaving the WARMINIT state).

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

None

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| TMFTestStart_Cnt_lgc | TMFTestStart_Cnt_lgc | TMFTestComplete_Cnt_lgc |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| TmprlMonSt_Cnt_M_enum | DT_TmprlMonSt | n/a | n/a | TMPRLMON_START_SEC_VAR_CLEARED_UNSPECIFIED |

| InitTestStatus_Cnt_M_enum | NxtrDiagMgrStatus | n/a | n/a | TMPRLMON_START_SEC_VAR_CLEARED_UNSPECIFIED |

| NTCStatusByte_Cnt_M_u08 | 1 | 0 | 13 | TMPRLMON_START_SEC_VAR_CLEARED_8 |

| InitialTime_mS_M_u32 | 1 | 0 | 232 - 1 | TMPRLMON_START_SEC_VAR_CLEARED_32 |

| TMFTestComplete_Cnt_M_lgc | 1 | FALSE | TRUE | TMPRLMON_START_SEC_VAR_CLEARED_BOOLEAN |

| TMFPrepCheckFlag_Cnt_M_lgc | 1 | FALSE | TRUE | TMPRLMON_START_SEC_VAR_CLEARED_BOOLEAN |

| TmprlMonPNAccum_Cnt_M_u16 | 1 | 0 | 1000 | TMPRLMON_START_SEC_VAR_CLEARED_16 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| DT_TmprlMonSt | TMPMON_RESET1 (0U)<br/>TMPMON_INIT_ALLOFF1 (1U)<br/>TMPMON_INIT_TMOFF1 (2U)<br/>TMPMON_INIT_PICINIT1 (3U)<br/>TMPMON_INIT_SF2OFF (4U)<br/>TMPMON_INIT_ALLON2 (5U)<br/>TMPMON_INIT_SF3OFF (6U)<br/>TMPMON_INIT_ALLON3 (7U)<br/>TMPMON_INIT_TMOFF2 (8U)<br/>TMPMON_RESET2 (9U)<br/>TMPMON_INIT_ALLOFF2 (10U)<br/>TMPMON_INIT_SF23OFF (11U)<br/>TMPMON_INIT_PICINIT2 (12U)<br/>TMPMON_OPERATE (13U)<br/>TMPMON_PREPCHECK (14U) | uint8 | 0 | 14 |

| TmprlMonState_Str | SysFault3Cmd_lgc | IoHwAb_BoolType | 0 | 1 |

| TmprlMonState_Str | SysFault2Cmd_lgc | IoHwAb_BoolType | 0 | 1 |

| TmprlMonState_Str | WdMonitorCmd_lgc | IoHwAb_BoolType | 0 | 1 |

| TmprlMonState_Str | WdResetCmd_lgc | IoHwAb_BoolType | 0 | 1 |

| TmprlMonState_Str | FetDrvCntlFdbk_lgc | IoHwAb_BoolType | 0 | 1 |

| TmprlMonState_Str | PwrSwitchEnFdbk_lgc | IoHwAb_BoolType | 0 | 1 |

| TmprlMonState_Str | StepTime_mS_u16 | uint16 | 0 | 216 - 1 |

| Constant Name |

| --- |

| <None> |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| TMPMON_NUMSTATES | 1 | Counts | 14U |

| Constant Name |

| --- |

| STD_LOW |

| STD_HIGH |

| Constant Name | Value | Software Segment |

| --- | --- | --- |

| TmprlMonStateTbl_Cnt_M_Str[TMPMON_NUMSTATES] | {{STD_LOW,  STD_LOW,  STD_LOW,  STD_LOW,  STD_LOW,  STD_LOW,  4U},<br/>{STD_LOW,  STD_LOW,  STD_LOW,  STD_HIGH, STD_LOW,  STD_LOW,  31U},<br/>{STD_HIGH, STD_HIGH, STD_LOW,  STD_HIGH, STD_LOW,  STD_LOW,  1U},<br/>{STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, 40U},<br/>{STD_HIGH, STD_LOW,  STD_HIGH, STD_HIGH, STD_LOW,  STD_LOW,  1U},<br/>{STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, 1U},<br/>{STD_LOW,  STD_HIGH, STD_HIGH, STD_HIGH, STD_LOW,  STD_LOW,  1U},<br/>{STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, 1U},<br/>{STD_HIGH, STD_HIGH, STD_LOW,  STD_HIGH, STD_LOW,  STD_LOW,  24U},<br/>{STD_LOW,  STD_LOW,  STD_LOW,  STD_LOW,  STD_LOW,  STD_LOW,  1U},<br/>{STD_LOW,  STD_LOW,  STD_LOW,  STD_HIGH, STD_LOW,  STD_LOW,  31U},<br/>{STD_LOW,  STD_LOW,  STD_HIGH, STD_HIGH, STD_LOW,  STD_LOW,  24U},<br/>{STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, 16U},<br/><br/>{STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, STD_HIGH, 0U},<br/>{STD_LOW,  STD_LOW,  STD_LOW,  STD_LOW,  STD_HIGH, STD_LOW,  0U}} | TMPRLMON_START_SEC_CONST_UNSPECIFIED |

| Data | Value |

| --- | --- |

| Rte_InitValue_TMFTestComplete_Cnt_lgc | FALSE |

| Rte_InitValue_TMFTestStart_Cnt_lgc | FALSE |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| TmprlMon_Per1 | 2 ms | ALL |

| TmprlMon_Per2 | 2 ms | WARMINIT |

| TmprlMon_Per3 | 4 ms | OPERATE, DISABLE |

| TmprlMon_Trns1 | Transition | Entering WARMINIT |

| TmprlMon_Trns2 | Transition | Entering DISABLE |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| <None> |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| TmprlMon_Per1 | RTE_START_SEC_SA_TMPRLMON_APPL_CODE |

| TmprlMon_Per2 | RTE_START_SEC_SA_TMPRLMON_APPL_CODE |

| TmprlMon_Per3 | RTE_START_SEC_SA_TMPRLMON_APPL_CODE |

| TmprlMon_Trns1 | RTE_START_SEC_SA_TMPRLMON_APPL_CODE |

| TmprlMon_Trns2 | RTE_START_SEC_SA_TMPRLMON_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial MDD | 25-May-11 | BG |

| 2 | 2 | Updated NTCs with global constants | 02-Dec-11 | OT |

| 3 | 3.0 | Initial Component MDD (started from scratch) | 21-Mar-12 | OT |

| 4 | 4 | Correction to move STD_LOW and STD_HIGH to global constant definitions since they are AUTOSAR defined constants | 28-Mar-12 | JJW |

| 5 | 5 | Changed NTC Status byte to STATIC, updated state times | 01-Apr-12 | OT |

| 6 | 6 | Updated to FDD 19B v002B (state times, NTC parameter info) | 19-Jun-12 | OT |

| 7 | 7 | Changed Per3 running states (to avoid conflict with ShtdnMech) | 25-Jul-12 | OT |

| 8 | 8 | Added functionality for Hardware Power Up, removed Trns2 (obsolete with change in Per3 running states) | 19-Sep-12 | OT |

| 9 | 9 | Addition of checkpoints  in the program flow | 27-Sep-12 | Selva |

| 10 | 10 | Updated to FDD Ver005<br/>DISABLE and ESMDIABLE steps are removed. Added ALLON2 Step.<br/>Transition times of ALLON1,ALLON2 and OPERATE changed<br/>Transition2 added for Shutdown operation | 28-SEP-12 | NRAR |

| 11 | 11 | Fix for anomaly #3912 | 24-Oct-12 | BWL |

| 12 | 12 | Update execution rate for Per1 | 24-Oct-12 | BWL |

| 13 | 13 | Multi-app support.  Removed Per2 | 12-Nov-12 | JJW |

| 14 | 14 | Updated to FDD ver 009 | 14-Apr-13 | SP |

| 15 | 15 | Updates for NTS param anomalies 5113 & 5280 | 26-Jul-13 | Jared |

|  |  |  |  |  |
