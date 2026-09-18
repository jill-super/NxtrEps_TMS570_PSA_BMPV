---
title: 'ePWM Integration Manual'
description: 'Converted design document: ePWM Integration Manual'
---

> **Source:** `ePWM/doc/ePWM_Integration_Manual.docx`  
> **Module:** [ePWM](../../../../cdd/epwm/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual  ePWM

Table of Contents

1	Dependencies	2

1.1	SWCs	2

1.2	Global Functions(Non RTE) to be provided to Integration Project	2

2	Configuration	3

2.1	Build Time Config	3

2.2	Configuration Files to be provided by Integration Project	3

ePWM_Cfg.h is manually created and used.	3

2.2.1	Da Vinci Parameter Configuration Changes	3

2.2.2	DaVinci Interrupt Configuration Changes	5

2.2.3	Manual Configuration Changes	5

3	Integration	6

3.1	Required Global Data Inputs	6

3.2	Required Global Data Outputs	6

3.3	Specific Include Path present	6

4	Runnable Scheduling	7

5	Memory Mapping	8

5.1	Mapping	8

5.2	Usage	8

5.3	Non  RTE NvM Blocks	9

5.4	RTE NvM Blocks	9

6	Other Configuration Changes	9

6.1.1	DIO and IOHwAb	9

6.1.2	Port	10

7	Compiler Settings	11

7.1	Preprocessor MACRO	11

7.2	Optimization Settings	11

8	Revision Control Log	12

## Dependencies

### SWCs

Note : Referencing the external components should be avoided in most cases. Only in unavoidable circumstance external components should be referred. Developer should track the references.

### Global Functions(Non RTE) to be provided to Integration Project

Nhet1_Per3

Nhet_Init1

ePWM_Per1

ePWM_Init1

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

### ePWM_Cfg.h is manually created and used.

Refer the ePWM_Cfg_Template.h provided in the tools path of the component for more details

#### Da Vinci Parameter Configuration Changes

*If uDiagRegValueLnkOffset  equals -1 , then we calculate the offset using the function sizeof (“uDiagRegValueLnk”) -1UL

NOTE – this list documents only the HTU-related registers which should be configured for the runtime register check (because they were added or updated since the integration manual has existed); it is not a complete list of the critical registers related to this component.

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

DiagStsCtrldDisRmpPres_Cnt_lgc

DiagStsNonRecRmpToZeroFltPres_Cnt_lgc

RampDwnStatusComplete_Cnt_lgc (from SF-05)

PWM Period, phase A, B, and C Duty Cycle Counts, and ePWM4 CMPB: macros must be configured in ePWM_cfg.h (see template file in the tools folder) to read the global variables holding these values.

In addition, code must be provided to write the ePWM4 CMPB global variable as follows: write the value 100 (decimal) near the beginning of the 2 ms loop.  Write the value 65535 (decimal) at least three PWM period times (use the max PWM period) after writing the value 100.  This is per the ADC SOCB configuration update subfunction of  ES-34B.

### Required Global Data Outputs

Nhet_HtuDataTrq_Cnt_G_str

Nhet_Htu1RstFail_Cnt_G_lgc

Macros must be configured in ePWM_cfg.h (see template file in the tools folder) to write the following outputs:

CMPA and CMPB values for ePWM1, ePWM2, ePWM3, and ePWM4

PWM Period for NHET1

This version of the ePWM component is intended to be used with DMA; the macros should write the PWM Period and  ePWM values to the global DMA data structure.

### Specific Include Path present

Yes

## Runnable Scheduling

This section specifies the required runnable scheduling.

## Memory Mapping

### Mapping

* Each …START_SEC… constant is terminated by a …STOP_SEC… constant as specified in the AUTOSAR Memory Mapping requirements.

### Usage

Table : ARM Cortex R4 Memory Usage

### .

### Non  RTE NvM Blocks

Note : Size of the NVM block if configured in developer

### RTE NvM Blocks

Note : Size of the NVM block if configured in developer

## Other Configuration Changes

#### DIO and IOHwAb

If NHET was previously used to generate PWM signals, reassignments are required (as the ePWM outputs will conflict with assigned DIO pins).  This is hardware-dependent; refer to the program’s Resource Allocation sheet or schematic.  The following pins are used by ePWM and the ePWM-specific NHET on the TMS570LS1227 PGE (144 pin) package (see the datasheet for more information):

#### Port

##### Pin Direction Settings

The changes in DIO (hardware-dependent) may require updates to the pin direction and other settings for the newly configured DIO signals.

##### Multiplexing Changes

Several multiplexing options must be configured for both external routing (peripherals to pins) and internal routing (peripherals to peripherals).

The following changes must be made within configurator:

- Multiplexing for DIO changes (hardware-dependent)

- Multiplexing for NHET component change

- This should result in PINMUX1[8-15] being set to 0x04

- While N2HET2[8] and [10] can be configured, configurator does not generate these values correctly (see the manual configuration below)

- ADC Trigger Table – select ADC Trigger Table 2

- This should result in PINMUX30[0-7] being set to 0x02

The following changes must be made with manual edits to Port_PBcfg.c:

* Configurator does not define symbols for these registers.  Define the following symbols manually:

#define PORT_BASE_ADDR_PINMUX_31  ((Port_RegisterPtrType)(0xFFFFEB8C))

#define PORT_BASE_ADDR_PINMUX_35  ((Port_RegisterPtrType)(0xFFFFEB9C))

#define PORT_BASE_ADDR_PINMUX_37  ((Port_RegisterPtrType)(0xFFFFEBA4))

#define PORT_BASE_ADDR_PINMUX_38  ((Port_RegisterPtrType)(0xFFFFEBA8))

A default value of 0x01 should be used for bytes not otherwise defined.

## Compiler Settings

### Preprocessor MACRO

None

### Optimization Settings

None

## Revision Control Log

| Module | Required Feature |

| --- | --- |

| uDiag | HTU MPU ESM (uDiag Component version FDD32B_TMS570_uDiag_000.24 or later)<br/>(Configuration of ESM Registers) |

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| uDiag/RuntimeRegCheck/HTU__MP0S_HTU1 | Address Linked during runtime |  |

| uDiagRegAddress |  | 4294419572 (0xFFF7A474) |

| uDiagRegValueLnk |  | Nhet_HtuDataTrq_Cnt_G_str |

| uDiagRegValueLnkOffset |  | 0 |

|  |  |  |

| uDiag/RuntimeRegCheck /HTU__MP0E_HTU1 | Address Linked during runtime |  |

| uDiagRegAddress |  | 4294419576(0xFFF7A478) |

| uDiagRegValueLnk |  | Nhet_HtuDataTrq_Cnt_G_str |

| uDiagRegValueLnkOffset* |  | Sizeof(Nhet_HtuDataTrq_Cnt_G_str)-4 |

| uDiag/RuntimeRegCheck HTUDCP1_IFADDRA_HTU1 | Address Linked during runtime |  |

| uDiagRegAddress |  | (0xFF4E0010 |

| uDiagRegValueLnk |  | Nhet_HtuDataTrq_Cnt_G_str.HtuDataTrq1_Cnt_u32[0] |

| uDiagRegValueLnkOffset |  | 0 |

| uDiag/RuntimeRegCheck/HTU__MP1S_HTU1 |  |  |

| uDiagRegAddress |  | 4294419532(0xFFF7A44C) |

| uDiagRegValue |  | 0 |

|  |  |  |

| uDiag/RuntimeRegCheck /HTU__MP1E_HTU1 |  |  |

| uDiagRegAddress |  | 4294419536(0xFFF7A450) |

| uDiagRegValue |  | 0 |

|  |  |  |

|  |  |  |

|  |  |  |

|  |  |  |

|  |  |  |

|  |  |  |

| uDiag/RuntimeRegCheck HTUDCP2_IFADDRA_HTU1 | Address Linked during runtime |  |

| uDiagRegAddress |  | 0xFF4E0020 |

| uDiagRegValueLnk |  | (Nhet_HtuDataTrq_Cnt_G_str.HtuDataTrq2_Cnt_u32[0]) |

| uDiagRegValueLnkOffset |  | 0 |

| uDiag/RuntimeRegCheck/HTU__CPENA_HTU1 |  |  |

| uDiagRegAddress |  | 0xFFF7A404U |

| uDiagRegValue |  | 0x14U |

| uDiag/RuntimeRegCheck/HTU__GCR_HTU1 |  |  |

| uDiagRegAddress |  | 0xFFF7A400U |

| uDiagRegValue |  | 0x10100 |

| uDiag/RuntimeRegCheck/HTU__PCR_HTU1 |  |  |

| uDiagRegAddress |  | 0xFFF7A464U |

| uDiagRegValue |  | 0xA |

| uDiag/RuntimeRegCheck/HTU__MPCS_HTU1 |  |  |

| uDiagRegAddress |  | 0xFFF7A470U |

| uDiagRegValue |  | 0x07u |

| uDiag/RuntimeRegCheck/HTUDCP1__ITCOUNT_HTU1 |  |  |

| uDiagRegAddress |  | 0xFF4E001CU |

| uDiagRegValue |  | 0x80001 |

| uDiag/RuntimeRegCheck/HTUDCP1__IHADDRCT_HTU1 |  |  |

| uDiagRegAddress |  | 0xFF4E0018U |

| uDiagRegValue |  | 0x40368 |

| uDiag/RuntimeRegCheck/HTUDCP2__ITCOUNT_HTU1 |  |  |

| uDiagRegAddress |  | 0xFF4E002CU |

| uDiagRegValue |  | 0x80001 |

| uDiag/RuntimeRegCheck/HTUDCP2__IHADDRCT_HTU1 |  |  |

| uDiagRegAddress |  | 0xFF4E0028U |

| uDiagRegValue |  | 0x40538 |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| None |  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| D_CONFIGHETREGDMA_CNT_U32 | The value will be set to 0 to disable DMA and set  to 1 for Enable DMA | ePWM_Cfg.h |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| Nhet_Init1 | Place in EcuStartup_Init1 (EcuStartup.c) along with ePWM_Init1, following the memory initialization routine SchM_InitMemory. | Init |

| ePWM_Init1 | Place in EcuStartup_Init1 (EcuStartup.c) along with Nhet_Init1, following the memory initialization routine SchM_InitMemory. | Init |

| ePWM_Per1 | Must be placed in the motor control ISR, following PwmCdd (or whichever function populates the global variables used by ePWM). | Cyclic (ISR) |

| ePWM2_Per1 | Schedule after StOpCtrl and CtrldDisShtdn, and before DiagMgr | 2ms (RTE) |

| ePWM2_Trns1 | Schedule on transition into the WARMINIT state | Event (RTE) |

| ePWM2_Trns2 | Schedule on transition into the DISABLE state | Event (RTE) |

| Nhet1_Per1 | Schedule  before NHet1 period 2 | 2ms (RTE) |

| Nhet1_Per2 | Schedule before Digital HwTrqSensor | 2ms (RTE) |

| Nhet1_Per3 | Must be placed in the motor control ISR, following PwmCdd and after ePWM_Per1 (or whichever function populates the global variables used by Nhet). | Cyclic(ISR) |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| EPWM_START_SEC_CODE | Runnable Code |  |

| NHET_START_SEC_CODE | Runnable Code |  |

| NHET1_START_SEC_CODE | Runnable Code |  |

| NHET_START_SEC_VAR_CLEARED_UNSPECIFIED |  |  |

| NHET1_START_SEC_VAR_CLEARED_32 |  |  |

| NHET1_START_SEC_VAR_CLEARED_16 |  |  |

| NHET1_START_SEC_VAR_CLEARED_8 |  |  |

| NHET_START_SEC_VAR_CLEARED_BOOLEAN |  |  |

| NHET1_START_SEC_CONST_8 |  |  |

| EPWM_START_SEC_VAR_CLEARED_16 |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| Full driver |  |  |

| Block Name |

| --- |

| None |

| Block Name |

| --- |

| None |

| Pin | Function |

| --- | --- |

| 6 | N2HET1[11], MIBSPI3NCS[4], N2HET2[18], ETPWM1SYNCO |

| 14 | GIOA[5], EXTCLKIN, ETPWM1A |

| 15 | GIOA[6], N2HET2[4], ETPWM1B |

| 22 | GIOA[7], N2HET2[6], ETPWM2A |

| 23 | N2HET1[1], SPI4ENA, N2HET2[8] |

| 24 | N2HET1[3], SPI4NCS[0], N2HET2[10] |

| 25 | N2HET1[0], SPI4CLK, ETPWM2B |

| 30 | N2HET1[2], SPI4SIMO, ETPWM3A |

| 31 | N2HET1[5], SPI4SOMI, N2HET2[12], ETPWM3B |

| 33 | N2HET1[7], N2HET2[14], ETPWM7B |

| Register | Bits | Value | Selected Option |

| --- | --- | --- | --- |

| PINMUX2 | 24-31 | 0x04 | ETPWM1A |

| PINMUX3 | 16-23 | 0x04 | ETPWM1B |

| PINMUX4 | 0-7 | 0x04 | ETPWM2A |

| PINMUX4 | 16-23 | 0x10 | N2HET2[8] (configurator errata) |

| PINMUX4 | 24-31 | 0x10 | N2HET2[10] (configurator errata) |

| PINMUX5 | 0-7 | 0x04 | ETPWM2B |

| PINMUX5 | 8-15 | 0x04 | ETPWM3A |

| PINMUX5 | 16-23 | 0x08 | ETPWM3B |

| PINMUX6 | 0-7 | 0x10 | ETPWM7B |

| PINMUX31* | 16-31 | 0x0202 | ADC2 Trigger Event Selection |

| PINMUX35* | 24-31 | 0x00 | SOC4A_SEL cleared |

| PINMUX37* | 0-31 | 0x01010102 | Sync time bases, enable clocks for ePWM 0 to 3 |

| PINMUX38* | 0-31 | 0x01000001 | Enable clocks for ePWM 4 and 7 |

| Rev # | Change Description | Change Description | Date | Date | Author |

| --- | --- | --- | --- | --- | --- |

| 1,2 | Initial version | Initial version | 15-Feb-13 | 15-Feb-13 | OT |

| 3 | Updated the Cd_Nhet1.C integration | Updated the Cd_Nhet1.C integration | 25-July-13 | 25-July-13 | Selva |

| 4 | Updated for FDD v5 ES34B | Updated for FDD v5 ES34B | 7-April-14 | 7-April-14 | Selva |

| 5 | Anomaly fix 6589 - Correct the value for the HTU MP0E register | Anomaly fix 6589 - Correct the value for the HTU MP0E register | 23-Apr-14 | 23-Apr-14 | SB |

| 6 | Updated for critical register check | Updated for critical register check | 2-May-14 | 2-May-14 | Selva |

| 7 | Corrected the IHADDR  DCP1 and DCP2 values | Corrected the IHADDR  DCP1 and DCP2 values | 2-May-14 | 2-May-14 | Selva |

| 8 | Added ePWM2_Per1 and updated global data information and critical register information per ES-34B v008. | 27-Jan-15 | 27-Jan-15 | KMC | KMC |

|  |  |  |  |  |  |
