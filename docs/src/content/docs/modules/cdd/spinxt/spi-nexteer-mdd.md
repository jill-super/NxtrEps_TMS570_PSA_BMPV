---
title: 'Spi Nexteer MDD'
description: 'Converted design document: Spi Nexteer MDD'
---

> **Source:** `SpiNxt/doc/Spi_Nexteer_MDD.docx`  
> **Module:** [SpiNxt](../../../../cdd/spinxt/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

## Module  -- Spi Driver

## High-Level Description

This module provides the following Autosar API:

- Spi_SetupEB()

- Spi_Init()

- Spi_AsyncTransmit()

- Spi_GetSequenceResult()

This module provides the following TI Halcogen API:

- mibspiSetCtrlData() – Note: this is a modified form of the standard mibspiSetData() API

- mibspiTransfer()

- mibspiGetData()

- mibspiSetData()

The Autosar API naming has been altered from the Autosar standard to allow co-existence of this module and a Third Party Spi driver implementation in the same project.  SWC’s operating within the Rte can be mapped to either the Spi service ports offered by this BSW or the Third Parties Spi driver service ports by only changing the Rte service port mapping.

This driver exists to provide configurations/use cases that cannot provided by the third party Spi driver due to limitations in the design of the module.

The subset of the Texas Instruments Halcogen mibspi API  is provided specifically to support the Turns Counter Flash Programming SWC and the Digital MSB SWC.  If the Turns Counter Flash Programming SWC design and the Digital MSB design changed to use the standard Autosar API, then the provided mibspi API could be changed to module internal functions or removed.  However, the requirements of the Digital MSB component are such that its SPI usage does not fit easily into the Autosar API definition (more detail provided in section 9).

### References

PIC16(L)F1847 Data Sheet – DS41453B (41453B.pdf)

Turns Counter Column Position Sensor FDD 20C (FDD 20C Turns Counter Column Position Sensor (BMW EA3) Rev 03.doc)

TMS570LS31x/21x 16/32-Bit RISC Flash Microcontroller Technical Reference Manual – September 2011 (spnu499.pdf)

Specification of the SPI Handler/Driver v3.0.0 (AUTOSAR_SWS_SPIHandlerDriver.pdf)

Turns Counter Flash Programming FDD 98 Rev 002

Digital MSB FDD ES50ARev00

Allegro A1331 Data Sheet Addendum – Programming Reference A1331-ADD1

## Figures

### Diagram – Function Data Sharing

This diagram shows all data that is shared between functions within the module.

#### Diagram – Function (Name)

This diagram describes the functional characteristics and data flow of a given function.

(Note – This is not mandatory, only used where a graphical representation helps explain the function.  It is left to the author’s discretion.  New headers of this level (Level 3) should be created for each function.

## Variable Data Dictionary

For details on module input / output variable, refer to the Data Dictionary for the application.  Input / output variable names are listed here for reference.

(Note: Full variable names required in table.)

(Note: All global variables including End Of Line data used should be shown here)

### Module Internal Variables

This section identifies the name, range and resolutions for module specific data created by this module.  If there are no range restrictions on the variable, the term “FULL” is placed into the table for legal range.

#### User defined typedef definition/declaration

This section documents any user types uniquely used for the module.

## Constant Data Dictionary

### Calibration Constants

This section lists the calibrations used by the module.  For details on calibration constants, refer to the Data Dictionary for the application.

### Program(fixed) Constants

#### Embedded Constants

All embedded constants whose values are provided in Eng units will be evaluated to the equivalent counts by using the FPM_InitFixedPoint_m() macro within the #define statement.

##### Local

##### Global

This section lists the global constants used by the module.  For details on global constants, refer to the Data Dictionary for the application.

#### Module specific Lookup Tables Constants

(This is for lookup tables (arrays) with fixed values, same name as other tables)

## Functions/Macros used by the Sub-Modules

### Library Functions / Macros

The library and functions / Macros that are called by the various sub modules are identified below,

CALL_MIBSPI3_NOTIFFCN()

### Data Hiding Functions

<None>

### Global Functions/Macros Defined by this Module

#### Spi Setup External Buffer

##### Description

This driver function is a minimalist implementation intended for use with the Turns Counter component.  Additionally this function does not provide any error detection at this time. The function body is conditionally compiled such that the SetupEB functionality is provided when D_SPINXTUSEWITH_CNT_ENUM == D_SPINXT_USEWITHTC, and the function simply returns E_NOT_OK when D_SPINXTUSEWITH_CNT_ENUM has any other value.

#### Spi Get Sequence Result

##### Description

#### MIBSPI Transfer

##### Description

Set the Enable Transfer Group bit in the appropriate register to the transfer of the mibspi transfer group defined by the arguments:

mibspi->TGCTRL[group] |= 0x80000000UL

#### Spi Asynchronous Transmit

##### Description

This driver function is a minimalist implementation intended for use with the Turns Counter component.  It assumes one-to-one channel-to-sequence correspondence.  The function body is conditionally compiled such that the Turns Counter-specific Asynchrounous Transmit functionality is provided when D_SPINXTUSEWITH_CNT_ENUM == D_SPINXT_USEWITHTC, and the function simply returns E_NOT_OK when D_SPINXTUSEWITH_CNT_ENUM has any other value.

#### MIBSPI Set Data

##### Description

This function copies transmit data from the data[] argument into the appropriate mibspi ram transmit buffer, as selected by the mibspi and group arguments.  It is based on the Halcogen function of the same name.

#### MIBSPI Set Control and Data

##### Description

This function copies transmit control and data words from the data[] argument into the appropriate mibspi ram transmit buffer, as selected by the mibspi and group arguments.  It is based on the Halcogen function mibspiSetData, modified to copy the complete transmit buffer including both control and data

#### MIBSPI Get Data

##### Description

This function copies receive data from the appropriate mibspi ram receive buffer, as selected by the mibspi and group arguments, into the data[] argument.  It is based on the Halcogen function of the same name, modified to optimize for use with the Digital MSB since it will be called from the Motor Control ISR.  The function is conditionally compiled such that optimized Digital MSB specific functionality is provided when D_SPINXTUSEWITH_CNT_ENUM == D_SPINXT_USEWITHDIGMSB, and the original Halcogen functionality is provided when D_SPINXTUSEWITH_CNT_ENUM has any other value.

### Local Functions/Macros Used by this MDD only

#### MIBSPI Set Data 8 Bit

##### Description

This function copies transmit data from the data[] argument into the appropriate mibspi ram transmit buffer, as selected by the mibspi and group arguments.  It  is based on the Halcogen function mibspiSetData, modified to copy from a uint8 buffer rather than uint16.

#### MIBSPI Get Data 8 Bit

##### Description

This function copies receive data from the appropriate mibspi ram transmit buffer, as selected by the mibspi and group arguments, into the data[] argument.  It  is based on the Halcogen function mibspiGetData, modified to copy to a uint8 buffer rather than uint16.

#### MIBSPI Enable Group Notification

##### Description

This function enables the transfer group interrupt for the mibspi, transfer group, and interrupt level defined by the arguments.

#### MIBSPI Notification

##### Description

This is an error callback that is provided by the application and is called on an error interrupt.  The parameter passed to the callback is a copy of the error interrupt flag register.  It is hardcoded for channel 0/sequence 0 and the Turns Counter application.  Because it is hardcoded for the Turns Counter application, it is conditionally compiled such that it provides the Turns Counter error callback functionality when compiled with D_SPINXTUSEWITH_CNT_ENUM == D_SPINXT_USEWITHTC, and returns without doing anything when compiled with D_SPINXTUSEWITH_CNT_ENUM set to any other value.

#### MIBSPI Group Notification

##### Description

This is a callback function provided by the application.  It is called when a transfer is complete.  The parameter is the transfer group that triggered the interrupt. This driver is designed to only receive data on mibspi3 group 0 for the Turns Counter communication function.   Because it is hardcoded for the Turns Counter application, it is conditionally compiled such that it provides the Turns Counter error callback functionality when compiled with D_SPINXTUSEWITH_CNT_ENUM == D_SPINXT_USEWITHTC, and returns without doing anything when compiled with D_SPINXTUSEWITH_CNT_ENUM set to any other value.

## Software Module Implementation

### Runtime Environment (RTE) Initial Values

This section lists the initial values of data written by this module but controlled by the RTE. After RTE initialization, the data in this table will contain these values.

### Initialization Functions

#### Init: SpiNxt_Init

##### Design Rationale

The initialization function initializes mibspi3 and mibspi5 registers as needed by the Turns Counter and Turns Counter Flash Programming components, or by the Digital MSB component, controlled by a SpiNxt configuration parameter (see Integration Manual) which controls a constant value in the generated SpiNxt_Cfg.h file.  The initialization values are hardcoded in the SpiNxt.h file and are specified by the Turns Counter (), Turns Counter Reflash (FDD98) and Digital MSB () FDDs.

Additional information regarding initialization of MIBSPI3 when used by Turns Counter (per FDD20C):

The actual chip select for the PIC Turns Counter SPI transfers on MIBSPI3 uses a Dio channel, configured by the Dio and Port components as SPI_TCCS.  The required chip select hold time before SPI clocking begins is controlled by the use of the MIBSPI3 tick counter  triggering the SPI transfer.  (See SpiNxt_AsyncTransmit and the value of MIBSPI3_TICKCNT.)

The Dio chip select must remain low throughout the 10 byte transfer, with a minimum 9.5 usec delay between bytes.  It is desired to implement the 9.5 usec delay in  hardware.  In order to accomplish this with the TMS570 SPI peripheral, it is necessary to use the C2TDELAY, the T2CDELAY, and WDELAY as the sum of all three is needed to reach the desired delay time at an 80MHz VCLK rate.  More details provided in the C2TDELAY, T2CDELAY, and WDELAY sections of the tables below, to explain the values of MIBSPI3_DELAY and MIBSPI3_FMT0.

However, use of C2TDELAY and T2CDELAY requires transmit control words configured to use a MIBSPI3 chip select pin and to release the chip select between transfers.  Therefore a “dummy” SPI chip select is used in the control words in the transmit buffer (see value of MIBSPI3_BUFRAMCTRLINIT).  This chip select is toggled during the SPI transfer but only to accomplish the delay timing; it is not toggling a pin on the PIC Turns Counter.

##### Module Outputs

None

##### Module Internal

### Periodic Functions

None

### Fault Recovery Functions

None

### Shutdown Functions

None

### Interrupt Functions

#### Isr: _IrqUnit2TxRx

##### Design Rationale

None

##### Program Flow Start

None

##### SpiNxt_IrqUnit2TxRx

##### Program Flow End

None

#### Isr: _IrqUnit2TxRxERR

None

##### Program Flow Start

None

##### SpiNxt_IrqUnit2TxRxERR

##### Program Flow End

None

### Serial Communication Functions

None

## Execution Requirements

### Execution Sequence of the Module

(Describe in words relevant details about the execution sequence of the different sub modules.)

### Execution Rates for sub-modules called by the Scheduler

This table serves as reference for the Scheduler design

### Execution Requirements for Serial Communication Functions

## Memory Map Definition Requirements

### Sub Modules (Functions)

This table identifies the software segments for functions identified in this module.

### Local Functions

This table identifies the software segments for local functions identified in this module.

## Known Issues / Limitations With Design

Driver has several functions and all initializations hardcoded for what is needed by the Turns Counter , the Turns Counter Reflash, or the Digital MSB.  Future modifications of the SPI interface of those components will probably require changes to this driver.  New uses of the SPI driver would also require driver changes.  Currently the only configurability is through the configuration parameter SpiNxt/SpiNxtGeneral/SpiNxtUseWith which selects either Turns Counter or Digital MSB functionality.

The Autosar API was not implemented for use by the Digital MSB for the following reasons:
a) The digital MSB triggers SPI transfers external to the SPI driver, through the NHET as set up in the ePWM component.  This means the SpiNxt_AsyncTransmit () function (if implemented for use by digital MSB) could not follow the Autosar requirement to initiate the transfer and set the driver/handler status accordingly.
b) The digital MSB transfers require chip select to be released after each word transferred.  This means the four words would have to be defined as four channels/four jobs.  Each channel requires its own buffer (internal or external). Because the SPI data reads and writes occur in the motor control ISR, they need to be very efficient and cannot afford the overhead of four calls to SpiNxt_SetupEB() that would be needed to implement the double buffering being done on the read data.  Use of a possible SpiNxt_ReadIB() would have this same issue even without the double buffering.

