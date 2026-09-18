---
title: 'StaMd Integration Manual'
description: 'Converted design document: StaMd Integration Manual'
---

> **Source:** `StaMd/doc/StaMd_Integration_Manual.docx`  
> **Module:** [StaMd](../../../../asw/stamd/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual - StaMd

Table of Contents

1	Dependencies	2

1.1	SWCs	2

1.2	Functions to be provided to Integration Project	2

2	Configuration	3

2.1	Build Time Config	3

2.2	Configuration Files to be provided by Integration Project	3

2.2.1	Da Vinci Config generation	3

2.2.2	Manual Configuration Changes	3

3	Integration	4

3.1	Required Global Data Inputs	4

3.2	Optional Global Data Inputs	4

3.3	Specific Include Path present	4

4	Runnable Scheduling	5

5	Memory Mapping	6

5.1	Mapping	6

5.2	Usage	6

5.3	NvM Blocks	6

6	Compiler Settings	6

6.1	Preprocessor MACRO	6

6.2	Optimization Settings	6

7	Revision Control Log	7

## Dependencies

### SWCs

Note : Referencing the external components should be avoided in most cases. Only in unavoidable circumstance external components should be refered. Developer should track the references.

### Global Functions(Non RTE) to be provided to Integration Project

extern FUNC(void, MCU_CODE) Mcu_PerformReset(void);

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

### Ap_StaMd_Cfg.h

#### Da Vinci Parameter Configuration Changes

#### DaVinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

### Required Global Data Outputs

### Specific Include Path present

The …StaMd/include patch needs to be added to the include search path of the CCS project. Typical setting: "${workspace_loc:/FORD_S550_P552/StaMd/include}"

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

<Define all the preprocessor Macros needed and conditions when needed>.

### Optimization Settings

<Define Optimization levels that are needed and conditions when needed>.

## Revision Control Log

| Module | Required Feature |

| --- | --- |

| ECUStatup.c | StaMd_Init0 needs to be called from EcuStartup_Init2 via a trusted wrapper after Nvm ‘read all’ is complete, by calling Call_StaMd_Init0. <br/>ECUStartup needs to also include the Ap_StaMd.h header file. <br/>The StaMd_Init0 is defined outside of the RTE and is responsible for updating Type H memory across applications at start up.  StaMd_Init0 needs to be added to a non-trusted function list in a trusted application in the O.S. |

| NtWrap.c, .h, O.S changes | Add trusted function call to NtWrap : <br/><br/>/* Trusted wrapper Function */<br/>void TRUSTED_NtWrapS_StaMd_Init0<br/>(TrustedFunctionIndexType FunctionIndex, TrustedFunctionParameterRefType FunctionParams)  <br/>{<br/>   StaMd_Init0();<br/>} <br/>…<br/>void Call_StaMd_Init0(void)<br/>{<br/>   (void) CallTrustedFunction<br/>   (NtWrapS_StaMd_Init0,<br/>   (TrustedFunctionParameterRefType)0);<br/>} |

|  |  |

| Modules | Notes |  |

| --- | --- | --- |

| <None> |  |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| TypeHDataSize | Total size of all Type H data in bytes |  |

| StaMdCPEnable | This container contains the configuration (parameters) for the StaMd Watchdog checkpoints. |  |

| StaMdTODType | This container defines the configuration for the type of TOD implementation used:<br/>TOD_2msToggle<br/>TOD_SteadyState (*common setting)<br/>TOD_None |  |

| StaMdNvMWriteAllAPI | This container defines the API used for the NvM Write All function. (*common setting is NvMProxy_WriteAll if the NvM proxy is used). |  |

| StaMdNvMGetErrorStatusAPI | This container defines the API used for the NvM Get Error Status function. (*common setting is NvMProxy_GetErrorStatus if the NvM proxy is used). |  |

| StaMdTrnsDiagMgrShtDwnTaskActivation | This container defines the DiagMgr shutdown function. If StaMdCoreOsAppRef matches the application referenced for DiagMgrDemIfOsAppRef in DiagMgr then the generated output will be a client/server call and this field is ignored. If they do not match, then a task activation call is created and the task defined in this field is activated. <br/>NOTE: Typical setting is Task_TrnsB_9 for the application 9 transition function, from which the StaMd9_Trns_DemShutdown function is called in some programs. |  |

| GenerateExcludeOsAppRef | This parameter defines the application(s) which do not require a States and Modes component. |  |

| StaMdCoreOsAppRef | This parameter defines the application which contains the core States and Modes component. |  |

| StaMdsComOsAppRef | This parameter defines the application which interfaces with the serial communications functions. |  |

| StaMdSysCovOsAppRef | This parameter defines the application which performs the states and modes systematic coverage. |  |

| ISR Name | VIM # | Priority Dependency | Notes |

| --- | --- | --- | --- |

| <None> |  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

| <None> |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| None | None | Init |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

|  |  | 10ms |

| Memory Section | Contents | Notes |

| --- | --- | --- |

| STAMD_START_SEC_VAR_SAVED_ZONEHGS_32<br/>STAMD_START_SEC_VAR_SAVED_ZONEHGS_8 |  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| <Memmap usuage info> |  |  |

| Block Name |

| --- |

| <None > |

| Block Name |

| --- |

| None |

| Rev # | Change Description | Date | Author |

| --- | --- | --- | --- |

| 1 | Initial version | 12-Dec-13 | BDO |

|  |  |  |  |
