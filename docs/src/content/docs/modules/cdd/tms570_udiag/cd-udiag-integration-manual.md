---
title: 'Cd uDiag Integration Manual'
description: 'Converted design document: Cd uDiag Integration Manual'
---

> **Source:** `TMS570_uDiag/doc/Cd_uDiag_Integration_Manual.docx`  
> **Module:** [TMS570_uDiag](../../../../cdd/tms570_udiag/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual –Cd_uDiag

Table of Contents

1	Dependencies	2

1.1	SWCs	2

1.2	Functions to be provided to Integration Project	2

2	Configuration	3

2.1	Build Time Config	3

2.2	Configuration Files to be provided by Integration Project	3

2.2.1	Da Vinci Parameter Configuration Changes	4

2.2.2	DaVinci Interrupt Configuration Changes	5

2.2.3	Manual Configuration Changes	5

3	Integration	6

3.1	Required Global Data Inputs	6

3.2	Optional Global Data Inputs	6

3.3	Specific Include Path present	6

4	Runnable Scheduling	6

5	Memory Mapping	7

5.1	Mapping	7

5.2	Usage	7

5.3	NvM Blocks	7

6	Compiler Settings	7

6.1	Preprocessor MACRO	7

6.2	Optimization Settings	7

7	Revision Control Log	8

## Dependencies

NOTE – the TMS570_uDiag component includes both uDiag and FlsTst functionality.  For complete integration information on the TMS570_uDiag component, also see the FlsTst integration manual (in the TMS570_uDiag\doc folder).

### SWCs

NOTES:

*When uDiagEnableFPUDiag is set to STD_OFF, the floating point exception diagnostic is disabled and EnableVFPInterrupt() is optional.

**_fiqhandler needed only if configuring Mcu_FpuIrq  as an interrupt (see section 2.2.2).

*** EnableESMLInterrupt() is now called from a function in the TMS570_uDiag component, as of component version FDD32B_TMS570_uDiag_000.23.  When using component version FDD32B_TMS570_uDiag_000.23 or later, any other call(s) to the EnableESMLInterrupt()  function, e.g. in EcuStartup, must be removed. This fixes anomaly 6133.

**** DmaRstFail needed only when DMA_MPU_ENABLE is set to STD_ON; Htu1RstFail needed only when N2HET1TU_MPU_ENABLE is set to STD_ON; Htu2RstFail needed only when N2HET2TU_MPU_ENABLE is set to STD_ON.  See section 2.2.3.

### Functions to be provided to Integration Project

< Global function (except the ones that are defined in RTE modules) that is defined in this component but used by other function>

FUNC(void, CD_UDIAG_APPL_CODE) uDiagFPU_Init1(void);

FUNC(void, CD_UDIAG_APPL_CODE) uDiagFPU_Init2(void);

UDIAG_COMPILER_ISR void Mcu_FpuIrq(void);

FUNC(void, CD_UDIAG_APPL_CODE) uDiagCCRM_Init(void);

FUNC(void, CD_UDIAG_APPL_CODE) uDiagClockMonitor_Init(void);

FUNC(void, CD_UDIAG_APPL_CODE) uDiagECC_Init(void);

FUNC(void, CD_UDIAG_APPL_CODE) uDiagESM_Init(void);

FUNC(void, CD_UDIAG_APPL_CODE) uDiagIOMM_Init(void);

FUNC(void, CD_UDIAG_APPL_CODE) uDiagParity_Init(void);

FUNC(void, CD_UDIAG_APPL_CODE) uDiagPeriphMPU_Init(void);

FUNC(void, CD_UDIAG_APPL_CODE) uDiagStaticRegs_Init(void);

FUNC(void, CD_UDIAG_APPL_CODE) uDiagVIM_Init(void);

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

uDiag_Cfg.c generated from uDiag_Cfg.c.tt

uDiag_Cfg.h generated from uDiag_Cfg.h.tt

#### Da Vinci Parameter Configuration Changes

*The uDiagGladiatorCompatible parameter selects ESM Group 1 Channel 7 (as used on Gladiator) vs Group 1 Channel 34 (as used on Champion) for NHET2 Parity Error.  On programs where code compatibility is required, the Gladiator ESM configuration must be used, because the Champion configuration enables an interrupt that is Reserved for Gladiator.  NOTE that on Champion parts running code configured as Gladiator-compatible, an NHET2 RAM Parity Error will trigger only a Critical Registers Verification Fault , with no NHET2 RAM Fault diagnostic.

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

*Note – these enable parameters must be defined for the TMS570_uDiag component.  They should be #defined to either STD_ON or STD_OFF as directed for the specific application/integration project; in general they will be on when the corresponding peripheral is used and off when it is not used, but there are application-specific exceptions.  Some of the enable parameters are also used by other components.  In addition, there may be other similar enable parameters used by other components which are not currently used in the uDiag component.

## Integration

### Required Global Data Inputs

<Mention any global variable that this component requires from other components>

ResetCause_Cnt_Enum

Dma_DmaRstFail_Cnt_G_lgc (when DMA_MPU_ENABLE is set to STD_ON)

Nhet_Htu1RstFail_Cnt_G_lgc (when N2HET1TU_MPU_ENABLE is set to STD_ON)

Nhet_Htu2RstFail_Cnt_G_lgc (when N2HET2TU_MPU_ENABLE is set to STD_ON)

### Optional Global Data Inputs

<Mention any global variable that this component requires for other components>

### Specific Include Path present

<Yes>

## Runnable Scheduling

This section specifies the required runnable scheduling.

*NOTE: When uDiagEnableFPUDiag is set to STD_OFF, the floating point exception diagnostic is disabled and the calls to uDiagFPU_Init1() and uDiagFPU_Init2() are optional.

## Memory Mapping

### Mapping

* Each …START_SEC… constant is terminated by a …STOP_SEC… constant as specified in the AUTOSAR Memory Mapping requirements.

### Usage

Table 1: ARM Cortex R4 Memory Usage

### NvM Blocks

Note : Size of the NVM block if configured in developer

## Compiler Settings

### Preprocessor MACRO

<Define all the preprocessor Macros needed and conditions when needed>.

### Optimization Settings

## Revision Control Log

| Module | Required Feature |

| --- | --- |

| TMS570_Startup | _coreGetFPSCR_()<br/>_coreGetSecondaryAuxiliaryControlRegister_()<br/>_coreSetSecondaryAuxiliaryControlRegister_()<br/>Reset Causes <br/>_fiqhandler** |

| Basic System Services | EnableVFPInterrupt()*<br/>EnableESMLInterrupt()*** |

| Dma | Dma_DmaRstFail_Cnt_G_lgc**** |

| Nhet | Nhet_Htu1RstFail_Cnt_G_lgc****<br/>Nhet_Htu2RstFail_Cnt_G_lgc**** |

| Modules | Notes |  |

| --- | --- | --- |

| None |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| uDiagGeneral\uDiagEnableFPUDiag | When set to STD_ON,the floating point exception diagnostic is enabled.  When set to STD_OFF, the diagnostic is disabled, the EnableVFPInterrupt() function (see section 1.1) is optional, interrupt configuration of Mcu_FpuIrq (see section 2.2.2) is optional, and the calls to uDiagFPU_Init1() and uDiagFPU_Init2() (see section 4) are optional. | TMS570_uDiag |

| OsOSFIQHandler\NONO_AUTO\OsOSFIQHandler | Must be set to “_fiqhandler” when Mcu_FpuIrq is configured as an interrupt.  (See section 2.2.2). | Os |

| uDiagGeneral\uDiagGladiatorCompatible | Must be set to STD_ON for programs where code compatibility is required between Gladiator and Champion parts.*  Set to STD_OFF for programs where only Champion parts are used. | TMS570_uDiag |

| uDiagGeneral\uDiagVIMPerTrusted | Set to STD_ON when uDiagVIM_Per() is called from a trusted task.  Set to STD_OFF when uDiagVIM_Per() is called from a non-trusted task. NOTE that when this parameter is set to STD_OFF, the void function TWrapS_uDiagVIM_RednRpdShtdn(void) must be added as a trusted function. | TMS570_uDiag |

| uDiagGeneral\uDiagECCPerTrusted | Set to STD_ON when uDiagECC_Per() is called from a trusted task.  Set to STD_OFF when uDiagECC_Per() is called from a non-trusted task. NOTE that when this parameter is set to STD_OFF, the void function TWrapS_uDiagECC_RednRpdShtdn(void) must be added as a trusted function. | TMS570_uDiag |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| Mcu_FpuIrq | 47 | higher priority than any other FIQ that uses floating point | Must be an FIQ and Category 1 when configured, and if FIRQPR0 is included in the runtime register check, its value needs to be changed in the RuntimeRegCheck configuration.  When uDiagEnableFPUDiag is set to STD_OFF, the floating point exception diagnostic is disabled and  the interrupt configuration of Mcu_FpuIrq is optional. |

| Isr_ESMH | 0 | Highest priority FIQ | Must be FIQ and Category 1 |

| Isr_ESML | 20 |  | Must be IRQ and Category 2 |

|  |  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| N2HET1_PARITY_ENABLE | *See note | Appinit_cfg.h |

| N2HET2_PARITY_ENABLE | *See note | Appinit_cfg.h |

| N2HET1TU_PARITY_ENABLE | *See note | Appinit_cfg.h |

| N2HET2TU_PARITY_ENABLE | *See note | Appinit_cfg.h |

| MIBADC1_PARITY_ENABLE | *See note | Appinit_cfg.h |

| MIBADC2_PARITY_ENABLE | *See note | Appinit_cfg.h |

| DCAN1_PARITY_ENABLE | *See note | Appinit_cfg.h |

| DCAN2_PARITY_ENABLE | *See note | Appinit_cfg.h |

| VIM_PARITY_ENABLE | *See note | Appinit_cfg.h |

| DMA_PARITY_ENABLE | *See note | Appinit_cfg.h |

| DMA_MPU_ENABLE | *See note | Appinit_cfg.h |

| N2HET1TU_MPU_ENABLE | *See note | Appinit_cfg.h |

| N2HET2TU_MPU_ENABLE | *See note | Appinit_cfg.h |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| uDiagCCRM_Init | Before the OS is started | ECU Startup |

| uDiagClockMonitor_Init | Before the OS is started | ECU Startup |

| uDiagECC_Init | Before the OS is started | ECU Startup |

| uDiagESM_Init | Before the OS is started | ECU Startup |

| uDiagIOMM_Init | Before the OS is started | ECU Startup |

| uDiagParity_Init | Before the OS is started | ECU Startup |

| uDiagPeriphMPU_Init | Before the OS is started | ECU Startup |

| uDiagStaticRegs_Init | Before the OS is started | ECU Startup |

| uDiagVIM_Init | Before the OS is started | ECU Startup |

| uDiagFPU_Init1* | Before the OS is started | ECU Startup |

| uDiagFPU_Init2* | After the OS is started, before any code that uses floating point | ECU Startup |

| uDiagPeriphStartup_Init | After DiagMgr initialization | RTE (Init) |

| uDiagResetHandler_Init | After DiagMgr initialization | RTE (Init) |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

| <Runnable name> | None | RTE/ISR(<time>ms) |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| UDIAG_START_SEC_VAR_SAVED_UNSPECIFIED | FPUExceptionAddr_Cnt_D_u32 | do not clear on reset |

| UDIAG_START_SEC_VAR_CLEARED_UNSPECIFIED |  |  |

| UDIAG_START_SEC_VAR_CLEARED_BOOLEAN |  |  |

| UDIAG_START_SEC_VAR_CLEARED_16 |  |  |

| UDIAG_START_SEC_VAR_CLEARED_32 |  |  |

| WDGRESETHANDLER_START_SEC_VAR_POWER_ON_CLEARED_8 |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| <Memmap usuage info> |  |  |

| Block Name |

| --- |

| <NvM Block Info> |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version – includes information for Cd_uDiagFPU and Cd_uDiagUtility only | 6-Jun-2013 | Kathleen Creager |

| 2 | Added uDiagGeneral\uDiagEnableFPUDiag to configuration parameters, and related notes, for enabling/disabling floating point exception diagnostic. Added “Category 1” and mention of Runtime Register Check to notes on configuring Mcu_FpuIrq. Added OsOSFIQHandler configuration parameter.  Clarified scheduling requirements on uDiagFPU_Init2(). | 26-Jun-13 | KMC |

| 3 | Added information on parameters uDiagGladiatorCompatible and uDiagVIMPerTrusted,FlsTstBlockSize,  interrupt routines, and optimization settings as needed for changes made  to fix anomalies 5403, 5801, 5491, 5809, and 5810.  NOTE that this integration manual is not complete; it includes only information related to changes made to the component beginning in June 2013.. | 16-Oct-13 | KMC |

| 4 | Updated for change to call init functions from EcuStartup instead of as RTE init functions, and removed unneeded instructions about inlining compiler directive, both changes per CR11158. Added dependency and note regarding EnableESMLInterrupt()  per CR 11157. Other misc cleanup. | 06-Jan-14 | KMC |

| 5 | Added uDiagPeriphMPU_Init runnable, added PARITY_ENABLE and MPU_ENABLE configuration parameters | 09-Apr-14 | KMC |

| 6 | Added uDiagPeriphStartup_Init runnable and related dependencies and global variables | 31-Jan-15 | KMC |

|  |  |  |  |