Several of the initialization constants (delay fields in the delay registers and data format registers, and the baudrate prescale field in the data format registers) have values that depend on the VCLK frequency.  These are currently hardcoded for 80 MHz VCLK for Digital MSB, and have values that will work for both 75MHz and 80MHz VCLK for Turns Counter / Turns Counter Reflash (see spreadsheet attached to Turns Counter Reflash FDD).  A future improvement would be to calculate these values based on a VCLK configuration parameter.

## Revision Control Log

| Module Inputs | Module Outputs | Module Outputs |

| --- | --- | --- |

| None | None | None |

| Variable Name | Resolution | Legal Range<br/>(min) | Legal Range<br/>(max) | Software Segment |

| --- | --- | --- | --- | --- |

| ExtBufCfg_Str<br/>[D_SPINXTNUMCHAN_CNT_U16] | See structure definition | See structure definition | See structure definition | SPINXT_START_SEC_VAR_CLEARED_UNSPECIFIED |

| SeqResult_Enum<br/>[D_SPINXTNUMSEQ_CNT_U16] | Enum | SPI_SEQ_OK (= 0) | SPI_SEQ_CANCELLED (=4) | SPINXT_START_SEC_VAR_CLEARED_UNSPECIFIED |

| Typedef Name | Element Name | User Defined Type | Legal Range<br/>(min) | Legal Range<br/>(max) |

