---
title: 'Quadrant Detection MDD'
description: 'Converted design document: Quadrant Detection MDD'
---

> **Source:** `MtrCtrl_CM/doc/Quadrant_Detection_MDD.docx`  
> **Module:** [MtrCtrl_CM](../../../../asw/mtrctrl_cm/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module  --

## High-Level Description

This module takes the cumulative motor position and determines the motor direction (using a previously saved state variable and a calibration constant for hysteresis).  It then computes the torque command sign from the scaled torque command and uses both of these values to determine the motor quadrant.

## Figures

### Component Diagram

#### Diagram – Function QuadDet_Per1

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

Abs_f32_m()

Sign_f32_m()

### Data Hiding Functions

### Global Functions/Macros Defined by this Module

None

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

None

### Periodic Functions

#### Per: _Per1

##### Design Rationale

None

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

MtrTrqCmdScl_MtrNm_T_f32 = Rte_IRead_QuadDet_Per1_MtrTrqCmdScl_MtrNm_f32();

CumMtrPos_Deg_T_f32 = Rte_IRead_QuadDet_Per1_MRFCumMtrPos_Deg_f32();

##### Determine Motor Direction

##### Determine Instantaneous Torque Command Sign

##### Determine Motor Quadrant

##### Store Local copy of outputs into Module Outputs

Rte_IWrite_QuadDet_Per1_InstMtrDir_Cnt_s(PrevInstMtrDir_Cnt_M_s);

Rte_IWrite_QuadDet_Per1_MtrQuad_Cnt_u(MtrQuad_Cnt_T_u);

##### Program Flow End

N/A

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

QuadDet_Per1 executes every 2 milliseconds.

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

- INLINE functions defined in globalmacro.h are not unit testedRevision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| MtrTrqCmdScl_MtrNm_f32 | MtrTrqCmdScl_MtrNm_f32 | InstMtrDir_Cnt_s |

| MRFCumMtrPos_Deg_f32 | MRFCumMtrPos_Deg_f32 | MtrQuad_Cnt_u |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| MtrTrqCmdSign_Cnt_D_s | 1 | -1, 1 | -1, 1 | AP_QUADRANTDETECT_VAR_NOINIT |

| PrevCumMtrPos_Deg_M_f32 | Single Precision Float | -1 | 1 | AP_QUADRANTDETECT_VAR_INIT |

| PrevInstMtrDir_Cnt_M_s | 1 | -1 | 1 | AP_QUADRANTDETECT_VAR_INIT |

|  |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Constant Name |

| --- |

| k_InstMtrDirHyst_Deg_f32 |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_CUMMTRPOSLOLMT_DEG_F32 | Single Precision Float | Degrees | min value of  MRFCumMtrPos_Deg_f32 |

| D_CUMMTRPOSHILMT_DEG_F32 | Single Precision Float | Degrees | max value of  MRFCumMtrPos_Deg_f32 |

| D_MTRTRQCMDTOL_MTRNM_F32 | Single Precision Float | MtrNm | 0.00390625 |

| Constant Name |

| --- |

| D_QUADRANT1_CNT_U |

| D_QUADRANT2_CNT_U |

| D_QUADRANT3_CNT_U |

| D_QUADRANT4_CNT_U |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Data | Value |

| --- | --- |

| Rte_InitValue_InstMtrDir_Cnt_s08 | 0 |

| Rte_InitValue_MRFCumMtrPos_Deg_f32 | 0 |

| Rte_InitValue_MRFMtrTrqCmdScl_MtrNm_f32 | 0 |

| Rte_InitValue_MtrQuad_Cnt_u08 | 1 |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| QuadDet_Per1 | 2 ms | WARM INIT, OPERATE, DISABLE, OFF |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| <None> |  |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1 | Initial MDD for component based design | 23-Dec-11 | O.T. |

|  |  |  |  |  |
