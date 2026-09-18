---
title: 'Fee Interface MDD'
description: 'Converted design document: Fee Interface MDD'
---

> **Source:** `NvMMgr/doc/Fee_Interface_MDD.docx`  
> **Module:** [NvMMgr](../../../../services/nvmmgr/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module  --

## High-Level Description

This module contains the specific interfacing functions that are needed for TI’s Fee Driver.  This includes an initialization routine and configurable trusted function interfaces that allow compatibility with the NvM/MemIf BSW.

## Figures

### Diagram – Function Data Sharing

N/A

#### Diagram – Function (Name)

N/A

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

<None>

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

#### Global Functions Defined if BC_FEEIF_ECUSTARTUPTRUSTED == STD_OFF

##### TWrapC_FeeIf_Init

This is the client (non-trusted) side of the FeeIf_Init Trusted Function

###### Description

##### TRUSTED_TWrapS_FeeIf_Init

This is the server (trusted) side of the FeeIf_Init Trusted Function

###### Description

##### TWrapC_Fee_MainFunction

This is the client (non-trusted) side of the Fee_MainFunction Trusted Function

###### Description

##### TRUSTED_TWrapS_Fee_MainFunction

This is the server (trusted) side of the Fee_MainFunction Trusted Function

###### Description

#### Global Functions Defined if BC_FEEIF_NVMTRUSTED == STD_OFF

##### TWrapC_Fee_Read

This is the client (non-trusted) side of the Fee_Read Trusted Function

###### Description

##### TRUSTED_TWrapS_Fee_Read

This is the server (trusted) side of the Fee_Read Trusted Function

###### Description

##### TWrapC_Fee_Write

This is the client (non-trusted) side of the Fee_Write Trusted Function

###### Description

##### TRUSTED_TWrapS_Fee_Write

This is the server (trusted) side of the Fee_Write Trusted Function

###### Description

##### TWrapC_Fee_EraseImmediateBlock

This is the client (non-trusted) side of the Fee_EraseImmediateBlock Trusted Function

###### Description

##### TRUSTED_TWrapS_Fee_EraseImmediateBlock

This is the server (trusted) side of the Fee_EraseImmediateBlock Trusted Function

###### Description

##### TWrapC_Fee_InvalidateBlock

This is the client (non-trusted) side of the Fee_InvalidateBlock Trusted Function

###### Description

##### TRUSTED_TWrapS_Fee_InvalidateBlock

This is the server (trusted) side of the Fee_InvalidateBlock Trusted Function

###### Description

##### TWrapC_Fee_Cancel

This is the client (non-trusted) side of the Fee_Cancel Trusted Function

###### Description

##### TRUSTED_TWrapS_Fee_Cancel

This is the server (trusted) side of the Fee_Cancel Trusted Function

###### Description

##### TWrapC_Fee_GetStatus

This is the client (non-trusted) side of the Fee_GetStatus Trusted Function

###### Description

##### TRUSTED_TWrapS_Fee_GetStatus

This is the server (trusted) side of the Fee_GetStatus Trusted Function

###### Description

##### TWrapC_Fee_GetJobResult

This is the client (non-trusted) side of the Fee_GetJobResult Trusted Function

###### Description

##### TRUSTED_TWrapS_Fee_GetJobResult

This is the server (trusted) side of the Fee_GetJobResult Trusted Function

###### Description

##### TWrapC_TI_Fee_SuspendResumeErase

This is the client (non-trusted) side of the TI_Fee_SuspendResumeErase Trusted Function

###### Description

While the command type is a uint8, the actual type is TI_Fee_EraseCommandType.

##### TRUSTED_TWrapS_TI_Fee_SuspendResumeErase

This is the server (trusted) side of the TI_Fee_SuspendResumeErase Trusted Function

###### Description

### Local Functions/Macros Used by this MDD only

#### Local Function #1

##### Description

N/A

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

(Note: For multiple init functions, insert new headers at the “Header 2” level – subset of “5.1 Initialization Functions” and follow the same sub-section design shown below)

#### Init: FeeIf_Init

##### Design Rationale

This function initializes the FEE driver.  After the FEE BSW initialization, the Fee_MainFunction is required to be called until the FEE reports a status that is not busy.  This is required because the NvM/MemIf BSWs currently make the assumption that the FEE driver will not be busy at initialization; however, the FEE driver may be busy if it has to finish any virtual sector swapping that may have been interrupted (i.e. the NvM currently can issue a new FEE command to the driver without first checking the FEE internal status the very first time after a new power cycle).

##### Module Outputs

None

##### Module Internal

None

##### Processing

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

See Integration Manual

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

FeeIf_Init currently does not implement any of the available error recovery mechanisms in the case of an issue with the FEE driver.  Additionally, it doesn’t set any faults or report out any errors to the user if one of these FEE memory errors occur.

For the provided trusted functions, there is currently neither checking on the passed parameters nor checking on the caller of the trusted function.  It was unclear during the current design if either of these was necessary.

This MDD is currently missing some datatype definition and ranges (specifically for the trusted function call wrappers).  The assumption was that these would not need to be unit tested and were for design documentation only.

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

|  |  |  |

|  |  |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

|  |  |  |  |  |

|  |  |  |  |  |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

|  |  |  |  |  |

|  |  |  |  |  |

| Constant Name |

| --- |

| <None> |

|  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| <None> |  |  |  |

|  |  |  |  |

| Constant Name |

| --- |

| <None> |

|  |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | TWrapC_FeeIf_Init | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TRUSTED_TWrapS_FeeIf_Init | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | FunctionIndex | TrustedFunctionIndexType |  |  |  |

|  | FunctionParams | TrustedFunctionParameterRefType |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TWrapC_Fee_MainFunction | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TRUSTED_TWrapS_Fee_MainFunction | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | FunctionIndex | TrustedFunctionIndexType |  |  |  |

|  | FunctionParams | TrustedFunctionParameterRefType |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TWrapC_Fee_Read | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | BlockNumber | uint16 |  |  |  |

|  | BlockOffset | uint16 |  |  |  |

|  | DataBufferPtr | uint8* |  |  |  |

|  | Length | uint16 |  |  |  |

| Return Value | myargs.TWrapS_Fee_Read_args.os_result | Std_ReturnType |  |  |  |

| Function Name | TRUSTED_TWrapS_Fee_Read | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | FunctionIndex | TrustedFunctionIndexType |  |  |  |

|  | FunctionParams | TrustedFunctionParameterRefType |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TWrapC_Fee_Write | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | BlockNumber | uint16 |  |  |  |

|  | DataBufferPtr | uint8* |  |  |  |

| Return Value | myargs.TWrapS_Fee_Write_args.os_result | Std_ReturnType |  |  |  |

| Function Name | TRUSTED_TWrapS_Fee_Write | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | FunctionIndex | TrustedFunctionIndexType |  |  |  |

|  | FunctionParams | TrustedFunctionParameterRefType |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TWrapC_Fee_EraseImmediateBlock | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | BlockNumber | uint16 |  |  |  |

|  |  |  |  |  |  |

| Return Value | myargs.TWrapS_Fee_EraseImmediateBlock_args.os_result | Std_ReturnType |  |  |  |

| Function Name | TRUSTED_TWrapS_Fee_EraseImmediateBlock | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | FunctionIndex | TrustedFunctionIndexType |  |  |  |

|  | FunctionParams | TrustedFunctionParameterRefType |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TWrapC_Fee_InvalidateBlock | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | BlockNumber | uint16 |  |  |  |

|  |  |  |  |  |  |

| Return Value | myargs.TWrapS_Fee_InvalidateBlock_args_args.os_result | Std_ReturnType |  |  |  |

| Function Name | TRUSTED_TWrapS_Fee_InvalidateBlock | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | FunctionIndex | TrustedFunctionIndexType |  |  |  |

|  | FunctionParams | TrustedFunctionParameterRefType |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TWrapC_Fee_Cancel | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TRUSTED_TWrapS_Fee_Cancel | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | FunctionIndex | TrustedFunctionIndexType |  |  |  |

|  | FunctionParams | TrustedFunctionParameterRefType |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TWrapC_Fee_GetStatus | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | myargs.TWrapS_Fee_GetStatus_args.os_result | uint8 |  |  |  |

| Function Name | TRUSTED_TWrapS_Fee_GetStatus | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | FunctionIndex | TrustedFunctionIndexType |  |  |  |

|  | FunctionParams | TrustedFunctionParameterRefType |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TWrapC_Fee_GetJobResult | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | None |  |  |  |  |

|  |  |  |  |  |  |

| Return Value | myargs.TWrapS_Fee_GetJobResult_args.os_result | uint8 |  |  |  |

| Function Name | TRUSTED_TWrapS_Fee_GetJobResult | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | FunctionIndex | TrustedFunctionIndexType |  |  |  |

|  | FunctionParams | TrustedFunctionParameterRefType |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TWrapC_TI_Fee_SuspendResumeErase | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | Command | uint8 | 0 | 1 |  |

| Return Value | N/A |  |  |  |  |

| Function Name | TRUSTED_TWrapS_TI_Fee_SuspendResumeErase | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | FunctionIndex | TrustedFunctionIndexType |  |  |  |

|  | FunctionParams | TrustedFunctionParameterRefType |  |  |  |

| Return Value | N/A |  |  |  |  |

| Function Name | None | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed |  |  |  |  |  |

|  |  |  |  |  |  |

| Return Value |  |  |  |  |  |

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

|  |  |

| Name of Sub Module | Software Segment |

| --- | --- |

|  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1 | Initial version | 07/15/13 | LWW |

| 2 | 1.1.1 | Added suspend/resume erase functions | 11/04/14 | KJS |

| 3 | 1.1.2 | Added FEE Single bit ECC correction | 12/15/14 | PS |

| 4 | 3.1.1 | Updated FEE component and removed Nexteer FEE ECC workaround | 1/27/15 | PS |