| --- | --- | --- | --- | --- |

| EbCfg_Type | SrcDataBufferPtr | Spi_DataType | N/A | N/A |

|  | DesDataBufferPtr | Spi_DataType | N/A | N/A |

|  | Length | Spi_NumberOfDataType | N/A | N/A |

| Constant Name |

| --- |

| <None> |

|  |

| Constant Name | Resolution | Units | Value when D_SPINXTUSEWITH_CNT_ENUM == D_SPINXTUSEWITHTC | Value when D_SPINXTUSEWITH_CNT_ENUM == D_SPINXTUSEWITHDIGMSB |

| --- | --- | --- | --- | --- |

| D_SPINXTUSEWITHTC | Count | Unitless | 0 | 0 |

| D_SPINXTUSEWITHDIGMSB | Count | Unitless | 1 | 1 |

| D_SPINXTUSEWITH_CNT_ENUM | Count | Unitless | 0 | 1 |

| SPI_TCDATA_CH | Count | Unitless | 0 | Not Defined |

| SPI_TCDATA_SEQ | Count | Unitless | 0 | Not Defined |

| SPI_DIE1DATA_CH | Count | Unitless | Not Defined | 0 |

| SPI_DIE2DATA_CH | Count | Unitless | Not Defined | 1 |

| SPI_DIE1DATA_SEQ | Count | Unitless | Not Defined | 0 |

