---
title: 'PSATA MDD'
description: 'Converted design document: PSATA MDD'
---

> **Source:** `PSATA/doc/PSATA_MDD.docx`  
> **Module:** [PSATA](../../../../asw/psata/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

### Module Design Document

### For

### CF14 PSA Torque Arbitrator

### VERSION: 1.0

### DATE: 10-Mar-2014

### Prepared By:

### Sankardu Varadapureddi,

### Nexteer Automotive,

### Saginaw, MI, USA

Location: The official version of this document is stored in the Nexteer Configuration Management System.

### Revision History

### Table of Contents

1	Abbrevations And Acronyms	5

2	References	6

3	PSA State Handler High-Level Description	7

4	Design details of software module	8

4.1	Graphical representation of PSA Torque Arbitrator	8

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

7	Software Module Implementation	11

7.1	Sub-Module Functions	11

7.1.1	Initialization Functions	11

7.1.1.1	Init: PSATA_Init1	11

7.1.1.1.1	Design Rationale	11

7.1.1.1.2	Module Outputs	11

7.1.1.1.3	Module Internal	11

7.1.2	PERIODIC FUNCTIONS	11

7.1.2.1	Per: PSATA_per1	11

7.1.2.1.1	Design Rationale	11

7.1.2.1.2	Store Module Inputs to Local copies	11

7.1.2.1.3	(Processing of function)………	11

7.1.2.1.4	Store Local copy of outputs into Module Outputs	11

7.1.3	Interrupt Functions	12

7.1.4	Serial Communication Functions	13

7.1.5	Local Function/Macro Definitions	13

7.1.5.1	Local Function #1	13

7.1.5.1.1	Description	13

7.1.5.2	Local Function #2	13

7.1.5.2.1	Description	13

7.1.6	GLObAL Function/Macro Definitions	13

7.1.7	Tranisition FUNCTIONS	13

8	Known Limitations With Design	14

9	UNIT TEST CONSIDERATION	15

10	Appendix	16

## Abbrevations And Acronyms

## References

This section lists the title & version of all the documents that are referred for development of this document

## PSA State Handler High-Level Description

The PSA Torque Arbitrator will be  equipped for EPS Systems with functions including Ramping and smoothing of PosServo command and Safety function. The safety function will monitor the PSA State Handler and PSA Torque Arbitrator.

## Design details of software module

### Graphical representation of PSA Torque Arbitrator

Refer FDD

### Data Flow Diagram

Refer FDD

### Module level DFD

Refer FDD

### Sub-Module level DFD

Refer FDD

### COMPONENT FLOW DIAGRAM

Refer FDD

## Variable Data Dictionary

### User defined typedef definition/declaration

<This section documents any user types uniquely used for the module.>

### Variable definition for enumerated types

## Constant Data Dictionary

### Program(fixed) Constants

### Embedded Constants

### Local

### Global

### Module specific Lookup Tables Constants

## Software Module Implementation

### Sub-Module Functions

### Initialization Functions

### Init: PSATA_Init1

### Design Rationale

Low pass filter to calucalte the init co-efficient ‘PSATA_FilterdTrqSV_HwNm_M_Str’.

Also trigger DIAG manager to make  ‘NTC_Num_SigPath5CrossChk’ ‘test not ready status’ to cleared. This is  done by setting NTC status to ‘Passed’.

### Module Outputs

None

### Module Internal

PSATA_FilterdTrqSV_HwNm_M_Str

### PERIODIC FUNCTIONS

### Per: PSATA_per1

### Design Rationale

Design follows implemenetation in FDD.

As per FDD owner,

- ‘NTC_Num_PosServFltMode’ and ‘NTC_Num_SigPath5CrossChk’ are different names used in different documents for the same NTC ‘196u’. Note that ‘NTC_Num_PosServFltMode’ is ignitial latched.

- In block ‘PSATA_Per1’,  there is a switch block based on 'PosSrvoNTC_Cnt_lgc >=1 'condition. ‘>’ condition will never be TRUE since 'PosSrvoNTC_Cnt_lgc' gets either ‘1’ or ‘0’ only. [Here option of ''PosSrvoNTC_Cnt_lgc ~=0' had been considered in the FDD design phase but if there is toggling in the value then in design it is not considered that option due to previous experiences.]

### Store Module Inputs to Local copies

HwTorque_HwNm_T_f32 = Rte_IRead_PSATA_Per1_HwTorque_HwNm_f32();

PosSrvoCmd_MtrNm_T_f32 = Rte_IRead_PSATA_Per1_PosSrvoCmd_MtrNm_f32();

PosSrvoEnable_Cnt_T_lgc = Rte_IRead_PSATA_Per1_PosSrvoEnable_Cnt_lgc();

VehicleSpeed_Kph_T_f32 = Rte_IRead_PSATA_Per1_VehicleSpeed_Kph_f32();

### (Processing of function)………

Refer to FDD  (Block ‘PSATA_Per1’)

### Store Local copy of outputs into Module Outputs

Rte_IWrite_PSATA_Per1_OpTrqOv_MtrNm_f32(OpTrqOv_MtrNm_T_f32);

Rte_IWrite_PSATA_Per1_PosSrvoNTC_Cnt_lgc(PSATA_PosSrvoNTC_Cnt_M_lgc);

### Interrupt Functions

None

### Serial Communication Functions

None

### Local Function/Macro Definitions

### Local Function #1

### Description

This function monitors 'State Handler' and 'PosServo' for errors. Sets 'PosSrvoNTC_Cnt_lgc'  signal accordingly.

Note: This implementation corresponds to lower half of 'PSATA_Per1' block.

### Local Function #2

### Description

Implementation of 'PosServoSmoothing' block. PosServoCmd changes instantly from zero when disabled to non-zero when enabled, and vice-versa. This routine calculates a scale factor for the PosServoCmd to smoothly ramp it in and out. First, it produces a linear scale factor, then feeds the linear factor into a lookup table to non-linearize it.This produces softer transitions when scale factor is near zero or near unity. The scale factor can decrease more rapidly when driver hand wheel torque is present.

### GLObAL Function/Macro Definitions

None

### Tranisition FUNCTIONS

None

## Known Limitations With Design

## UNIT TEST CONSIDERATION

FDD describes  functionality and structural breakdown of this componenet. Data dictionary contains all attributes of varibales and calibrations used.

## Appendix

| Sl. No. | Description | Author | Version | Date |

| --- | --- | --- | --- | --- |

| 1 | Initial Version | Sankardu Varadapureddi | 1.0 | 10-Mar-2015 |

|  |  |  |  |  |

|  |  |  |  |  |

|  |  |  |  |  |

|  |  |  |  |  |

| Abbreviation | Description |

| --- | --- |

| DFD | Design functional diagram |

| MDD | Module design Document |

| FDD | Functional Design Document |

| CF | Customer Function |

| Sr. No. | Title | Version |

| --- | --- | --- |

| 1 | MDD Guidelines | 1.4 |

| 2 | Software Naming Conventions | 1.2 |

| 3 | Software Design and Coding standards | 2.1 |

| 4 | CF14 PSA State handler FDD | 1.1.0 |

| 5 | Data Dictionary.xlsm | 1.0 |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| None |  |  |  |  |

|  |  |  |  |  |

| Enum  Name | Element Name | Value |

| --- | --- | --- |

| None |  |  |

| Constant Name | Resolution | Units | Value |

| --- | --- | --- | --- |

| D_NTCHIGH_CNT_LGC | 1 | CNT | 1 |

| D_NTCLOW_CNT_LGC | 1 | CNT | 0 |

| D_POSSRVONTCENABLE_MTRNM_F32 | single preicision float | MTRNM | 0.0F |

| D_POSSRVOTRANSITION_ULS_F32 | single preicision float | ULS | 0.01999999955F |

| D_SMOOTHINGHIGH_CNT_F32 | 1 | CNT | 1 |

| D_SMOOTHINGLOW_CNT_F32 | 1 | CNT | 0 |

| Constant Name |

| --- |

| D_ZERO_CNT_U8 |

| D_ZERO_ULS_F32 |

| D_TRUE_CNT_LGC |

| D_2MS_SEC_F32 |

| D_MTRTRQCMDHILMT_MTRNM_F32 |

| D_MTRTRQCMDLOLMT_MTRNM_F32 |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | Cal_PosSrvoNTC | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | PosSrvoCmd_MtrNm_T_f32 | Float32 | -8.800000191 | 8.800000191 |

|  | PosSrvoEnable_Cnt_T_lgc | Boolean | FALSE | TRUE |

|  | VehicleSpeed_Kph_T_f32 | Float32 | 0 | 511 |

| Return Value | N/A |  |  |  |

| Function Name | Cal_PosServoSmoothingFactor | Type | Min | Max |

| --- | --- | --- | --- | --- |

| Arguments Passed | HwTorque_HwNm_T_f32 | Float32 | -10 | 10 |

|  | PosSrvoEnable_Cnt_T_lgc | Boolean | FALSE | TRUE |

| Return Value | N/A |  |  |  |
