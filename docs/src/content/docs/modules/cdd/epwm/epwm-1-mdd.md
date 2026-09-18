---
title: 'ePWM 1 MDD'
description: 'Converted design document: ePWM 1 MDD'
---

> **Source:** `ePWM/doc/ePWM_1_MDD.docx`  
> **Module:** [ePWM](../../../../cdd/epwm/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module –

## High-Level Description

This module implements functionality with respect to  ES-34B ePWM.  This module implements the ePWM-related register initialization and the motor control and ADC SOCA configuration update subfunctions.

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

ePWM_Read_PWMPeriod_u16

ePWM_Read_DCPhsAComp_u16

ePWM_Read_DCPhsBComp_u16

ePWM_Read_DCPhsCComp_u16

ePWM_Write_ePWM1CMPA_Cnt_u16

ePWM_Write_ePWM1CMPB_Cnt_u16

ePWM_Write_ePWM2CMPA_Cnt_u16

ePWM_Write_ePWM2CMPB_Cnt_u16

ePWM_Write_ePWM3CMPA_Cnt_u16

ePWM_Write_ePWM3CMPB_Cnt_u16

ePWM_Write_ePWM4CMPA_Cnt_u16

ePWM_Write_ePWM4CMPB_Cnt_u16

### Data Hiding Functions

None

### Global Functions/Macros Defined by this Module

#### Global Functions #1

(For detailed info regarding values assigned to registers refer Reference Pdf attached below)

##### Description

### EPWM1

### EPWM2

### EPWM3

### EPWM4

### EPWM7

#### Global Functions #2

##### Design Rationale

PWM Period computed by Pwm_Cdd is read and adjusted.  Adjusted value is used for computations of the motor control PWM CMPA and CMPB values, and for the ADC SOCA update (ePWM4CMPA).

ADC SOCB update  is done in the 2ms loop (see integration manual)  then value (ePWM4CMPB) is read by this function and written to the appropriate buffer.

This function is called by the motor control ISR and so data cannot be transferred via the RTE;  therefore data is read and written via macros and global variables.

Due to timing constraints of the motor control ISR processing, outputs are not limited to their defined ranges before writing.

##### Store Module Inputs to Local copies

ePWM_Read_PWMPeriod_u16(&PWMPeriod_Cnt_T_u16)

ePWM_Read_DCPhsAComp_u16(&DCPhsAComp_Cnt_T_u16)

ePWM_Read_DCPhsBComp_u16(&DCPhsBComp_Cnt_T_u16)

ePWM_Read_DCPhsCComp_u16(&DCPhsCComp_Cnt_T_u16)

ePWM_Read_ePWM4CMPB_Cnt_u16(&ePWM4CMPB_Cnt_T_u16)

##### Processing

##### Store Local copy of outputs into Module Outputs

### Local Functions/Macros Used by this MDD only

#### Local Macro #1

##### Description

Disables the motor control EPWM outputs; forces A and B outputs low on all three motor control ePWMs (ePWM1, ePWM2, ePWM3)  (Refer the included register reference for more details of register)

ePWM1->AQCSFRC = 5U

ePWM1->DBCTL &= 0xFFFFFFFCU

ePWM2->AQCSFRC = 5U

ePWM2->DBCTL &= 0xFFFFFFFCU

ePWM3->AQCSFRC = 5U

ePWM3->DBCTL &= 0xFFFFFFFCU

#### Local Macro #2

##### Description

Enables the motor control EPWM outputs;  allows A and B outputs to be driven high/low as configured in register initialization (core initialization subfunction) and using the CMPA and CMPB values computed in the motor control configuration subfunction.  (Refer the included register reference for more details of register)

ePWM1->AQCSFRC = 0U;

ePWM1->DBCTL |= 3U;

ePWM2->AQCSFRC = 0U;

ePWM2->DBCTL |= 3U;

ePWM3->AQCSFRC = 0U;

ePWM3->DBCTL |= 3U;

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init:

##### Design Rationale

This component does not have an RTE Init function, however ePWM pin mux  settings are configured in the integration project and initialized in (patched) generated  code.  See the integration manual.

##### Module Outputs

None

##### Module Internal

None

##### Initialize EPWM Direction Register

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

### Execution Rates for sub-modules called by the Subroutine

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

QAC for the generated files not corrected.

## Reference

Register Reference

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| PWMPeriod_Cnt_u16 | PWMPeriod_Cnt_u16 | ePWM1CMPA_Cnt_u16 |

| DCPhsAComp_Cnt_u16 | DCPhsAComp_Cnt_u16 | ePWM1CMPB_Cnt_u16 |

| DCPhsBComp_Cnt_u16 | DCPhsBComp_Cnt_u16 | ePWM2CMPA_Cnt_u16 |

| DCPhsCComp_Cnt_u16 | DCPhsCComp_Cnt_u16 | ePWM2CMPB_Cnt_u16 |

| ePWM4CMPB_Cnt_u16 | ePWM4CMPB_Cnt_u16 | ePWM3CMPA_Cnt_u16 |

|  |  | ePWM3CMPB_Cnt_u16 |

|  |  | ePWM4CMPA_Cnt_u16 |

|  |  | ePWM4CMPB_Cnt_u16 |

|  |  |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| Constant Name |

| --- |

| k_ADCTrig1Offset_Cnt_s16 |

| k_PwmDeadBand_Cnt_u16<br/>k_PwmRelay_Cnt_u16 |

| Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) |  |

| --- | --- | --- | --- | --- |

|  |  |  |  |  |

| Constant Name |

| --- |

| None |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | ePWM_Init1 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | None |  |  |  |  |

| Function Name | ePWM_Per1 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | None |  |  |  |  |

| Function Name | ePWM_DisableOutputs | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | None |  |  |  |  |

| Function Name | ePWM_EnableOutputs | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | None |  |  |  |  |

| Data | Value |

| --- | --- |

| None |  |

| Global Function Name | Calling Frequency | Function in which the function is called |

| --- | --- | --- |

| ePWM_Init1 | On Event | ECU start up |

| ePWM_Per1 | On Event | Motor Control ISR subroutine |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| ePWM_Init1 | EPWM_START_SEC_CODE |

| ePWM_Per1 | EPWM_START_SEC_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1.0 | Initial Version ( FDD 34B) –Shutdown Mech not included | 18-Feb-13 | Selva |

| 2 | Anomaly 4605 – changed active state of ePWM modules 1-3 | 11-Mar-13 | OT |

| 3 | Updated to FDD 34B v003 | 18-Jun-13 | OT/Selva |

| 4 | Updated to FDD 34B v005 | 07-Apr-14 | Selva |

| 5 | Updated to ES-34B v008 | 25-Jan-15 | KMC |

|  |  |  |  |