| SPI_DIE2DATA_SEQ | Count | Unitless | Not Defined | 1 |

| D_SPINXTNUMCHAN_CNT_U16 | Count | Unitless | 1 | 2 |

| D_SPINXTNUMSEQ_CNT_U16 | Count | Unitless | 1 | 2 |

| D_TGSIZE_CNT_U16 | Count | Unitless | Not Defined |  |

| MIBSPI3_GCR1 | Count | Unitless | 3 | 3 |

| MIBSPI5_GCR1 | Count | Unitless | 3 | 3 |

| MIBSPI3_DELAY | Count | Unitless | 0xFFFF0000 | 0x04010000 |

| MIBSPI5_DELAY | Count | Unitless | 0 | 0x04010000 |

| MIBSPI3_FMT0 | Count | Unitless | 0xFF00FF08 | 0x04020710 |

| MIBSPI5_FMT0 | Count | Unitless | 0x5E148206 | 0x04020710 |

| MIBSPI5_FMT1 | Count | Unitless | 0x5E148210 | Not Defined |

| MIBSPI5_FMT2 | Count | Unitless | 0x0014820B | Not Defined |

| MIBSPI3_TGCNTRL0 | Count | Unitless | 0x403F0000 |  |

| MIBSPI3_TGCNTRL1 | Count | Unitless | 0x00000A00 |  |

|  |  |  |  |  |

| MIBSPI3_TOTALTGLENGTH | Count | Unitless | 10 |  |

| MIBSPI5_TGCNTRL0 | Count | Unitless | 0x40700000 | 0x010000 |

| MIBSPI5_TGCNTRL1 | Count | Unitless | 0x40700300 |  |

| MIBSPI5_TGCNTRL2 | Count | Unitless | 0x40700600 |  |

