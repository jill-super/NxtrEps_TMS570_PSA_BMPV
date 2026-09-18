---
title: 'CustomerBattDiagnostic MDD'
description: 'Converted design document: CustomerBattDiagnostic MDD'
---

> **Source:** `PSA_BMPV_EPS_TMS570/SwProject/CustBattDiag/doc/CustomerBattDiagnostic_MDD.docx`  
> **Module:** [SwProject/CustBattDiag](../../../../asw/swproject-custbattdiag/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

### Module Design Document

### For

### Customer Battery Voltage Diagnostics

### VERSION:

### DATE: --2015

### Revision History

### Table of Contents

1	Abbrevations And Acronyms	5

2	References	6

3	Battery Voltage Diagnostic High-Level Description	7

4	Design details of software module	8

4.1	Graphical representation of CustBattDiag	8

4.2	Data Flow Diagram	8

4.2.1	Module level DFD	8

4.2.2	Sub-Module level DFD	8

4.3	COMPONENT FLOW DIAGRAM	8

5	Variable Data Dictionary	9

5.1	User defined typedef definition/declaration	9

5.2	Variable definition for enumerated types	9

6	Constant Data Dictionary	10

6.1	Program(fixed) Constants	10

6.1.1	Embedded Constants	10

6.1.1.1	Local	10

6.1.1.2	Global	10

6.1.2	Module specific Lookup Tables Constants	10

6.1.3	Library Functions / Macros	11

6.1.4	Data Hiding Functions	11

7	Software Module Implementation	12

7.1	Initialization Functions	12

7.1.1	Init	12

7.1.1.1	Module Outputs	12

7.1.1.2	Module Internal	12

7.2	PERIODIC FUNCTIONS	13

7.2.1	Per: CustBattDiag_Per1	13

7.2.1.1	Design Rationale	13

7.2.1.2	Store Module Inputs to Local copies	13

7.2.1.3	Ntc 0xE5 and 0xE7 Diagnostics	13

7.2.1.4	Store Local copy of outputs into Module Outputs	13

7.2.2	Per: CustBattDiag_Per2	14

7.2.2.1	Design Rationale	14

7.2.2.2	Store Module Inputs to Local copies	14

7.2.2.3	Battery Voltage Diagnostics	14

7.2.2.4	Store Local copy of outputs into Module Outputs	16

7.3	Interrupt Functions	16

7.4	TRANSIENT FUNCTIONS	16

7.5	Serial Communication Functions	16

7.6	Local Function/Macro Definitions	16

7.6.1	Apply hysteresis	16

7.6.2	Description	16

7.6.3	Control Timers	17

7.6.4	Description	17

7.7	GLObAL Function/Macro Definitions	18

8	Known Limitations With Design	19

9	UNIT TEST CONSIDERATION	20

10	Appendix A – Configuration Schemes	21

## Abbrevations And Acronyms

## References

This section Lists the title & version of all the documents that are referred for development of this document

## Battery Voltage Diagnostic High-Level Description

This module is responsible for applying voltage and time based hysteresis to the battery voltage to determine customer specific over voltage and low voltage faults.  Requirements for all these faults are detailed in the SCIR.

## Design details of software module

### Graphical representation of CustBattDiag

None

### Data Flow Diagram

None

### Module level DFD

None

### Sub-Module level DFD

None

### COMPONENT FLOW DIAGRAM

## Variable Data Dictionary

### User defined typedef definition/declaration

### Variable definition for enumerated types

## Constant Data Dictionary

### Program(fixed) Constants

### Embedded Constants

### Local

### Global

### Module specific Lookup Tables Constants

### Library Functions / Macros

None

### Data Hiding Functions

Rte_Call_SystemTime_GetSystemTime_mS_u32 ()

Rte_Call_SystemTime_DtrmnElapsedTime_mS_u16 ()

Rte_Call_NxtrDiagMgr_SetNTCStatus ()

## Software Module Implementation

### Initialization Functions

None

### PERIODIC FUNCTIONS

### Per: CustBattDiag_Per1

### Design Rationale

The under voltage and over voltage diagnostics(NTC 0xE5 and 0xE7) are specified to run in all states and at a 10ms rate.  Due to the faster diagnostic timing and different enable conditions, these two NTCs were moved into their own periodic.

### Store Module Inputs to Local copies

BattVoltage_Volts_T_f32 = Rte_IRead_CustBattDiag_Per1_Batt_Volt_f32()

BattVoltage_Volts_T_u10p6 = FPM_FloatToFixed_m(BattVoltage_Volts_T_f32, u10p6_T)

### Ntc 0xE5 and 0xE7 Diagnostics

### Store Local copy of outputs into Module Outputs

None

### Per: CustBattDiag_Per2

### Design Rationale

The battery voltage diagnostics were split into two periodics.  Per1 handles the faster 10ms diagnostics while Per2 handles the rest.

### Store Module Inputs to Local copies

BattVoltage_Volts_T_f32 = Rte_IRead_CustBattDiag_Per2_Batt_Volt_f32()

VehSpd_Kph_T_f32 = Rte_IRead_ CustBattDiag _Per2_VehicleSpeed_Kph_f32()

EngOn_Cnt_T_lgc = Rte_IRead_ CustBattDiag _Per2_EngOn_Cnt_lgc()

EtatMT_Cnt_T_u08 = Rte_IRead_ CustBattDiag _Per2_EtatMTMT_Cnt_u08()

BattVoltage_Volts_T_u10p6 = FPM_FloatToFixed_m(BattVoltage_Volts_T_f32, u10p6_T)

SttdSelcted_Cnt_T_lgc = Rte_IRead_ CustBattDiag _Per2_STTdSelected_Cnt_lgc()

ValidEngineStatus_Cnt_T_lgc = Rte_IRead_CustBattDiag_Per2_ValidEngineStatus_Cnt_lgc()

VehSpdValid_Cnt_T_lgc = Rte_IRead_CustBattDiag_Per2_VehicleSpeedValid_Cnt_lgc()

SystemState_Cnt_T_enum = Rte_Mode_SystemState_Mode()

Rte_Call_EpsEn_OP_GET(&EpsEn_Cnt_T_lgc)

Rte_Call_SystemTime_GetSystemTime_mS_u32(&SystemTime_mS_T_u32)

### Battery Voltage Diagnostics

### Store Local copy of outputs into Module Outputs

None

### Interrupt Functions

None

### TRANSIENT FUNCTIONS

None

### Serial Communication Functions

None

### Local Function/Macro Definitions

### Control Timers

### Description

- CompareType_T_u08: 	Passed data to indicate passed, failed or in the hysteresis deadband

- SetTimer_T_ptr:	Pointer to the appropriate module specific 32-bit set timer under test (examples are set timer for over voltage, low voltage, battery Ok, etc.)

- ClrTimer_T_ptr:	Pointer to the appropriate module specific 32-bit clear timer under test (examples are set timer for over voltage, low voltage, battery Ok, etc.)

- SetTimer_ms_T_u16p0:	Calibration used for the time based hysteresis to set the condition.  Note that the calibrations will differ for set timers for over voltage, low voltage, etc.

- ClrTimer_ms_T_u16p0:	Calibration used for the time based hysteresis to clear the condition.  Note that the calibrations will differ for set timers for over voltage, low voltage, etc.

- NTCNum_T_u16:	Identifies the NTC number to set or clear

### GLObAL Function/Macro Definitions

## Known Limitations With Design

## UNIT TEST CONSIDERATION

None

## Appendix A – Configuration Schemes

| Sl. No. | Description | Author | Version | Date |

| --- | --- | --- | --- | --- |

| 1 | Initial version | Steve Horwath | 1 | 15-Oct-2014 |

| 2 | Input update, cleanup | Owen Tosh | 2 | 14-Jan-2015 |

| 3 | Updates for SCIR 003B | Owen Tosh | 3 | 20-Jul-2015 |

| 4 | Corrected E8 timer conditions | Owen Tosh | 4 | 14-Sept-2015 |

|  |  |  |  |  |

| Abbreviation | Description |

| --- | --- |

| MDD | Module design Document |

| Sr. No. | Title | Version |

| --- | --- | --- |

| 1 | MDD Guidelines | 1 |

| 2 | Software Naming Conventions | 1 |

| 3 | Coding Standands | 1 |

| 4 | PSA BMPV SCIR | 003 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

| Enum  Name | Element Name | Value |

| --- | --- | --- |

| None |  |  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_TESTPASSED_CNT_U08 | 1 | Count | 0 |

| D_TESTFAILED_CNT_U08 | 1 | Count | 1 |

| D_INDEADBAND_CNT_U08 | 1 | Count | 2 |

| D_LOCKED_CNT_U08 | 1 | Count | 0x00 |

| D_CUT_CNT_U08 | 1 | Count | 0x01 |

| D_STARTING_CNT_U08 | 1 | Count | 0x02 |

| D_ENGRUNNING_CNT_U08 | 1 | Count | 0x03 |

| D_STOPPED_CNT_U08 | 1 | Count | 0x04 |

| D_DRVRESTART_CNT_U08 | 1 | Count | 0x05 |

| D_DEGRESTART_CNT_U08 | 1 | Count | 0x06 |

| D_ENGPREPARING_CNT_U08 | 1 | Count | 0x07 |

| D_AUTOSTARTING_CNT_U08 | 1 | Count | 0x0A |

| D_AUTORESTART_CNT_U08 | 1 | Count | 0x0D |

| D_INVALID_CNT_U08 | 1 | Count | 0x0F |

| Constant Name |

| --- |

| RTE_MODE_StaMd_Mode_WARMINIT |

| RTE_MODE_StaMd_Mode_OPERATE |

| RTE_MODE_StaMd_Mode_DISABLE |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | ControlTimers | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | CompareType_T_u08 | Uint08 | 0 | 15 |

|  | SetTimer_T_ptr | uint32* | 0 | 2^32-1 |

|  | ClrTimer_T_ptr | uint32* | 0 | 2^32-1 |

|  | SetTimer_ms_T_u16p0 | uint16 | 0 | 65535 |

|  | ClrTimer_ms_T_u16p0 | uint16 | 0 | 65535 |

|  | NTCNum_T_u16 | uint16 | 0 | 255 |

| Return Value | None |  |  |  |
