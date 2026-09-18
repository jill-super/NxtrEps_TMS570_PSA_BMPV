---
title: 'Sweep2 MDD'
description: 'Converted design document: Sweep2 MDD'
---

> **Source:** `Sweep/doc/Sweep2_MDD.docx`  
> **Module:** [Sweep](../../../../asw/sweep/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module – Sweep2

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

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

none

### Local Functions/Macros Used by this MDD only

none

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

### Initialization Functions

None

### Periodic Functions

##### Design Rationale

None

##### Store Module Inputs to Local copies Fault Recovery Functions

See below

##### Description

##### Store Local copy of outputs into Module Outputs

See above

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

| InputMtrTrq_MtrNm_f32 | InputMtrTrq_MtrNm_f32 | OutputMtrTrq_MtrNm_f32 |

| Variable Name | Datatype | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment<br/>{Data Type} |

| --- | --- | --- | --- | --- | --- |

| SweepModeEn_Cnt_M_lgc | Boolean | N/A | FALSE | TRUE |  |

| SweepConfig_Cnt_M_u16 | Uint16 | 1 | 0 | FULL |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

|  |  |  |  |  |

| Constant Name |

| --- |

|  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_SWEEPMTRTRQ_CNT_U16 | 1 | Uint16 | 1 |

| Constant Name |

| --- |

| D_FALSE_CNT_LGC |

| D_ZERO_ULS_F32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

|  |  |  |  |

| Data | Value |

| --- | --- |

| InputMtrTrq_MtrNm_f32 | 0 |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| Sweep2_Per1 | 2ms | RTE_AP_SWEEP2_APPL_CODE |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| Sweep2_Per1 | RTE_AP_SWEEP2_APPL_CODE |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1 | Initial MDD version | 25-Mar-13 | VK |
