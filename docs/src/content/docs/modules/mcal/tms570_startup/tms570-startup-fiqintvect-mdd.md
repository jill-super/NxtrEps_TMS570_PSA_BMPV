---
title: 'TMS570 Startup FiqIntVect MDD'
description: 'Converted design document: TMS570 Startup FiqIntVect MDD'
---

> **Source:** `TMS570_Startup/doc/TMS570_Startup_FiqIntVect_MDD.docx`  
> **Module:** [TMS570_Startup](../../../../mcal/tms570_startup/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## High-Level Description

fiqintvect  provides the assembly language fiq handling function. The function loads the program counter with the value of the FIQ Interrupt Vector Register, which contains the address of the ISR with the highest priority pending FIQ request.

## Figures

### Diagram – Function Data Sharing

No Shared Data

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

<None>

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

NOTE that all global functions in this module must be assembled in ARM mode.  Therefore the .asm source file includes the .arm directive at the beginning of the file, applying the directive to all functions in the file.

#### Global Function #1

##### Design Rationale

This function is required when more than one FIQ is configured in the system.  When only one FIQ is configured, its ISR can be directly configured in DaVinci as the FIQ Handler.  (Alternatively, the _fiqhandler function could be configured and its code changed to branch to the one FIQ ISR.)  When there are multiple FIQs, the _fiqhandler function is needed so that the one handler configured in DaVinci will go to the correct ISR address as found in the processor FIQ Interrupt Vector Register.

##### Description

Loads the program counter with the value of the FIQ Interrupt Vector Register, which contains the address of the ISR with the highest priority pending FIQ request.

### .def	_fiqhandler

### .asmfunc

### _fiqhandler

### ldr		r8, fiqvectreg

### ldr		pc,  [r8]

### fiqvectreg	.word	0xFFFFFE74

### .endasmfunc

### Local Functions/Macros Used by this MDD only

None

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

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

### Serial Communication Functions

None

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

None

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| <None> | <None> | <None> |

|  |  |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| <None> |  |  |  |  |

|  |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| <None> |  |  |  |  |

|  |  |  |  |  |

| Constant Name |

| --- |

| <None> |

|  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| <None> |  |  |  |

| Constant Name |

| --- |

| <None> |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| <None> |  |  |  |

| Function Name | _fiqhandler | Type | Dir. | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |  |

| Return Value | None |  |  |  |  |  |

| Data | Value |

| --- | --- |

| <None> |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| <None> |  |  |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| <None> |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| _fiqhandler | N/A |

| Name of Local Function | Software Segment |

| --- | --- |

| None |  |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial Revision of MDD | 6/10/2013 | KMC |
