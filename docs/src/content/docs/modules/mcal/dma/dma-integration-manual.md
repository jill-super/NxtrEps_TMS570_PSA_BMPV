---
title: 'Dma Integration Manual'
description: 'Converted design document: Dma Integration Manual'
---

> **Source:** `Dma/doc/Dma Integration Manual.docx`  
> **Module:** [Dma](../../../../mcal/dma/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual – Dma

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

7	Architectural Concerns	7

7.1	Overall DMA Architecture	8

7.2	Affected Modules	9

7.2.1	IoHwAbstractionUsr	9

7.2.2	Adc	9

7.2.3	MtrCtrl_Irq	9

7.2.4	uDiag	10

8	Revision Control Log	12

## Dependencies

### SWCs

Note : Referencing the external components should be avoided in most cases. Only in unavoidable circumstance external components should be referred. Developer should track the references.

### Global Functions(Non RTE) to be provided to Integration Project

Dma_Init

Dma_SlowADCGroupValidity

Dma_InvalidateSlowADCGroup

Dma_SetupMtrCtrlGroups

Dma_SetupFlsTstBlock

Dma_EnableFlsTstBlock

Dma_DisableFlsTstBlock

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

Dma_Cfg.h should be manually generated based on the template provided in the Tools folder.

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

None

### Required Global Data Outputs

DMAData_G_str

Dma_DmaRstFail_Cnt_G_lgc

### Specific Include Path present

Yes

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

Dma.c should use the same optimization settings as other functions called from the MtrCtrl ISR (generally, optimize = 3, optimize for speed = 5).

## Architectural Concerns

DMA is a module that largely impacts the system architecture, particularly at the MtrCtrl ISR time domain.  As such, this section includes some considerations for integrating DMA into an integration project for the first time.

The examples show integration of every DMA channel; if only a subset is used, not all of these examples may apply.

### Overall DMA Architecture

The following diagram is taken from FDD52, and shows how the DMA channels fit into the MtrCtrl ISR process:

### Affected Modules

#### IoHwAbstractionUsr

Historically, ADC conversions were triggered by the 2ms loop through the MtrCtrl ISR (the MtrCtrl ISR would perform a software trigger to the “slow” ADC groups directly).  With DMA, the “slow” ADC group conversion is now triggered by ePWM SOCB, driven by ePWM4 using CMPB.

In this new architecture, IoHwAbstractionUsr must perform the following:

- Before CDDInterface_Per1, an IoHwAbstractionUsr runnable must update the value of ePWM4 CMPB (refer to the ePWM component for the interface).  It must also clear the ADC1 G2 Conversions Ended bit as follows:

adcREG1->GxSR[2u] = 1u;

- After the conversion completes, an IoHwAbstractionUsr runnable must update the value of ePWM4 CMPB to disable the ADC conversion (refer to the ePWM component).

- After the conversion completes but before the ADC values are required to be used, an IoHwAbstractionUsr runnable must read and process the data from the DMA destination buffer.  The buffer can optionally be cleared at this point.  Note that this can be done from the same runnable as disabling the ADC conversion.

- An IoHwAbstraction runnable can be called from the MtrCtrl ISR to capture any data from the “fast” ADC conversion needed by the 2ms loop (ex. a redundant read of switched battery voltage).  The DMA buffer should be copied to a standard CDDInterface global variable and read by CDDInterface_Per1 along with the rest of the MtrCtrl ISR data used by the 2ms loop.

The final IoHwAbstractionUsr component could then look something like this:

IoHwAb_CaptureADC – reads Switched Battery Voltage from ADC2 DMA buffer and writes it to a CDD variable.

IoHwAb_StartADC – enables the ADC1 conversion and clears the ADC1 G2 Conversions Ended bit.  Scheduled in the 2ms loop just before CDDInterface_Per1.

IoHwAb_ReadADC – checks that the ADC1 conversion completed and disables the ADC1 conversion.  Reads the values from the ADC1 DMA buffer as well as the redundant Switched Battery Voltage from CDDInterface.  Converts all of these signals to engineering units and outputs them to the rest of the RTE.  Scheduled in the 2ms loop at the end of the forward path.  See ePWM component for minimum elapsed time between enabling and disabling the ADC conversion via the write of the ePWM4 CMPB value.

#### Adc

The intended DMA architecture uses two ADC conversion groups: ADC1 Group 2 (“slow” ADC) and ADC2 Group 1 (“fast” ADC).  Historically, ADC2 Event Group was used instead of ADC2 Group 1 – this may mean that integrating DMA will require a program to switch the ADC group being used.

#### MtrCtrl_Irq

If this is the first integration of DMA into a program, the existing ADC triggering mechanism will need to be removed and replaced with the method described above.  This will largely involve calling an IoHwAbstractionUsr runnable.  In addition, the ADC Conversion Complete flag will still need to be cleared (though it may have changed, see above), as well as the DMA interrupt that calls the MtrCtrl ISR.  It can be cleared as follows:

DMACTRLREG->BTCFLAG = (1 << 3)

#### uDiag

The following entries should be added to the Static Register Check list.  Note that these values are subject to change depending on which channels are enabled.

* These values are dependent on whether certain channels are enabled in the configuration.

The following entries should be defined as link-time determined.

* These values are dependent on whether certain channels are enabled in the configuration.

## Revision Control Log

| Module | Required Feature |

| --- | --- |

| Adc | Using ADC triggers for DMA transfers as well as ADC conversion group sizes to calculate buffer sizes.  Only required if ADC DMA channels are enabled.  Requires version FDD33C_008_and_FDD33E_002.3 or later. |

| SpiNxt | Using SPI Rx buffer full triggers for DMA transfers as well as SPI transfer group sizes to calculate DMA buffer sizes.  Only required if SPI DMA channels are used.  Requires version ASR038_2.3.0_8 or later. |

| uDiag | If the FlsTst channels are enabled, uDiag is responsible for initializing and enabling these blocks.  Requires version FDD32B_TMS570_uDiag_000.24 or later. |

| ePWM | Using NHET triggers for DMA transfers as well as NHET program addresses for destination addresses.  Only required if NHET DMA channels are enabled.  Requires version FDD34B_EPWM_NHETSENT_005.0 or later. |

| TMS570_Startup | Note that the DMA parity functionality requires version FDD32B_TMS570_Startup_000.19 or later in the bootloader. Note that DMA MPU startup test functionality requires FDD32B_TMS570_startup_000.21 or later in the application. |

| DiagMgr | Error reporting mechanism required if either of the slow SPI or ADC channels are enabled. |

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| None |  |  |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| MtrCtrl_Irq | 40 |  | If using the Fast ADC channel, update this to use IRQ40. |

| Constant | Notes | SWC |

| --- | --- | --- |

| D_DMAFLSTSTENABLED_CNT_ENUM | STD_ON or STD_OFF – used to enable the FlsTst DMA channels. | Dma_Cfg.h |

| D_FASTSPIGROUPENABLED_CNT_ENUM | STD_ON or STD_OFF – used to enable the MtrCtrl ISR SPI DMA channels. | Dma_Cfg.h |

| D_FASTADCGROUPENABLED_CNT_ENUM | STD_ON or STD_OFF – used to enable the MtrCtrl ISR ADC DMA channel. | Dma_Cfg.h |

| D_FASTPWMGROUPENABLED_CNT_ENUM | STD_ON or STD_OFF – used to enable the MtrCtrl ISR NHET and ePWM DMA channels. | Dma_Cfg.h |

| D_SLOWADCGROUPENABLED_CNT_ENUM | STD_ON or STD_OFF – used to enable the 2ms ADC DMA channel. | Dma_Cfg.h |

| DMA_PARITY_ENABLE | STD_ON or STD_OFF – used to enable the parity check.  This should be enabled on all programs – note that there is a required change in the bootloader to accommodate this. | appinit_cfg.h |

| DMA_REPORTERRORSTATUS | Set to NxtrDiagMgrX_ReportNTCStatus, where X is the application calling the group validity check functions. | Dma_Cfg.h |

|  |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| Dma_Init | Must be scheduled before FlsTst_Init (uDiag) | Init |

| Dma_SetupMtrCtrlGroups | Must be scheduled after Dma_Init.  Should be scheduled after other used peripherals are enabled (SPI, ADC, ePWM, NHET, CRC).  Should be scheduled before the MtrCtrl ISR is enabled.  Only required if any of the SPI, ADC, or PWM groups are enabled. | Init |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| Dma_SlowADCGroupValidity | Must be scheduled before the data is collected from the 2ms ADC buffer.  Only required if the slow ADC channel is used. | 2ms |

| Dma_InvalidateSlowADCGroup | Must be scheduled after the data is collected from the 2ms ADC buffer.  Only required if the slow ADC channel is used. | 2ms |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| DMA_START_SEC_VAR_CLEARED_UNSPECIFIED | All global DMA variables in RAM (source and destination). | This section can be mapped to an application only available in supervisor mode.  In this case, Dma_InvalidateSlowADCGroup will need to be accessed with a trusted function call. |

| DMA_START_SEC_VAR_CLEARED_BOOLEAN | DMA reset fail flag |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| None |  |  |

| Block Name |

| --- |

| None |

| Block Name |

| --- |

| None |

| Name | Address | Expected Value |

| --- | --- | --- |

| DMA_PAR0 * | 0xFFFFF094 | 0x44440440 |

| DMA_PAR1 * | 0xFFFFF098 | 0x04004000 |

| DMA_DMAPCR | 0xFFFFF1A8 | 0x0000000A |

| DMA_DMAMPCTRL * | 0xFFFFF1B0 | 0x0F090909 |

| DMA_DMAMPR0S | 0xFFFFF1B8 | 0xFF0A0000 |

| DMA_DMAMPR0E | 0xFFFFF1BC | 0xFF473FFF |

| DMA_DMAMPR1S | 0xFFFFF1C0 | 0xFCF78C00 |

| DMA_DMAMPR1E | 0xFFFFF1C4 | 0xFE0001FF |

| DMA_DMAMPR3S | 0xFFFFF1D0 | 0x00200000 |

| DMA_DMAMPR3E | 0xFFFFF1D4 | 0xFFFFFFFF |

| DMA_CP00_IDADDR * | 0xFFF80004 | 0xFE000068 |

| DMA_CP00_ITCOUNT * | 0xFFF80008 | 0x00010001 |

| DMA_CP00_CHCTRL * | 0xFFF80010 | 0x0000F000 |

| DMA_CP01_IDADDR * | 0xFFF80024 | 0xFE000060 |

| DMA_CP01_CHCTRL * | 0xFFF80030 | 0x0000F108 |

| DMA_CP02_ISADDR * | 0xFFF80040 | 0xFF0C0202 |

| DMA_CP02_ITCOUNT * | 0xFFF80048 | 0x00010003 |

| DMA_CP02_CHCTRL * | 0xFFF80050 | 0x0000511F |

| DMA_CP02_EIOFF * | 0xFFF80054 | 0x00020004 |

| DMA_CP03_ISADDR * | 0xFFF80060 | 0xFF3A0002 |

| DMA_CP03_ITCOUNT * | 0xFFF80068 | 0x00010004 |

| DMA_CP03_CHCTRL * | 0xFFF80070 | 0x0000511F |

| DMA_CP03_EIOFF * | 0xFFF80074 | 0x00020004 |

| DMA_CP05_IDADDR * | 0xFFF800A4 | 0xFF4600E8 |

| DMA_CP05_ITCOUNT * | 0xFFF800A8 | 0x00010001 |

| DMA_CP05_CHCTRL * | 0xFFF800B0 | 0x0007A101 |

| DMA_CP06_IDADDR * | 0xFFF800C4 | 0xFCF78C10 |

| DMA_CP06_CHCTRL * | 0xFFF800D0 | 0x0000511F |

| DMA_CP09_ISADDR * | 0xFFF80120 | 0xFF3E00F2 |

| DMA_CP09_ITCOUNT * | 0xFFF80128 | 0x00010004 |

| DMA_CP09_CHCTRL * | 0xFFF80130 | 0x0000511F |

| DMA_CP09_EIOFF * | 0xFFF80134 | 0x00020004 |

| DMA_CP12_ISADDR * | 0xFFF80180 | 0xFF0A0202 |

| DMA_CP12_ITCOUNT * | 0xFFF80188 | 0x00010003 |

| DMA_CP12_CHCTRL * | 0xFFF80190 | 0x0000511F |

| DMA_CP12_EIOFF * | 0xFFF80194 | 0x00020004 |

| Name | Address | Expected Value | Offset |

| --- | --- | --- | --- |

| DMA_DMAMPR2S * | 0xFFFFF1C8 | DMAData_G_str | 0 |

| DMA_DMAMPR2E * | 0xFFFFF1CC | DMAData_G_str | sizeof(DMAData_G_str) – 1U |

| DMA_CP02_IDADDR * | 0xFFF80044 | DMAData_G_str.FastSPI_Cnt_u16[0] | 0 |

| DMA_CP03_IDADDR * | 0xFFF80064 | DMAData_G_str.FastADC_Cnt_u16[0] | 0 |

| DMA_CP05_ISADDR * | 0xFFF800A0 | DMAData_G_str.PWMPeriod_Cnt_u32 | 0 |

| DMA_CP06_ISADDR * | 0xFFF800C0 | DMAData_G_str.PWMCmp_Cnt_u16[0][0] | 0 |

| DMA_CP09_IDADDR * | 0xFFF80124 | DMAData_G_str.SlowADC_Cnt_u16[0] | 0 |

| DMA_CP12_IDADDR * | 0xFFF80184 | DMAData_G_str.SlowSPI_Cnt_u16[0] | 0 |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 10-Apr-14 | OT |

| 2 | Updates for safety mechanisms, data integrity mechanisms (FDD 52 v001) | 30-Apr-14 | OT |

| 3 | Removed slow SPI integrity scheme functions (FDD 52 v002) | 02-May-14 | OT |

| 4 | Added DMA Reset Failed global output per ES-52 v004; updated  section 7.2.* per ES 52 v004 and latest updates to associated components | 31-Jan-2015 | KMC |

|  |  |  |  |
