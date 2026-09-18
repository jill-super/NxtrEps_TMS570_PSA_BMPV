---
title: 'Adc Common MDD'
description: 'Converted design document: Adc Common MDD'
---

> **Source:** `Adc/doc/Adc_Common_MDD.docx`  
> **Module:** [Adc](../../../../ecuab/adc/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module -- Adc Core

## High-Level Description

The Adc Common module provides “stateless” application context independent functions which provide functionality required by both the Adc and Adc2 modules.  In order to operate in any given application, the function design must not write to any fixed static variable location, unless it is in Globally shared memory.  All static variable writes outside of Globally shared memory must be performed via pointer access where the caller provides the pointer reference to allowed writable memory in the application context from with the caller is executing.

The motivation for creating core functions is to reduce duplication and testing of common code design.

## Figures

### Component Diagram

None

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

None

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

#### Offset Calibration

Perform the ADC Calibration and Storing of offset.

##### Calibration Offset

### Local Functions/Macros Used by this MDD only

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

None

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

### Transition Functions

None

## Execution Requirements

### Execution Sequence of the Module

No integration scheduling required. The only service offered by this module has a fixed scheduling within the Adc subsystem.

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

INLINE functions defined in “GlobalMacro.h” are not unit tested

## Revision Control Log

| Module Inputs | Module Outputs |

| --- | --- |

| None | None |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Constant Name |

| --- |

| None |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_NUMOFADCCALREADS_CNT_U8 | 1 | Counts |  |

| Constant Name |

| --- |

| D_FALSE_CNT_LGC |

| D_TRUE_CNT_LGC |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | ADCOffsetCalibration | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | adcREG | adcctrlregs_t* | FULL | FULL |  |

|  |  |  |  |  |  |

| Return Value | Status_Cnt_T_u08 | uint8 | FULL | FULL |  |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| None |  |  |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| N/A |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| ADCOffsetCalibration | ADC_START_SEC_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial version | 24Apr13 | Selva |

|  |  |  |  |  |
