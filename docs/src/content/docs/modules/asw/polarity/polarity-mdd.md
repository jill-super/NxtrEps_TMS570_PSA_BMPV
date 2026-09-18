---
title: 'Polarity MDD'
description: 'Converted design document: Polarity MDD'
---

> **Source:** `Polarity/doc/Polarity_MDD.docx`  
> **Module:** [Polarity](../../../../asw/polarity/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module --

## High-Level Description

This module implements the polarity assignments for the EPS systems to allow for various configurations of input and output signals for proper alignment.

## Figures

### Diagram – Component Diagram

### Diagram – Function Data Sharing

No shared data.

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

(This is for lookup tables (arrays) with fixed values, same name as other tables)

## Functions/Macros used by the Sub-Modules

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules are identified below,

None

### Data Hiding Functions

### Global Functions/Macros Defined by this Module

N/A

### Local Functions/Macros Used by this MDD only

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init: _Init1

##### Design Rationale

During cold initialization, set all output ports to their values based on the stored polarity calibration.

##### Program Flow Start

N/A

##### Store Module Inputs to Local Copies

N/A

##### Processing

##### Store Local copy of outputs into Module Outputs

N/A

##### Program Flow End

N/A

### Serial Communication Functions

#### SCom: Polarity_SCom_ReadPolarity

##### Design Rationale

Read and return current polarity calibration to the testing tool.

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

N/A

##### (Processing of function)

##### Store Local copy of outputs into Module Outputs

N/A

##### Program Flow End

N/A

#### SCom: Polarity_SCom_SetPolarity

#### Design Rationale

##### Program Flow Start

N/A

##### Store Module Inputs to Local copies

N/A

##### Processing

##### Store Local copy of outputs into Module Outputs

N/A

##### Program Flow End

N/A

## Execution Requirements

### Execution Sequence of the Module

N/A

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

## Additional Comments

The polarity bits for hand wheel torque, hand wheel position, motor position, and motor velocity (bits 0 - 4) are assumed to be used at the “sensor” level to place the signals in the proper orientation for use within the ECU. For example, hand wheel torque bit should be used to get the torque signals into the Nexteer CRF described in the polarity FDD-25.

Porting a signal from CRF to MRF, or from MRF to CRF, shall be done with the assist assembly polarity bit (bit 5).

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

|  |  | HwTrqPolarity_Cnt_s08 |

|  |  | HwPosPolarity_Cnt_s08 |

|  |  | MtrPosPolarity_Cnt_s08 |

|  |  | MtrVelPolarity_Cnt_s08 |

|  |  | MtrElecMechPolarity_Cnt_s08 |

|  |  | AssistAssyPolarity_Cnt_s08 |

|  |  | SysC_ MtrElecMechPolarity_Cnt_s32 |

| Variable Name |  | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- | --- |

|  |  |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

|  |  |  |  |  |

|  |  |  |  |  |

| Constant Name |

| --- |

|  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

|  |  |  |  |

|  |  |  |  |

| D_HWTRQPOL_CNT_ | 1 | Counts | 0x01 |

| D_HWPOSPOL_CNT_ | 1 | Counts | 0x02 |

| D_MTRPOSPOL_CNT_ | 1 | Counts | 0x04 |

| D_MTRVELPOL_CNT_ | 1 | Counts | 0x08 |

| D_ASSTASSEMPOL_CNT_ | 1 | Counts | 0x10 |

| D_MTRELECMECHPOL_CNT_ | 1 | Counts | 0x20 |

|  |  |  |  |

|  |  |  |  |

|  |  |  |  |

| Constant Name |

| --- |

|  |

|  |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Data | Value |

| --- | --- |

| AssistAssyPolarity_Cnt_s08 | 0 |

| HwPosPolarity_Cnt_s08 | 0 |

| HwTrqPolarity_Cnt_s08 | 0 |

| MtrElecMechPolarity_Cnt_s08 | 0 |

| MtrPosPolarity_Cnt_s08 | 0 |

| MtrVelPolarity_Cnt_s08 | 0 |

|  |  |

|  |  |

|  |  |

|  |  |

|  |  |

|  |  |

|  |  |

| Function Name | Polarity_SCom_ReadPolarity | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed |  |  | FULL | FULL |

| Return Value | N/A |  |  |  |

| Function Name | Polarity_SCom_SetPolarity | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed |  |  | FULL | FULL |

| Return Value |  |  |  |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| Polarity_Init1 | Executed Once after RTE is started | ColdInit |

|  |  |  |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| Polarity_SCom_ReadPolarity |  |

| Polarity_SCom_SetPolarity |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| Polarity_Init1 |  |

|  |  |

| Polarity_SCom_ReadPolarity |  |

| Polarity_SCom_SetPolarity |  |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1 | Initial MDD | 23May11 | NRAR |

| 2 | 2 | Carried over from for component based design | 14Nov11 | JWW |

| 3 | 3 | Updates and initial release for component based design | 21Apr2012 | KJS |

| 4 | 4 | Update for GSOD redundant output – FDDv006 | 22-Oct-12 | JWJ |

|  |  |  |  |  |