| MIBSPI5_TGCNTRL3 | Count | Unitless | 0x40701000 | Not Defined |

| MIBSPI5_TGCNTRL4 | Count | Unitless | 0x40701400 | Not Defined |

| MIBSPI5_TGCNTRL5 | Count | Unitless | 0x40707500 | Not Defined |

| MIBSPI5_TOTALTGLENGTH | Count | Unitless | 117 |  |

| MIBSPI3_BUFRAMCTRLINIT | Count | Unitless | 0x84F7 |  |

| MIBSPI5_BUFRAMCTRLINIT | Count | Unitless | Not Defined |  |

| MIBSPI3_INTCFG | Count | Unitless | Defined |  |

| MIBSPI3_LVL | Count | Unitless | 0 | Not Defined |

| MIBSPI3_INT0 | Count | Unitless | 0 | Not Defined |

| MIBSPI3_TICKCNT | Count | Unitless | 0x80000010 | 0 |

| MIBSPI5_TICKCNT | Count | Unitless | Not Defined | 0 |

| MIBSPI3_TG0_NOTIF | Count | Unitless | Defined | Not Defined |

|  |  |  |  |  |

|  |  |  |  |  |

| Constant Name |

| --- |

|  |

|  |

| Constant Name | Resolution | Value | Software Segment |

| --- | --- | --- | --- |

| None |  |  |  |

| Function Name | SpiNxt_SetupEB | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | Channel | Spi_ChannelType | 0 | 255 |  |

|  | SrcDataBufferPtr | Spi_DataType | NA | NA |  |

|  | DesDataBufferPtr | Spi_DataType | NA | NA |  |

|  | Length | Spi_NumberOfDataType | 0 | 65535 |  |

| Return Value |  | Std_ReturnType | E_OK | E_NOT_OK |  |

| Function Name | SpiNxt_GetSequenceResult | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | Sequence | Spi_SequenceType | 0 | 255 |  |

| Return Value |  | Spi_SeqResultType | SPI_SEQ_OK | SPI_SEQ_CANCELLED |  |

| Function Name | mibspiTransfer | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | mibspi | mibspiBASE_t * | FULL | FULL |  |

|  | group | uint32 | 0 | 7 |  |

| Return Value | N/A |  |  |  |  |

| Function Name | SpiNxt_AsyncTransmit | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | Sequence | Spi_SequenceType | 0 | 255 |  |

| Return Value | result_T_Cnt | Std_ReturnType | E_OK | E_NOT_OK |  |

| Function Name | mibspiSetData | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | mibspi | mibspiBASE_t* | FULL | FULL |  |

|  | group | uint32 | 0 | 7 |  |

|  | data | uint16[] | FULL | FULL |  |

| Return Value | N/A |  |  |  |  |

| Function Name | mibspiSetCtrlData | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | mibspi | mibspiBASE_t* | FULL | FULL |  |

|  | group | uint32 | 0 | 7 |  |

|  | data | Uint32[] | FULL | FULL |  |

| Return Value | N/A |  |  |  |  |

| Function Name | mibspiGetData | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | mibspi | mibspiBASE_t* | FULL | FULL |  |

|  | group | uint32 | 0 | 7 |  |

|  | data | uint16[] | FULL | FULL |  |

| Return Value | [error flags] | uint32 | 0 | 0x5F |  |

| Function Name | mibspiSetData8 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | mibspi | mibspiBASE_t* | FULL | FULL |  |

|  | group | uint32 | 0 | 7 |  |

|  | data | uint8[] | FULL | FULL |  |

| Return Value | N/A |  |  |  |  |

| Function Name | mibspiSetData8 | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | mibspi | mibspiBASE_t* | FULL | FULL |  |

|  | group | uint32 | 0 | 7 |  |

|  | data | uint8[] | FULL | FULL |  |

| Return Value | [error flags] | uint32 | 0 | 0x5F |  |

| Function Name | mibspiEnableGroupNotification | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | mibspi | mibspiBASE_t * | FULL | FULL |  |

|  | group | uint32 | 0 | 7 |  |

|  | level | uint32 | 0 | 1 |  |

| Return Value | N/A |  |  |  |  |

| Function Name | mibspiNotification | Type | Min | Max | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- | --- |

| Arguments Passed | mibspi | mibspiBASE_t* |  |  |  |  |

