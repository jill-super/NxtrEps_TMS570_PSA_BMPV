---
title: 'HiLoadStall MDD'
description: 'Converted design document: HiLoadStall MDD'
---

> **Source:** `HiLoadStall/doc/HiLoadStall_MDD.docx`  
> **Module:** [HiLoadStall](../../../../asw/hiloadstall/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module  -- HiLoadStall

## High-Level Description

The High Load Stall Thermal Management algorithm protects the system from prolonged intervals of high assist torque at near-stall conditions.

## Figures

### Diagram – Function Data Sharing

This diagram shows all data that is shared between functions within the module.

None

#### Diagram – Ret HiLoadStall _Per1

This diagram describes the functional characteristics and data flow of a given function.

## Module Inputs and Outputs

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

(Note: Full variable names required in table.)

(Note: All global variables including End Of Line data used should be shown here)

### Module Internal Variables

This section identifies the name, range and resolutions for module specific data created by this module.  If there are no range restrictions on the variable, the term “FULL” is placed into the table for legal range.

(Note: If no module specific variables are used by the design, place the text “None” in the first Variable Name cell in the table)

#### User defined typedef definition/declaration

This section documents any user types uniquely used for the module.

## Constant Data Dictionary

### Calibration Constants

This section lists the calibrations used by the module.  For details on calibration constants, refer to the Data Dictionary for the application.

(Note: If no calibrations are used by the design, place the text “None” in the first location in the table)

### Program(fixed) Constants

#### Embedded Constants

All embedded constants whose values are provided in Eng units will be evaluated to the equivalent counts by using the FPM_InitFixedPoint_m() macro within the #define statement.

##### Local

##### Note: RtnLoopTime depends on the rate of the periodic function.

##### Global

This section lists the global constants used by the module.  For details on global constants, refer to the Data Dictionary for the application.

#### Module specific Lookup Tables Constants

(This is for lookup tables (arrays) with fixed values, same name as other tables)

## Software Module Implementation

### Initialization Functions

#### Init: HiLoadStall_Init()

##### Design Rationale

None

##### Module Outputs

None

##### Module Internal

None

### Periodic Functions

#### Per: HiLoadStall_Per1

##### Design Rationale

None

##### Program Flow Start

Rte_Call_HiLoadStall_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

MtrVelCRF_MtrRadpS_T_f32 = Rte_IRead_HiLoadStall_Per1_HighStallLmt _MtrVelCRF_MtrRadpS_f32()

PreLimitForStall_MtrNm_T_f32 = Rte_Iread_HiLoadStall_Per1_HighStallLmt _ PreLimitForStall_MtrNm_f32()

DftStallLimit_Cnt_T_lgc  = Rte_Iread_HiLoadStall_Per1_HighStallLmt _DftStallLimit_Cnt_lgc()

PreLimitForStall_MtrNm_T_u8p8 = FPM_FloatToFixed_m(PreLimitForStall_MtrNm_T_f32, u8p8_T)

##### Determine EOT Thermal Limiting

###### EOT Thermal Algorithm Enable

###### Low Pass Filter

###### EOT Thermal Protection Limit Table

###### Slew Limiting

###### Serial Comm Defeat Sub-Function

##### Store Local copy of outputs into Module Outputs

##### Rte_IWrite_HiLoadStall_Per1_AssistStallLimit_MtrNm_f32(PrevAssistStallLimit_MtrNm_M_f32)

##### Program Flow End

Rte_Call_HiLoadStall_Per1_CP1_CheckpointReached()

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

None

### Local Function/Macro Definitions

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

Inline functions in globalmacros.h are not unit tested.

## Revision Control Log

| Module Inputs (Global Variable Name) | Module Outputs (Global Variable Name) |

| --- | --- |

| MtrVelCRF_MtrRadpS_f32 | AssistStallLimit_MtrNm_f32 |

| PreLimitForStall_MtrNm_f32 |  |

| DftStallLimit_Cnt_lgc |  |

|  |  |

| Variable Name | Resolution | (min) | (max) | Software Segment |

| --- | --- | --- | --- | --- |

| PrevAssistStallLimit_MtrNm_M_f32 | Single Precision Floating Point | 0 | 8.8 | HILOADSTALL_START_SEC_VAR_CLEARED_32 |

| ModPreLimitFiltSV_MtrNm_M_u8p24 | 2^-24 | 0 | 8.8 | HILOADSTALL_START_SEC_VAR_CLEARED_32 |

| ModPreLimit_MtrNm_D_u8p8 | 0.00390625 | 0 | 8.8 | HILOADSTALL_START_SEC_VAR_CLEARED_16 |

| FiltModPreLimit_MtrNm_D_u8p8 | 0.00390625 | 0 | 8.8 | HILOADSTALL_START_SEC_VAR_CLEARED_16 |

| StallLimit_MtrNm_D_u8p8 | 0.00390625 | 0 | 8.8 | HILOADSTALL_START_SEC_VAR_CLEARED_16 |

| Variable Name | Typedef Name | Storage Type | Safety Critical Classification |

| --- | --- | --- | --- |

| None |  |  |  |

| Constant Name |

| --- |

| k_AbsMtrVelBkt_MtrRadps_f32 |

| k_EOTThrmPrtLPFKn_Cnt_u16 |

| t_EOTThrmIndptTbl_MtrNm_u8p8 |

| t_EOTThrmDpntTbl_MtrNm_u8p8 |

| k_EOTThrmSlwLmtStp_MtrNm_f32 |

| Constant Name | Resolution | Value |

| --- | --- | --- |

|  |  |  |

| Constant Name |

| --- |

| D_MTRTRQCMDHILMT_MTRNM_F32 |

| D_ZERO_ULS_F32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

|  |  |  |  |

| Function Name | Task List | Calling Frequency | in which the function is called |

| --- | --- | --- | --- |

| HiLoadStall _Per1 |  | 2ms | All |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| HiLoadStall_Per1() | RTE_START_SEC_AP_HILOADSTALL_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial release | 15DEC11 | M. Story |

| 2 | 2.0 | Changed ranges on M variables for unsigned. Made ModPreLimitFiltSV_Cnt_M_u16 name match code. | 07Jan12 | M. Story |

| 3 | 3.0 | Changes to correct state variable issue found during review.  Updated slew limit logic and replaced local constants with use of global constants.  Variable name updates and added output legal range limit. | 27Jan12 | LWW |

| 4 | 4.0 | Check Point added for Periodic program flow | 21-Sep-2012 | Selva |

|  |  |  |  |  |
