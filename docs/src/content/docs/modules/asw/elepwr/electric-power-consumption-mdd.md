---
title: 'Electric Power Consumption MDD'
description: 'Converted design document: Electric Power Consumption MDD'
---

> **Source:** `ElePwr/doc/Electric_Power_Consumption_MDD.docx`  
> **Module:** [ElePwr](../../../../asw/elepwr/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module -- Electric Power Consumption

## High-Level Description

This module estimates the instantaneous electric power at the input of the control module and the supply current.

## Figures

### Diagram – Component Diagram

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

The library functions / Macros that are called by the various sub modules are identified below,

### Data Hiding Functions

None

### Local Functions/Macros Used by this MDD only

None

## Software Module Implementation

### Initial Data Values

### Periodic Functions

#### Per: ElePwr_Per1

##### Design Rationale

None

##### Program Flow Start

Rte_Call_ElePwr_Per1_CP0_CheckpointReached()

##### Store Module Inputs to Local copies

##### Calculate Modulator Input Power

##### Store Local copy of outputs into Module Outputs

##### Program Flow End

### Rte_Call_ElePwr_Per1_CP1_CheckpointReached()

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

None

### Serial Communication Functions

None

## Execution Requirements

### Execution Rates for sub-modules called by the Scheduler

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

None

## Revision Control Log

| Module Inputs | Module Outputs |

| --- | --- |

| Vecu_Volt_f32 | ElectricPower_Watt_f32 |

| MtrVoltDax_Volt_f32 | SupplyCurrent_Amp_f32 |

| MtrVoltQax_Volt_f32 |  |

| MtrCurrDax_Amp_f32 |  |

| MtrCurrQax_Amp_f32 |  |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| ModInPower_Watt_D_f32 | Single Precision Floating Point | -2000 | 2000 | ELEPWR_START_SEC_VAR_CLEARED _32 |

| DropInPower_Watt_D_f32 | Single Precision Floating Point | -200 | 200 | ELEPWR_START_SEC_VAR_CLEARED _32 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Constant Name |

| --- |

| k_CntlrInResist_Ohm_f32 |

| k_PstcPowerLoss_Watt_f32 |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_SQRT3OVR2_ULS_F32 | Single precision Float | Float32 | 0.866025403784 |

| D_ELECPOWERLOLMT_WATT_F32 | Single precision Float | Watt | (-2000.0) |

| D_ELECPOWERHILMT_WATT_F32 | Single precision Float | Watt | 2000.0 |

| D_SUPPLYCURRENTLOLMT_AMP_F32 | Single precision Float | Amp | (-200.0) |

| D_SUPPLYCURRENTHILMT_AMP_F32 | Single precision Float | Amp | (200.0) |

| Constant Name |

| --- |

| D_ZERO_ULS_F32 |

|  |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Data | Value |

| --- | --- |

| Rte_InitValue_Vecu_Volt_f32 |  |

| Rte_InitValue_MtrVoltDax_Volt_f32 | 0.0 |

| Rte_InitValue_MtrVoltQax_Volt_f32 | 0.0 |

| Rte_InitValue_MtrCurrDax_Amp_f32 | 0.0 |

| Rte_InitValue_MtrCurrQax_Amp_f32 | 0.0 |

| Rte_InitValue_ElectricPower_Watt_f32 | 0.0 |

| Local Copy | Module Input |

| --- | --- |

| Vecu_Volt_f32 | Rte_IRead_ElePwr_Per1_Vecu_Volt_f32() |

| MtrVoltDax_Volt_f32 | Rte_IRead_ElePwr_Per1_ MtrVoltDax_Volt_f32 () |

| MtrVoltQax_Volt_f32 | Rte_IRead_ElePwr_Per1_ MtrVoltQax_Volt_f32 () |

| MtrCurrDax_Amp_f32 | Rte_IRead_ElePwr_Per1_ MtrCurrDax_Amp_f32 |

| MtrCurrQax_Amp_f32 | Rte_IRead_ElePwr_Per1_ MtrCurrQax_Amp_f32 () |

| Local Copy | Module Output |

| --- | --- |

| ElecPower_Watt_T_f32 | Rte_IWrite_ElePwr_Per1_ ElectricPower_Watt_f32() |

| SupplyCurrent_Amp_T_f32 | Rte_IWrite_ElePwr_Per1_SupplyCurrent_Amp_f32 () |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| ElePwr_Per1 | 10 ms | All |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| None |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| ElePwr_Per1 | RTE_AP_ELEPWR_APPL_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

| None |  |

| Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- |

| 1 | Initial AUTOSAR version (SF08 v001). | 1-Dec-12 | Selva |

| 2 | Name changed  from CmElecPwr to ElePwr | 10-Dec-12 | Selva |

| 3 | Anomaly 6242 Limit Outputs | 02-Apr-14 | SB |

|  |  |  |  |