|  | flags | uint32 |  |  |  |  |

| Return Value | N/A |  |  |  |  |  |

| Function Name | mibspiGroupNotification | Type | Min | Max | UTP Tol. |

| --- | --- | --- | --- | --- | --- |

| Arguments Passed | mibspi | mibspiBASE_t* | FULL | FULL |  |

|  | group | uint32 | 0 | 7 |  |

| Return Value | N/A |  |  |  |  |

| Data | Value |

| --- | --- |

| <None> |  |

| MIBSPI 3 SPI Delay Register (SPIDELAY) | MIBSPI 3 SPI Delay Register (SPIDELAY) | MIBSPI 3 SPI Delay Register (SPIDELAY) |

| --- | --- | --- |

| Position | Desired Value | Description |

| bit 31-24 | 255 | C2TDELAY: Chip-select-active to transmit-start delay<br/>t C2TDELAY= (C2TDELAY + 2) *VCLK Period<br/><br/>Per §8.5.3 of [2] parameter 3 specifies a 9.5 uS clock idle time between bytes.<br/>It is desired to implement the delay in hardware.  In order to accomplish this with the TMS570 SPI peripheral, the Spi to CS CLK start delay is used.<br/>Per [2] the FDD design desires to maximize the clock idle time between bytes using the hardware delays available.<br/>Table 24-26 of [3] indicates the C2TDELAY has a max of 1FFh, however, the field is 8 bits wide so this is considered a typo in the data sheet and the actual max is FFh (255).  With an 80MHz VCLK, using the equation in the table yields a maximum delay of 3.2125 uS. |

| bit 23-16 | 255 | T2CDELAY: Transmit-end-to-chip-select-inactive-delay<br/>t T2CDELAY= (T2CDELAY +1) *VCLK Period<br/><br/><br/>Per §8.5.3 of [2] parameter 4 specifies a minimum 1.5 uS delay.  <br/>Per [2] the FDD design desires to maximize the clock idle time between bytes using the hardware delays available.<br/>Table 24-26 of [3] indicates the T2CDELAY has a max of 1FFh, however, the field is 8 bits wide so this is considered a typo in the data sheet and the actual max is FFh (255).  With an 80MHz VCLK, using the equation in the table yields a maximum delay of 3.2 uS.<br/>The maximum delay of  3.2 uS is achieved by setting this parameter to 255. |

| bit 15-8 | 0 | T2EDELAY: Transmit-data-finished to ENA-pin-inactive time-out<br/><br/>ENA pin functionality is disabled, so this parameter has no effect.  It is set arbitrarily set to 0. |

| bit 7-0 | 0 | C2EDELAY: Chip-select-active to ENA-signal-active time-out<br/><br/>ENA pin functionality is disabled, so this parameter has no effect.  It is set arbitrarily set to 0. |

| MIBSPI 3 SPI Data Format 0 Register (SPIFMT0) | MIBSPI 3 SPI Data Format 0 Register (SPIFMT0) | MIBSPI 3 SPI Data Format 0 Register (SPIFMT0) |

| --- | --- | --- |

| Position | Desired Value | Description |

| bit 31-24 | 255 | WDELAY: Delay in between transmissions for data<br/>WDELAY * PVCLK + 2 * PVCLK<br/><br/>The inter-byte delay is accomplished via a combination of the CS activation and deactivation delays and this parameter.  The other 2 delays are 3.212uS + 3.200uS = 6.412uS. Per [2] the FDD design desires to maximize the clock idle time between bytes using the hardware delays available.<br/>Table 24-28 of [3] indicates the WDELAY has a max of 63, which is an error in the data sheet, 254 is the actual max reported by Eric Best, TI FAE.  With an 80MHz VCLK, using the equation in the table yields a maximum delay of 3.2 uS. |

| bit 23 | 0 | PARPOL: Parity polarity: even or odd<br/><br/>Parity not enabled, so this has parameter has no effect.  Arbitrarily se to 0. |

| bit 22 | 0 | PARITYENA: Parity enable for data<br/><br/>Per §8.5.3 of [2], Data Format specifies Parity to be disabled, so this parameter is set to 0. |

| bit 21 | 0 | WAITENA: <br/><br/>Per §8.5.3 of [2], Data Format specifies WAITENA to be disabled, so this parameter is set to 0. |

