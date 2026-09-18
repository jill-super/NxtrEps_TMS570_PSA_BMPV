---
title: 'Controller Temperature MDD'
description: 'Converted design document: Controller Temperature MDD'
---

> **Source:** `CtrlTemp/doc/Controller_Temperature_MDD.docx`  
> **Module:** [CtrlTemp](../../../../asw/ctrltemp/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module -- Controller Temperature

## High-Level Description

This module monitors the controller’s temperature sensor output, filters that output, and checks whether the output is within a lower and upper limit.

## Figures

### Diagram – Function Data Sharing

This diagram shows all data that is shared between functions within the module.

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

#### Init: CtrlTemp_Init1

##### Design Rationale

None

##### Module Outputs

##### Module Internal

Rte_IRead_CtrlTemp__TemperatureADC_Volt_f32)

CtrlTemp_DegC__f32 = (– k_TempSnsrOffset_Volts_f32) * k_TempSnsrScaling_DegpVolt_f32

CtrlTemp_DegC_M_f32 = Limit_m(CtrlTemp_DegC__f32, D_CTRLTEMPLOLMT_DEGC_F32, D_CTRLTEMPHILMT_DEGC_F32)

CtrlLPF_Init_f32_m(CtrlTemp_DegC_M_f32, k_TempSnsrLPFKn_Hz_f32, D_2MS_SEC_F32, &CtrlTempSV_M_str)

Rte_IWrite_CtrlTemp_Init1_FiltMeasTemp_DegC_f32 (CtrlTemp_DegC_M_f32)

### Periodic Functions

#### Per: CtrlTemp_Per1

##### Design Rationale

None

##### Program Flow Start

##### Rte_Call_CtrlTemp_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

DiagStsTempRdPrf_Cnt_T_lgc = Rte_Iread_CtrlTemp_Per1_DiagStsTempRdPrf_Cnt_lgc();

_Volts_T_f32 = Rte_Iread_CtrlTemp_Per1_TemperatureADC_Volt_f32()

CtrlTemp_DegC_T_f32 = (_Volts_T_f32 – k_TempSnsrOffset_Volts_f32) * k_TempSnsrScaling_DegpVolt_f32

##### (Processing of function)………

###### Calculate Temperature

##### Store Local copy of outputs into Module Outputs

CtrlTemp_DegC_T_f32 = Limit_m(CtrlTemp_DegC_T_f32, D_CTRLTEMPLOLMT_DEGC_F32, D_CTRLTEMPHILMT_DEGC_F32);

Rte_Iwrite_CtrlTemp_Per1_FiltMeasTemp_DegC_f32 (CtrlTemp_DegC_T_f32 );

##### Program Flow End

Rte_Call_CtrlTemp_Per1_CP1_CheckpointReached()

#### Per: CtrlTemp_Per2

##### Design Rationale

None

##### Program Flow Start

##### Rte_Call_CtrlTemp_Per2_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

##### (Processing of function)………

##### Store Local copy of outputs into Module Outputs

##### Program Flow End

Rte_Call_CtrlTemp_Per2_CP1_CheckpointReached()

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

None

### Local Function/Macro Definitions

None

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

None

## Revision Control Log

| Module Inputs (Global Variable Name) | Module Outputs (Global Variable Name) |

| --- | --- |

| DiagStsTempRdPrf_Cnt_lgc | FiltMeasTemp_DegC_f32 |

| TemperatureADC_Volt_f32 |  |

|  |  |

| Variable Name | Resolution | (min) | (max) | Software Segment |

| --- | --- | --- | --- | --- |

| CtrlTempSV_M_str | LPF32KSV_Str |  |  | CTRLTEMP_START_SEC_VAR_CLEARED_UNSPECIFIED |

| CtrlTempSV_M_str .K_Uls_f32 | Single Precision Floating Point |  |  |  |

| CtrlTempSV_M_str .SV_Uls_f32 | Single Precision Floating Point |  |  |  |

| CtrlTemp_DegC_M_f32 | Single Precision Floating Point |  |  | CTRLTEMP_START_SEC_VAR_CLEARED_32 |

| CtrlTempErrorAcc_Cnt_M_u16 | 1 |  |  | CTRLTEMP_START_SEC_VAR_CLEARED_16 |

| CtrlTempFiltOut_DegC_D_f32 | Single Precision Floating Point |  |  | CTRLTEMP_START_SEC_VAR_CLEARED_32 |

| Variable Name | Typedef Name | Storage Type | Safety Critical Classification |

| --- | --- | --- | --- |

| None |  |  |  |

| Constant Name |

| --- |

| k_TempSnsrFiltDft_Cnt_lgc |

| k_TempSnsrLPFKn_Hz_f32 |

| k_TempSnsrDefVal_DegC_f32 |

| k_TempSensDiag_Cnt_str |

| k_TempSensLowLimit_DegC_f32 |

| k_TempSensHighLimit_DegC_f32 |

| k_TempSnsrScaling_DegpVolt_f32 |

| k_TempSnsrOffset_Volts_f32 |

|  |

|  |

| Constant Name | Resolution | Value |

| --- | --- | --- |

| D_CTRLTEMPLOLMT_DEGC_F32 | Single Precision Floating Point | -50.0 |

| D_CTRLTEMPHILMT_DEGC_F32 | Single Precision Floating Point | 150.0 |

| Constant Name |

| --- |

| D_2MS_SEC_F32 |

|  |

|  |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

|  |  |  |  |

| Function Name | Task List | Calling Frequency | in which the function is called |

| --- | --- | --- | --- |

| CtrlTemp_Init1() |  | Once | Once after RTE is started |

| CtrlTemp_Per1() |  | 2ms | All |

| CtrlTemp_Per2() |  | 100ms | All |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| CtrlTem_Init1() | RTE_SA_CTRLTEMP_APPL_CODE |

| CtrlTem_Per1() | RTE_SA_CTRLTEMP_APPL_CODE |

| CtrlTem_Per2() | RTE_SA_CTRLTEMP_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1.0 | Initial release | 18MAY11 | SAH |

| 2 | 2.0 | Added Reduced Performace temperature selecture per #SF-6 001 | 02DEC11 | M. Story |

| 3 | 3.0 | Anomaly 2995 Limits not set correctly | 29FEB12 | M. Story |

| 4 | 4.0 | Anomaly 2994 use CntrlTemp_DegC_T_f32 temporary variable internal to the Per1 function | 03MAR12 | M. Story |

| 5 | 5.0 | Updated component to FDD SF-06 revision 4 | 16May12 | KJS |

| 6 | 6.0 | Updated floating point filter structure with K and SV ranges | 12Jun12 | KJS |

| 7 | 7.0 | Anomaly 3505 Use output from LPF for diagnostics. | 23Aug12 | Srikanth |

| 8 | 8.0 | Added watchdog checkpoints. | 16 Sept 12 | BWL |

| 9 | 9.0 | Added “Variables” missing from Module internal variable and their software segment | 18 sep 12 | SSK |

| 10 | 10.0 | Changed local constants to calibration to facilate the use of different temperature sensors. |  |  |

| 11 | 11.0 | Corrected naming conventions of new conversion calibrations. | 08Nov12 | LN |

| 12 | 12.0 | Corrected anomaly 4541 | 06Apr13 | KJS |

|  |  |  |  |  |
