---
title: 'PWMCdd Integration Manual'
description: 'Converted design document: PWMCdd Integration Manual'
---

> **Source:** `SVDrvr_CM/doc/PWMCdd_Integration_Manual.docx`  
> **Module:** [SVDrvr_CM](../../../../cdd/svdrvr_cm/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual – PWMCdd

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

### Global Functions(Non RTE) to be provided to Integration Project

CDDPorts_ClearPhsReasSum(uint16 DataAccessBfr_Cnt_T_u16)

CDD_ApplyPWMMtrElecMechPol(sint8 MtrElecMechPol_Cnt_s8)

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

<Configuration file that will generated from this components that will require Da Vinci Config generation or manual generation. Describe each parameter >

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

The following global symbols must be defined in CDD_Data.c and .h (populated by PwmCdd):

- uint16: CDD_DCPhsComp_Cnt_G_u16[3]

- uint16: CDD_PWMPeriod_Cnt_G_u16

NHET/EPWM  version corresponding PWMCdd component spilt and using global variables CDD_DCPhsComp_Cnt_G_u16 and CDD_PWMPeriod_Cnt_G_u16  should be used.

- CDD_Read_PhaseAdvanceFinal_Rev_u0p16

- CDD_Read_CorrectedMtrPos_Rev_u0p16

- CDD_Read_CommOffset_Cnt_u16

### Required Global Data Outputs

- CDD_Write_DCPhsBComp_Cnt_u16p0

- CDD_Write_DCPhsCComp_Cnt_u16p0

### Specific Include Path present

Yes - The “include” directory of this SWC needs to be included in the integration project include search path.

## Runnable Scheduling

This section specifies the required runnable scheduling.

### .

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

| CDD_Data | Global variables for DC Phs Comp (for using in Nhet/) |

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| None |  |  |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| None |  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| d_PwmFreq_Hz_Cnt_u16            <br/>d_PWMFreqDither_Hz_u16 |  |  |

| Init | Scheduling Requirements | Scheduling Requirements | Trigger | Trigger |

| --- | --- | --- | --- | --- |

| PwmCdd_Init | PwmCdd_Init | Place in EcuStartup.  Execute along with NHET initialization. | Place in EcuStartup.  Execute along with NHET initialization. | ISR |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| PwmCdd_Per1 | Must be placed in the motor control ISR, before Nhet (or whichever function populates the global variables used byNhet). | Cyclic (ISR) * |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| PWMCDD_START_SEC_VAR_CLEARED_16 | Variable Definitions |  |

|  |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| Full driver |  |  |

| Block Name |

| --- |

| None |

| Block Name |

| --- |

| None |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 14-Feb-13 | Selva |

| 2 | Added cal k_PWMBaseFrequency_Hz to replace constant d_PWMFreqBase_Hz_u16. | 21-Jan-14 | LK |
