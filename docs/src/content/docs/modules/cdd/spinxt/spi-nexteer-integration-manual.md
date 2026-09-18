---
title: 'Spi Nexteer Integration Manual'
description: 'Converted design document: Spi Nexteer Integration Manual'
---

> **Source:** `SpiNxt/doc/Spi_Nexteer_Integration_Manual.docx`  
> **Module:** [SpiNxt](../../../../cdd/spinxt/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual -- Spi Nexteer

## Dependencies

### SWCs

### Global Functions(Non RTE) to be provided to Integration Project

void SpiNxt_Init(void);

Std_ReturnType SpiNxt_AsyncTransmit( Spi_SequenceType Sequence );
NOTE that this function is hardcoded for use with the Turns Counter component and returns E_NOT_OK when SpiNxt not configured for use with Turns Counter (see section 2.2.1).

Spi_SeqResultType SpiNxt_GetSequenceResult( Spi_SequenceType Sequence );

Std_ReturnType SpiNxt_SetupEB(    Spi_ChannelType Channel,
    P2CONST(Spi_DataType, AUTOMATIC, SPI_APPL_DATA) SrcDataBufferPtr,
    P2VAR(Spi_DataType, AUTOMATIC, SPI_APPL_DATA) DesDataBufferPtr,
    Spi_NumberOfDataType Length);
NOTE that this function is hardcoded for use with the Turns Counter component and returns E_NOT_OK when SpiNxt not configured for use with Turns Counter (see section 2.2.1).

void  mibspiSetData(const mibspiBASE_t *mibspi, uint32 group, const uint16 data[]);

void mibspiSetCtrlData(const mibspiBASE_t *mibspi, uint32 group, const uint32 data[]);

uint32 mibspiGetData(const mibspiBASE_t *mibspi, uint32 group, uint16 data[]);
NOTE this function is optimized for use by the Digital MSB component when SpiNxt is configured for use with Digital MSB (see section 2.2.1).  In that configuration, the mibspi argument must be equal to the base register address of mibspi3 or mibspi5, and the data argument must be the receive data buffer for the caller.

void mibspiTransfer(mibspiBASE_t *mibspi, uint32 group);

## Configuration

### Build Time Config

### Configuration Files to be provided by Integration Project

#### Da Vinci Parameter Configuration Changes

#### Da Vinci Interrupt Configuration Changes

#### Manual Configuration Changes

## Integration

### Required Global Data Inputs

<None>

### Required Global Data Outputs

<None>

### Specific Include Path present

<Yes>

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

<Define all the preprocessor Macros needed and conditions when needed>.

### Optimization Settings

<Define Optimization levels that are needed and conditions when needed>.

## Revision Control Log

| Module | Required Feature |

| --- | --- |

| Dio | Dio_WriteChannel() when SpiNxt used with Turns Counter |

| TMS570 MIBSPI3 and MIBSPI5 peripheral | Exclusive access to the MIBSPI3 and MIBSPI5 peripheral registers.<br/>MIBSPI3 CS3 provided as a No Connect pin on CCA design when SpiNxt used with Turns Counter |

| Os | Category 2 ISR mapping for MIBSPI3 IRQ sources when SpiNxt used with Turns Counter |

| TurnsCounter | TurnsCounter_TxConfirmation() when SpiNxt used with Turns Counter |

| ePWM | Must provide SPI transmit trigger on N2HET1[14] for mibspi3, and N2HET1[18] for mibspi5, when SpiNxt used with Digital MSB. |

| Modules | Notes |

| --- | --- |

| None |  |

| Parameter | Notes | SWC |

| --- | --- | --- |

| Dio Channel Name: “SPI_TCCS” | Chip Select DIO output mapped to the turns counter chip select pin when used with Turns Counter | Dio |

| All MIBSPI3 and MIBSPI5 configuration | The third party Spi driver shall be configured such that it does not read/write any of the MIBSPI3 or MIBSPI5 control registers. | Spi |

| Port pin SPI3CLK: SPI Output |  | Port |

| Port pin SPI3NCS3: SPI Output | When used with Turns Counter | Port |

| Port pin SPI3NCS0: SPI Output | When used with Digital MSB | Port |

| Port pin SPI3SIMO: SPI Output |  | Port |

| Port pin SPI3SOMI: SPI Input |  | Port |

| Port pin SPI5CLK: SPI Output |  | Port |

| Port pin SPI5NCS0: SPI Output | When used with Digital MSB | Port |

| Port pin SPI5SIMO: SPI Output |  | Port |

| Port pin SPI5SOMI: SPI Input | When used with Digital MSB | Port |

| SPINXT_EXCLUSIVE_AREA_0 | This exclusive are covers the events that need to be synchronized to minimize jitter on the CS to SCLK delay specified by the TurnsCounter FDD 20C (when used with Turns Counter) | SchM |

| SpiNxtGeneral\ SpiNxtUseWith | This parameter controls generation of the SpiNxt_Cfg.h file.  Set to D_SPINXT_USEWITHTC for use with the PIC Turns Counter, or set to D_SPINXT_USEWITHDIGMSB for use with the Digital MSB.<br/>When this parameter is set to D_SPINXT_USEWITHTC, the SpiNxt.h file provides the following constants which previously were manually configured: SPI_TCDATA_CH, SPI_TCDATA_SEQ, D_SPINXTNUMCHAN_CNT_U16, and CALL_MIBSPI3_NOTIFFCN(). | SpiNxt |

|  |  |  |

|  |  |  |

| ISR Name | Notes | SWC |

| --- | --- | --- |

| SpiNxt_IrqUnit2TxRx: MIBSPI3 level 0 interrupt | Category 2 interrupt mapped to Mibspi3 RxTx interrupt source when used with Turns Counter | Os |

| SpiNxt_IrqUnit2TxRxERR: MIBSPI3 level 1 interrupt | Category 2 interrupt mapped to Mibspi3 RxTx error interrupt source when used with Turns Counter | Os |

| Constant | Notes | SWC |

| --- | --- | --- |

| None |  |  |

| Init | Scheduling Requirements | Trigger |

| --- | --- | --- |

| SpiNxt_Init() | Must be executed prior to using any of the module C/S API. | Init |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

|  |  |  |

| Constant | Notes |

| --- | --- |

| SPINXT_START_SEC_VAR_CLEARED_UNSPECIFIED |  |

| SPINXT_START_SEC_CODE |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| Full driver |  |  |

| Block Name |

| --- |

| <None > |

| Block Name |

| --- |

| <None > |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1 | Initial version |  | JJW |

| 2 | 2 | Added exclusive area configuration and Category 2 interrupt configuration |  | JJW |

| 3 | 3 | Added ISR MIBSPI level configuration requirement |  | JJW |

| 4 | 4 | New Notification build configuration parameter |  | JJW |

| 5 | 5 | Changes and additions for configurability of SpiNxt to be used with PIC Turns Counter or with Digital MSB. | 8/2/13 | KMC |

|  |  |  |  |  |
