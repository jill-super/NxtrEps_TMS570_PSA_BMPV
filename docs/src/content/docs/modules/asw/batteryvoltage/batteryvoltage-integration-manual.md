---
title: 'BatteryVoltage Integration Manual'
description: 'Converted design document: BatteryVoltage Integration Manual'
---

> **Source:** `BatteryVoltage/doc/BatteryVoltage_Integration_Manual.docx`  
> **Module:** [BatteryVoltage](../../../../asw/batteryvoltage/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual – Battery Voltage

Table of Contents

1	Dependencies	2

1.1	SWCs	2

1.2	Global Functions(Non RTE) to be provided to Integration Project	2

2	Configuration	3

2.1	Build Time Config	3

2.2	Configuration Files to be provided by Integration Project	3

2.2.1	Da Vinci Parameter Configuration Changes	3

2.2.2	DaVinci Interrupt Configuration Changes	3

2.2.3	Manual Configuration Changes	3

3	Integration	4

3.1	Required Global Data Inputs	4

3.2	Required Global Data Outputs	4

3.3	Specific Include Path present	4

4	Runnable Scheduling	5

5	Memory Mapping	6

5.1	Mapping	6

5.2	Usage	6

5.3	Non  RTE NvM Blocks	6

5.4	RTE NvM Blocks	6

6	Compiler Settings	6

6.1	Preprocessor MACRO	6

6.2	Optimization Settings	6

7	Revision Control Log	7

## Dependencies

### SWCs

Note : Referencing the external components should be avoided in most cases. Only in unavoidable circumstance external components should be referred. Developer should track the references.

* Note: EnableOvervoltThreshInterrupt() must be called from ECUStartup.c as soon as possible, but AFTER Adc_Init(), so as to allow configuration of the ADC registers (and subsequently magnitude threshold).

### Global Functions(Non RTE) to be provided to Integration Project

- ISR(Isr_OvervoltThresh)

- Since the ISR that contains the overvoltage threshold diagnostic is enabled in ECUStartup.c, the NTC could be set before the RTE starts. In this case the non-Rte “report NTC staus” API should be used. Also, the application that contains the Battery Voltage ISR and NTC is configured at the integration level.  A component specific API,  BATTERYVOLTAGE_REPORTERRORSTATUS, is used in the ISR source code and a header file, Template_BatteryVoltage_Cfg.h, needs to be configured to link the BATTERYVOLTAGE_REPORTERRORSTATUS() to the appropriate NxtrDiagMgr???_ReportNTCStatus() function. Remove the “Template_” from the file name and replace the ??? in the API with the appropriate application and place the file in the Header folder of the integration project.

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

<Configuration file that will generated from this components that will require Da Vinci Config generation or manual generation. Describe each parameter >

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

None

### Required Global Data Outputs

None

### Specific Include Path present

No

## Runnable Scheduling

This section specifies the required runnable scheduling.

## Memory Mapping

### Mapping

* Each …START_SEC… constant is terminated by a …STOP_SEC… constant as specified in the AUTOSAR Memory Mapping requirements.

### Usage

Table 1: ARM Cortex R4 Memory Usage

### Non  RTE NvM Blocks

Note : Size of the NVM block if configured in developer

### RTE NvM Blocks

Note : Size of the NVM block if configured in developer

## Compiler Settings

### Preprocessor MACRO

None

### Optimization Settings

None

## Revision Control Log

| Module | Required Feature |

| --- | --- |

| ADC | D_ADC1CURRENTMODE_ULS_LGC configuration constant |

| Basic System Services | EnableOvervoltThreshInterrupt()* |

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| None |  |  |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| Isr_OvervoltThresh | 31 | None | Category 2 IRQ |

| Constant | Notes | SWC |

| --- | --- | --- |

| BATTERYVOLTAGE_REPORTERRORSTATUS |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| BatteryVoltage_Init1 | None | RTE (Warm init) |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| BatteryVoltage_Per1 | None | RTE (2ms) |

| BatteryVoltage_Per2 | None | RTE (4ms) |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| BATTERYVOLTAGE_START_SEC_VAR_CLEARED_32 | float32 | None |

| BATTERYVOLTAGE_START_SEC_VAR_CLEARED_16 | uint16 | None |

| BATTERYVOLTAGE_START_SEC_VAR_CLEARED_BOOLEAN | boolean | None |

| Feature | RAM | ROM |

| --- | --- | --- |

| <Memmap usuage info> |  |  |

| Block Name |

| --- |

| None |

| Block Name |

| --- |

| OvervoltageData (6 bytes) |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 16-Apr-13 | Jared |

| 2 | Added Overvoltage Threshold ISR, some cleanup, updated template | 3-Jan-14 | Jared |

| 3 | Added BATTERYVOLTAGE_REPORTERRORSTATUS and new template header file. | 8-Jan-14 | BDO |
