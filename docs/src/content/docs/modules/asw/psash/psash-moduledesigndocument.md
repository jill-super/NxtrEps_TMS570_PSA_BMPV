---
title: 'PSASH ModuleDesignDocument'
description: 'Converted design document: PSASH ModuleDesignDocument'
---

> **Source:** `PSASH/doc/PSASH_ModuleDesignDocument.docx`  
> **Module:** [PSASH](../../../../asw/psash/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

### For

### PSASH

### May 11, 2016

### Prepared For:

### Software Engineering

### Nexteer Automotive,

### Saginaw, MI, USA

### Prepared By:

### SEPG,

### Nexteer Automotive,

### Saginaw, MI, USAChange History

### Table of Contents

1	Introduction	5

1.1	Purpose	5

1.2	Scope	5

2	PSASH High-Level Description	6

3	Design details of software module	7

3.1	Graphical representation of PSASH	7

3.2	Data Flow Diagram	7

3.2.1	Module level DFD	7

3.2.2	Sub-Module level DFD	7

3.3	Component diagram	7

3.4	Variable Data Dictionary	7

3.4.1	User defined ‘typedef’ definition/declaration	7

3.4.2	Variable definition for enumerated types	7

3.5	Constant Data Dictionary	7

3.5.1	Program Constants	7

3.5.2	Module Specific Lookup Tables	8

3.6	Software Module Implementation	8

3.6.1	Sub-Module Functions	8

3.6.2	Interrupt Service Routines	8

3.6.3	_SCOMM () Functions	8

3.6.4	Module Internal (Local) Functions	8

3.6.4.1	Local Function #1	8

3.6.4.1.1	Description	9

3.6.4.2	Local Function #2	9

3.6.4.2.1	Description	9

3.6.4.3	Local Function #3	9

3.6.4.3.1	Description	9

3.6.4.4	Local Function #4	9

3.6.4.4.1	Description	10

3.6.4.5	Local Function #5	10

3.6.4.5.1	Description	10

3.6.4.6	Local Function #6	10

3.6.4.6.1	Description	10

3.6.4.7	Local Function #7	10

3.6.4.7.1	Description	10

3.6.4.8	Local Function #8	10

3.6.4.8.1	Description	11

3.6.4.9	Local Function #9	11

3.6.4.9.1	Description	11

3.6.4.10	Local Function #10	11

3.6.4.10.1	Description	11

3.6.5	Transition Functions	12

4	Known Limitations with Design	13

5	UNIT TEST CONSIDERATION	14

Appendix A	Abbreviations and Acronyms	15

Appendix B	Glossary	16

Appendix C	References	17

## Introduction

### Purpose

### Scope

## PSASH High-Level Description

## Design details of software module

Refer FDD.

### Graphical representation of PSASH

### Data Flow Diagram

Refer FDD

#### Module level DFD

#### Sub-Module level DFD

### Component diagram

Refer FDD

### Variable Data Dictionary

#### User defined ‘typedef’ definition/declaration

None

#### Variable definition for enumerated types

None

### Constant Data Dictionary

#### Program Constants

##### Local Constants

##### Global Constants

Refer .m file

#### Module Specific Lookup Tables

None

### Software Module Implementation

#### Sub-Module Functions

##### Initialization sub-module {PSASH_Init1()}

Refer FDD for the functionality.

##### Periodic sub-module {PSASH_Per1 ()}

Refer FDD for the functionality.

Following deviations are done in the SW implementation:

- In FDD, 'PSASH_ApaEnaRgln_Cnt_M_lgc' flag is set within ‘PSASH_CONTROL_PROGRESS entry' sub block.  In SW implementation, 'PSASH_ApaEnaRgln_Cnt_M_lgc' is set to TRUE in main periodic function.

- In ‘Determine Apa Allowed’ block, float variable ‘OutputRampMult_Uls_f32’ is compared to ‘D_ONE_ULS_F32’  for equality. This float equality operation is not allowed. So in SW implementation, this float variable is converted to fixed integer before comparison.

- ‘SystemState_Cnt_enum’ range should be ‘0’ to ‘4’ and initial value should be ‘3’ in .m file

- Requirement traceability to be corrected in FDD.

Above deviations confirmed with FDD owner and FDD will be updated inline with current SW implementation in next FDD updates.

##### Non Periodic sub-module {_NONPer()}

None

#### Interrupt Service Routines

None

#### _SCOMM () Functions

None

#### Module Internal (Local) Functions

### Local Function #1

### Description

Checks all exit paths from 'PSASH_PROGRESS entry' state.

### Local Function #2

### Description

Checks all exit paths from 'PSASH_AVAILABLE_READY / PSASH_AVAILABLE_TRANSITIONCAUSE entry' states.

### Local Function #3

### Description

Checks all exit paths from 'PSASH_Unavailable_ready' state.

### Local Function #4

### Description

If 'Sig_Uls_T_f32' is greater than 'Thd_Uls_T_f32', return TRUE.

### Local Function #5

### Description

If 'Sig_Uls_T_f32' is greater than or equal to 'Thd_Uls_T_f32', return TRUE.

### Local Function #6

### Description

If 'Sig_Uls_T_f32' is less than or equal  'Thd_Uls_T_f32', return TRUE.

### Local Function #7

### Description

Implementation of "Determine Apa Allowed" block.

### Local Function #8

### Description

Implementation of "Determine Regulation Errors" block.

### Local Function #9

### Description

Implementation of "Handwheel intervention" block. ‘HwActionMinReached_Cnt_T_lgc’ and ‘HwActionMaxReached_Cnt_T_lgc’ are the

outputs of this function.

### Local Function #10

### Description

Implementation of "Determine Regulation Errors" block.

#### Transition Functions

None

## Known Limitations with Design

None

## UNIT TEST CONSIDERATION

None

###### Abbreviations and Acronyms

###### Glossary

Note: Terms and definitions from the source “Nexteer Automotive” take precedence over all other definitions of the same term.  Terms and definitions from the source “Nexteer Automotive” are formulated from multiple sources, including the following:

- ISO 9000

- ISO/IEC 12207

- ISO/IEC 15504

- Automotive SPICE® Process Reference Model (PRM)

- Automotive SPICE® Process Assessment Model (PAM)

- ISO/IEC 15288

- ISO 26262

- IEEE Standards

- SWEBOK

- PMBOK

- Existing Nexteer Automotive documentation

###### References

| Description | Author | Version | Date |

| --- | --- | --- | --- |

| Initial Version | Sankardu Varadapureddi | 1.0 |  |

|  |  |  |  |

|  |  |  |  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

|  |  |  |  |

|  |  |  |  |

| Function Name | Chk_Progs_Exit_Conds | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | FaultActv_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | ThrmlLmtReached_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | VehSpdTooHigh_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | HwActionMaxReached_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | ApaCmdReq_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | ApaAllowed_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | ApaRelaxReq_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | HwPosCmdErr_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | MtrStalled_Cnt_T_lgc | boolean | FALSE | TRUE |

| Return Value | N/A |  |  |  |

| Function Name | Chk_Available_Exit_Conds | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | ApaAllowed_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | ApaCmdReq_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | VehSpdTooHigh_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | MtrStalled_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | HwActionMinReached_Cnt_T_lgc | boolean | FALSE | TRUE |

| Return Value | None |  |  |  |

| Function Name | Chk_UnAvailableReady_Exit_Conds | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | FaultActv_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | ApaEna_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | ApaAllowed_Cnt_T_lgc | boolean | FALSE | TRUE |

| Return Value | None |  |  |  |

| Function Name | IsVehicleSpeedAbvThd | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | Sig_Uls_T_f32 | float32 | 0 | 511 |

|  | Thd_Uls_T_f32 | float32 | 0 | 10000 |

| Return Value | ThdExcdd_Cnt_T_lgc | boolean | FALSE | TRUE |

| Function Name | IsThermLimitAbvThd | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | Sig_Uls_T_f32 | float32 | 0 | 1 |

|  | Thd_Uls_T_f32 | float32 | 0 | 10000 |

| Return Value | ThdExcdd_Cnt_T_lgc | boolean | FALSE | TRUE |

| Function Name | IsAssistStallBlwThd | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | Sig_Uls_T_f32 | float32 | 0 | 8.8 |

|  | Thd_Uls_T_f32 | float32 | 0 | 10000 |

| Return Value | ThdExcdd_Cnt_T_lgc | boolean | FALSE | TRUE |

| Function Name | DtrmnApaAllwd | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | ApaAuthn_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | HandwheelAuthority_Uls_T_f32 | float32 | 0 | 1 |

|  | OutputRampMult_Uls_T_f32 | float32 | 0 | 1 |

| Return Value | ApaAllowed_Cnt_T_lgc | boolean | FALSE | TRUE |

| Function Name | DtrmnRglnErr | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | HandwheelPosition_HwDeg_T_f32 | float32 | -1440 | 1440 |

|  | PosSrvoHwAngle_HwDeg_T_f32 | float32 | -780 | 780 |

| Return Value | HwPosCmdErr_Cnt_T_lgc | boolean | FALSE | TRUE |

| Function Name | HwIntv | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | HwTorque_HwNm_T_f32 | float32 | -10 | 10 |

|  | *HwActionMinReached_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | *HwActionMaxReached_Cnt_T_lgc | boolean | FALSE | TRUE |

| Return Value | None |  |  |  |

| Function Name | DtrmnSysFlt | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | VehicleSpeedValid_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | CpkOk_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | PosSrvoNTC_Cnt_T_lgc | boolean | FALSE | TRUE |

|  | FTermActv_Cnt_T_lgc | boolean | FALSE | TRUE |

| Return Value | FaultActv_Cnt_T_lgc | boolean | FALSE | TRUE |

| Abbreviation or Acronym | Description |

| --- | --- |

|  |  |

|  |  |

| Term | Definition | Source |

| --- | --- | --- |

| MDD | Module Design Document |  |

| DFD | Data Flow Diagram |  |

| Ref. # | Title | Version |

| --- | --- | --- |

| 1 | AUTOSAR Specification of Memory Mapping (Link:AUTOSAR_SWS_MemoryMapping.pdf) | v1.3.0 R4.0 Rev 2 |

| 2 | MDD Guideline | EA3 01.04.00 |

| 3 | Software Naming Conventions.doc | 2.0 |

| 4 | Software Design and Coding Standards.doc | 2.1 |

| 5 | CF013B_PSASH_Design | 1.1.0 |