| bit 20 | 0 | SHIFTDIR: Shift direction for data<br/><br/>Per §8.5.3 of [2], Data Format specifies MSB shifted out first, so this parameter is set to 0. |

| bit 19 | 0 | Reserved: |

| bit 18 | 0 | DIS CS TIMERS: Disable chip-select timers for this format.<br/><br/>Delays specified by C2TDELAY and T2CDELAY are required for creating the inter byte delay specified in §8.5.3 of [2], so this is set to 0 to enable the delays. |

| bit 17 | 0 | POLARITY: SPI data clock polarity<br/><br/>§8.5.3 of [2], Clock settings specify the polarity to be Inactive-Low, so this is set to 0.  (Note that the Active-High, requirement is not understood and is ignored in the configuration in this module.  When the clock is active it is toggling states to provide edges, thus specifying the active state as a constant level has an unknown meaning) |

| bit 16 | 0 | PHASE: SPI data clock delay<br/><br/>§8.5.3 of [2], Clock settings specify the SCLK edges to be synchronized with the data stream, so this is set to 0. |

| bit 15-8 | 255 | PRESCALE: PRESCALE is use to derive SPICLK from VCLK<br/>BRFormat = VBUSPCLK / (PRESCALEx ÷ 1)<br/><br/>Turns Counter function in [2]§8.5.3 requires a clock source frequency of 300 kHz, however this is not an actual requirement as discussed with the FDD owner, but rather a documentation of the implementation choice at the time of FDD release.  The physical maximum for SPI clock is specified in [1]Table 30-15 by SP71 and SP72 parameters.  With the 8MHz PIC clock the time parameters = 1/(8MHz/4) + 20ns = 250ns + 20ns = 270 ns.  This results in an overall period of 540ns = 1.85 MHz<br/>Table 24-28 of [3] indicates the PRESCALE is 8 bits wide providing a max of 255.  With an 80MHz VCLK, this results in a minimum of baud rate of approx. 314 baud. |

| bit 7-5 | 0 | Reserved: |

| bit 4-0 | 8 | CHARLEN: SPI data data-word length.<br/><br/>Per §8.5.3 of [2], Data Format specifies a value of 8 for this parameter. |

| Function Name | Calling Frequency | System State(s) in which the function is called |

| --- | --- | --- |

| <None> |  |  |

| Function Name | Sub-Module called by (Serial Comm Function Name) |

| --- | --- |

| <None> |  |

| Name of Sub Module | Software Segment |

| --- | --- |

| Spi_SetupEB() | SPINXT_START_SEC_CODE |

| Spi_GetSequenceResult() | SPINXT_START_SEC_CODE |

| Spi_AsyncTransmit() | SPINXT_START_SEC_CODE |

| Spi_Init() | SPINXT_START_SEC_CODE |

| mibspiSetData() | SPINXT_START_SEC_CODE |

| mibspiSetCtrlData() | SPINXT_START_SEC_CODE |

| mibspiGetData() | SPINXT_START_SEC_CODE |

| mibspiTransfer() | SPINXT_START_SEC_CODE |

| Name of Sub Module | Software Segment |

| --- | --- |

| mibspiSetData8() | SPINXT_START_SEC_CODE |

| mibspiGetData8() | SPINXT_START_SEC_CODE |

| mibspiEnableGroupNotification() | SPINXT_START_SEC_CODE |

| mibspiNotification() | SPINXT_START_SEC_CODE |

| mibspiGroupNotification() | SPINXT_START_SEC_CODE |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 | 1 | Initial versiond |  | JJW |

| 2 | 2 | AsyncTransmit design improvement using exclusive areas and message transmit state check to ensure proper management of data transmission.<br/>Added setting DIO CS channels to inactive during init<br/>Added mibspi unit check around Error notification processing | 15-Mar-12 | JJW |

| 3 | 3 | Added Notification function hook for end of sequence notification | 23-Mar-12 | JJW |

| 4 | 4 | Increased WDELAY and T2CDELAY to meet updated FDD 20C requirements | 27-Mar-12 | JJW |

| 5 | 5 | Added metrics hooks to interrupt service routines. | 22-Mar-13 | BWL |

| 6 | 6 | Completed documentation of all functions in the module, along with changes required for the Digital MSB and the fix for anomaly 4713. | 05-Aug-13 | KMC |

|  |  |  |  |  |
