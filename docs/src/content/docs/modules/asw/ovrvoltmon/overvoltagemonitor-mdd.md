---
title: 'OverVoltageMonitor MDD'
description: 'Converted design document: OverVoltageMonitor MDD'
---

> **Source:** `OvrVoltMon/doc/OverVoltageMonitor_MDD.docx`  
> **Module:** [OvrVoltMon](../../../../asw/ovrvoltmon/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module -- OverVoltageMonitor

Overvoltage monitor function operates so that when an overvoltage condition occurs on any of the CPU supply voltages the motor inverter operation is shutdown before the CPU can respond.

## High-Level Description

## Figures

### Diagram – Function Data Sharing

#### Diagram – Function (Name)

## Variable Data Dictionary

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

(Note: Full variable names required in table.)

(Note: All global variables including End Of Line data used should be shown here)

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

### Data Hiding Functions

Rte_Call_NxtrDiagMgr_SetNTCStatus

### Global Functions/Macros Defined by this Module

#### Global Function #1

##### Description

### Local Functions/Macros Used by this MDD only

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

(Note: For multiple init functions, insert new headers at the “Header 2” level – subset of “5.1 Initialization Functions” and follow the same sub-section design shown below)

#### None

### Periodic Functions

#### Per: OvrVoltMon_Per1

##### Design Rationale

##### Program Flow Start

Rte_Call_OvrVoltMon_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

##### Processing

##### Store Local copy of outputs into Module Outputs

N/A

##### Program Flow End

Rte_Call_OvrVoltMon_Per1_CP1_CheckpointReached()

### Fault Recovery Functions

### Shutdown Functions

### Interrupt Functions

### Serial Communication Functions

## Execution Requirements

### Execution Sequence of the Module

(Describe in words relevant details about the execution sequence of the different sub modules.)

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

|  |  |  |

|  |  |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

|  | 1 | 1 | 512 | OVRVOLTMON_START_SEC_VAR_CLEARED_16 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

|  |  |  |  |  |

|  |  |  |  |  |

| Constant Name |

| --- |

| k_CPUSupplyOV_Cnt_Str |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| None |  |  |  |

| Constant Name |

| --- |

| None |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name |  | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed |  |  |  |  |

|  |  |  |  |  |

| Return Value |  |  |  |  |

| Data | Value |

| --- | --- |

|  |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| OvrVoltMon_Per1 | 2ms | OPERATE |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| N/A |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| OvrVoltMon_per1 | RTE_SA_OVRVOLTMON_APPL_CODE |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial AutoSAR Release | 10-July-12 | NRAR |

| 2 | 2.0 | Changed from PSTEP to NSTEP when no fault | 29-July-12 | NRAR |

| 3 | 3.0 | MDD version update | 30-July-12 | NRAR |

| 4 | 4 | Updated states diagnostic is run in | 07-Aug-12 | LWW |

| 5 | 5 | Checkpoints added and mempmap macros corrected | 27-sep-12 | Selva |

|  |  |  |  |  |
