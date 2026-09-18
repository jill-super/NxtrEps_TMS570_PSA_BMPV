---
title: 'SPNU501F'
description: 'Converted design document: SPNU501F'
---

> **Source:** `Fls/doc/SPNU501F.pdf`  
> **Module:** [Fls](../../../../mcal/fls/)  
> **Note:** Text extracted automatically from PDF (51 pages) with pypdf; layout, figures and formatting are not preserved.

---

F021 Flash API
Version 2.01.00
Reference Guide
Literature Number: SPNU501F
December 2012 – Revised May 2014

---

Contents
1 Introduction......................................................................................................................... 4
1.1 Reference Material....................................................................................................... 4
1.2 Function Listing Format ................................................................................................. 4
2 F021 Flash API Overview ...................................................................................................... 6
2.1 Introduction................................................................................................................ 6
2.2 API Overview ............................................................................................................. 6
2.3 Using API.................................................................................................................. 7
3 API Functions .................................................................................................................... 10
3.1 Flash State Machine Functions ....................................................................................... 10
3.2 Asynchronous Functions .............................................................................................. 16
3.3 Program Functions ..................................................................................................... 18
3.4 Read Functions ......................................................................................................... 20
3.5 Informational Functions ................................................................................................ 29
3.6 Utility Functions ......................................................................................................... 32
3.7 User Definable Functions.............................................................................................. 33
4 API Macros ........................................................................................................................ 34
4.1 FAPI_CHECK_FSM_READY_BUSY ................................................................................ 34
4.2 FAPI_CLEAR_FSM_DONE_EVENT................................................................................. 34
4.3 FAPI_GET_FSM_STATUS............................................................................................ 35
4.4 FAPI_SUSPEND_FSM ................................................................................................ 36
4.5 FAPI_WRITE_EWAIT .................................................................................................. 37
4.6 FAPI_WRITE_LOCKED_FSM_REGISTER ......................................................................... 37
5 Recommended FSM Flows .................................................................................................. 37
5.1 New Devices From Factory ........................................................................................... 37
5.2 Recommended Erase Flows .......................................................................................... 38
5.3 Recommended Program Flow ........................................................................................ 40
Appendix A Flash State Machine Commands................................................................................. 41
A.1 Flash State Machine Commands.................................................................................... 41
Appendix B Typedefs and Enumerations....................................................................................... 42
B.1 Type Definitions ....................................................................................................... 42
B.2 Enumerations .......................................................................................................... 42
Appendix C Flash Validation Procedure ........................................................................................ 47
Appendix D Parallel Signature Analysis (PSA) algorithm................................................................. 48
Appendix E Revision History ....................................................................................................... 49
2 Table of Contents SPNU501F – December 2012 – Revised May 2014
Submit Documentation Feedback
Copyright © 2012–2014, Texas Instruments Incorporated

---

www.ti.com
List of Figures
1 FMSTAT Register .......................................................................................................... 35
2 Recommended Sector Erase Flow....................................................................................... 38
3 Recommended Bank Erase Flow ........................................................................................ 39
4 Recommended Program Flow............................................................................................ 40
List of Tables
1 Summary of Flash State Machine Functions............................................................................. 6
2 Summary of Asynchronous Command Functions ....................................................................... 6
3 Summary of Program Functions ........................................................................................... 6
4 Summary of Read Functions ............................................................................................... 7
5 Summary of Information Functions........................................................................................ 7
6 Summary of User Defined Functions...................................................................................... 7
7 Summary of Utility Functions............................................................................................... 7
8 FMSTAT Register Field Descriptions.................................................................................... 35
9 Flash State Machine Commands ........................................................................................ 41
10 API Version History ........................................................................................................ 49
11 Document Revision History ............................................................................................... 50
3SPNU501F – December 2012 – Revised May 2014 List of Figures
Submit Documentation Feedback
Copyright © 2012–2014, Texas Instruments Incorporated

---

Reference Guide
SPNU501F – December 2012 – Revised May 2014
1 Introduction
Background
This reference guide provides a detailed description of Texas Instruments' F021 Flash API functions that
can be used to erase, program and verify F021 Flash on TI devices.
1.1 Reference Material
Use this guide in conjunction with the F021 Flash Module chapter in the device-specific technical
reference manual and data sheet that is being used. For additional options for programming and erasing
the Flash, see the Advanced F021 Flash API Erase/Program Usage (SPNA148).
1.2 Function Listing Format
This is the general format of an entry for a function, compiler intrinsic, or macro.
A short description of what function function_name() does.
Synopsis
Provides a prototype for function function_name().
<return_type> function_name(
<type_1> parameter_1,
<type_2> parameter_2,
<type_n> parameter_n
)
Parameters
parameter_1 [in] Pointer to x
parameter_2 [out] Handle for y
parameter_n [in/out] Pointer to z
Parameter passing is categorized as follows:
• In — Means the function uses one or more values in the parameter that you give it without storing any
changes.
• Out — Means the function saves one or more of the values in the parameter that you give it. You can
examine the saved values to find out useful information about your application.
• In/out — Means the function changes one or more of the values in the parameter that you give it and
saves the result. You can examine the saved values to find out useful information about your
application.
Description
Describes the function function_name(). This section also describes any special characteristics or
restrictions that might apply:
• Function blocks or might block under certain conditions
• Function has pre-conditions that might not be obvious
• Function has restrictions or special behavior
All trademarks are the property of their respective owners.
4 SPNU501F – December 2012 – Revised May 2014
Submit Documentation Feedback
Copyright © 2012–2014, Texas Instruments Incorporated

---

www.ti.com Introduction
Return Value
Specifies any value or values returned by function function_name().
See Also
Lists other functions or data types related to function function_name().
Example
Provides an example (or a reference to an example) that illustrates the use of function function_name().
5SPNU501F – December 2012 – Revised May 2014
Submit Documentation Feedback
Copyright © 2012–2014, Texas Instruments Incorporated

---

F021 Flash API Overview www.ti.com
2 F021 Flash API Overview
2.1 Introduction
The F021 Flash API is a library of routines that when called with the proper parameters in the proper
sequence, erases, programs, or verifies Flash memory on Texas Instruments microcontrollers using the
F021 (65nm) process. On ARM Cortex devices, these routines must be run in a privileged mode (a mode
other than user) to allow access to the Flash memory controller registers. The API verifies for the selected
bank, that the appropriate RWAIT or EWAIT value is set for the specified system frequency.
2.2 API Overview
Table 1. Summary of Flash State Machine Functions
API Function Description
Fapi_disableAutoEccCalculation() (1) Disables auto generation of ECC when data is written into an FWPWRITEx
register.
Fapi_disableBanksForOtpWrite() Disables all banks from programming customer OTP
Fapi_disableFsmDoneEvent() Disables the generation of an FSM_Done event at the end of a program or erase
operation.
Fapi_enableAutoEccCalculation() (1) Enables auto generation of ECC when data is written into an FWPWRITEx register.
Fapi_enableBanksForOtpWrite() Enables banks to allow programming of customer OTP
Fapi_enableEepromBankSectors() Enables the sectors in EEPROM bank for program and erase operations
Fapi_enableFsmDoneEvent() Enables the generation of an FSM_Done event at the end of a program or erase
operation.
Fapi_enableMainBankSectors() Enables the sectors in Main banks for program and erase operations
Fapi_initializeFlashBanks() Required Bank initialization before any erase, program, or verify API function.
Fapi_isAddressEcc() Determines if address falls in Flash memory controller ECC ranges
Fapi_remapEccAddress() Remaps an ECC address to corresponding main address
Fapi_remapMainAddress() Remaps an Main address to corresponding ECC address
Fapi_setActiveFlashBank() Sets the active bank for a erase or program command
(1) This function is only available on devices with the L2FMC Flash Controller.
Table 2. Summary of Asynchronous Command Functions
API Function Description
Fapi_issueAsyncCommand() Issues a command to FSM for operations that do not require an address
Fapi_issueAsyncCommandWithAddress() Issues a command to FSM for operations that require an address
Table 3. Summary of Program Functions
API Function Description
Sets up the required registers for programming and issues the command to theFapi_issueProgrammingCommand() FSM
Fapi_issueProgrammingCommandForEccAdd Remaps an ECC address to the main data space and then call
ress() Fapi_issueProgrammingCommand()
6 SPNU501F – December 2012 – Revised May 2014
Submit Documentation Feedback
Copyright © 2012–2014, Texas Instruments Incorporated

---

www.ti.com F021 Flash API Overview
Table 4. Summary of Read Functions
API Function Description
Fapi_doVerify() Verifies specified Flash memory range against supplied values
Fapi_doVerifyByByte() Verifies specified Flash memory range against supplied values by byte
Fapi_doBlankCheck() (1) Verifies specified Flash memory range against erased state
Fapi_doBlankCheckByByte() (1) Verifies specified Flash memory range against erased state by byte
Fapi_doMarginRead() Reads a specified Flash memory range using the specified read-margin mode
Fapi_doMarginReadByByte() Reads a specified Flash memory range using the specified read-margin mode by
byte
Fapi_doPsaVerify() Verifies a specified Flash memory range against the supplied PSA value
Fapi_calculatePsa() Calculates a PSA value for the specified Flash memory range
Fapi_flushPipeline() Flushes the pipeline buffers in the Flash memory controller
(1) On devices using L2FMC memory controller, ECC may not be disabled for Banks 0 - 6 and therefore performing a blank check
with the Flash API functions are not supported.
Table 5. Summary of Information Functions
API Function Description
Fapi_getLibraryInfo() Returns the information specific to the compiled version of the API library
Fapi_getDeviceInfo() Returns the information specific to the device the API library is being executed on
Fapi_getBankSectors() Returns the sector information for a bank
Table 6. Summary of User Defined Functions
API Function Description
Fapi_serviceWatchdogTimer() User modifiable function to service watchdog timer
Table 7. Summary of Utility Functions
API Function Description
Fapi_calculateFletcherChecksum() Function calculates a Fletcher checksum for the memory range specified
Fapi_calculateEcc() Calculates the ECC for the supplied address and 64-bit word
Fapi_waitDelay() (1) Creates a delay
(1) This function is deprecated and should not be used in new projects
2.3 Using API
This section describes how to use the various API functions and any relevant flows.
2.3.1 Initialization Flow
For proper initialization of the device prior to any Flash operations, see the device-specific initialization
document. Additionally, all API functions require execution in privilege mode.
2.3.1.1 Before Using Any Erase, Program or Read Flash API Function
Before using any asynchronous command Table 2 , program Table 3 or read Table 4 functions, the
function Fapi_initializeFlashBanks() must be called to correctly initialize the Flash Memory controller.
7SPNU501F – December 2012 – Revised May 2014
Submit Documentation Feedback
Copyright © 2012–2014, Texas Instruments Incorporated

---

F021 Flash API Overview www.ti.com
2.3.1.2 Bank Setup
Before performing a Flash erase or program operation for the first time or on a different Bank than is the
current active Bank, the function Fapi_setActiveFlashBank() must be called. Additionally,
Fapi_enableMainBankSectors() (for banks 0-6) or Fapi_enableEepromBankSectors() (for bank 7) must be
called before the first sector erase or program operation and always before a bank erase operation.
2.3.1.3 On System Frequency Change
If the System operating frequency (HCLK) is changed after the initial call to Fapi_initializeFlashBanks(),
this function along with Fapi_setActiveFlashBank() must be called again before any asynchronous
command Table 2 , program Table 3 or read Table 4 function. This will update the Flash Memory
controller to the new system frequency.
2.3.2 Flash Addressing
For program and erase operations on Bank 0 to Bank 6, the API and the FMC requires the standard Flash
memory map where Bank 0, Sector 0 begins at address 0. For the read functions on the Flash memory in
Bank 0 to Bank 6, they need either current address mapping (Flash addresses starting at either 0 {Power
On State} or 0x0800_0000 {RAM-Flash swap) or mirrored addresses starting at 0x2000_0000.
2.3.3 Building With the API
The macro _L2FMC must be defined before the inclusion of the header file F021.h on devices with the
L2FMC Flash controller.
#define _L2FMC
2.3.3.1 Object Library Files
All ARM Cortex Flash API object files are distributed in the ARM standard EABI ELF object format. For the
CortexR4/R5 cores, the library files are built using Thumb2 mode.
2.3.3.2 Distribution Files
The following API files are distributed with the installer:
• Library Files - (All library files were built using TI's code generation tools for ARM v5.1.3 with the
following compile options: -mv7R4 --abi=eabi --strict_ansi -g -O3 --symdebug:dwarf_version=3 --
diag_warning=225 --gen_func_subsections=on --enum_type=packed --code_state=16 )
– F021_API_CortexR4_BE.lib – This is the Flash API object file for Cortex R4 Big Endian devices.
– F021_API_CortexR4_BE_v3D16.lib – This is the Flash API object file for Cortex R4 Big Endian
devices that are using floating point unit. (In addition to the general build options, this library was
built using : --float_support=VFPv3D16)
– F021_API_CortexR4_BE_L2FMC.lib – This is the Flash API object file for Cortex R4 Big Endian
devices using the L2FMC memory controller.
– F021_API_CortexR4_LE.lib – This is the Flash API object file for Cortex R4 Little Endian devices.
(In addition to the general build options, this library was built using : -me)
– F021_API_CortexR4_LE_v3D16.lib – This is the Flash API object file for Cortex R4 Little Endian
devices that are using floating point unit. (In addition to the general build options, this library was
built using : -me --float_support=VFPv3D16)
– F021_API_CortexR4_LE_L2FMC.lib – This is the Flash API object file for Cortex R4 Little Endian
devices using the L2FMC memory controller.
– F021_API_CortexR4_BE_L2FMC_v3D16.lib – This is the Flash API object file for Cortex R4/R5 Big
Endian devices using the L2FMC memory controller and float point unit. (In addition to the general
build options, this library was built using : --float_support=VFPv3D16)
– F021_API_CortexR4_LE_L2FMCv3D16.lib – This is the Flash API object file for Cortex R4/R5 Little
Endian devices using the L2FMC memory controller and float point unit. (In addition to the general
build options, this library was built using : -me --float_support=VFPv3D16)
8 SPNU501F – December 2012 – Revised May 2014
Submit Documentation Feedback
Copyright © 2012–2014, Texas Instruments Incorporated

---

www.ti.com F021 Flash API Overview
• Source Files
– Fapi_UserDefinedFunctions.c – This is file that contains the user definable functions.
• Include Files
– F021.h – This is the master include file and includes all other include files. This should be the only
include file added to the users's code.
• The following include files should not be included directly by the user’s code, but are listed here for
user reference:
– Compatibility.h - A set of macros to be used for backwards compatibility for 1.x.x versions of the
API.
– Constants.h – Constant definitions used by the API.
– FapiFunctions.h - Contains all the Fapi function prototypes.
– Helpers.h – Set of helper defines
– Registers.h – Definitions common to all register implementations and includes the appropriate
register include file for the selected device type.
– Registers_FMC_BE.h – Big Endian Flash memory controller registers structure for TMS570/RM4
devices.
– Registers_FMC_LE.h – Little Endian Flash memory controller registers structure for TMS570/RM4
devices.
– Types.h – Contains all the enumerations and structures used by the API
– Below are a set of compiler specific support header files:
• CGT.ARM.h - Contains a set of definitions used by the ARM compiler
• CGT.CCS.h - Contains a set of definitions used by the TI CCS compiler
• CGT.gcc.h - Contains a set of definitions used by the gcc compiler
• CGT.GHS.h - Contains a set of definitions used by the GreenHills compiler
• CGT.IAR.h - Contains a set of definitions used by the IAR EWARM compiler
• Library information files
– build_information.txt - This file contains function callgraphs, worst case stack usage for each
function, function size in bytes and MD5 and SHA1 checksums for all files delivered in the installer
package.
– License_Agreement.pdf - This file contains the libraries license agreement.
– readme.txt - This file contains build specific information.
– Release_Notes.pdf - This file contains release specific information.
– spna148.pdf - This is the application note, Advanced F021 Flash API Erase/Program Usage.
– spnu501e.pdf - This file.
– spnz210.pdf - This is the library errata document.
2.3.4 Executing API From Flash
NOTE: The F021 Flash API library cannot be executed from the same bank as the active bank
selected for the API commands to operate on. On single bank devices, the F021 Flash API
must be executed from RAM.
2.3.5 Memory Regions Required to be Readable
NOTE: The F021 Flash API library must be able to read from addresses 0x000, 0x100, 0x200,
0x300, and the TI OTP region, 0xF008_0000 - 0xF00B_0000, for the API to operate
correctly.
9SPNU501F – December 2012 – Revised May 2014
Submit Documentation Feedback
Copyright © 2012–2014, Texas Instruments Incorporated

---

API Functions www.ti.com
3 API Functions
3.1 Flash State Machine Functions
3.1.1 Fapi_disableAutoEccCalculation()
Disables auto generation of ECC on L2FMC devices
Synopsis
Fapi_StatusType Fapi_disableAutoEccCalculation(void)
Parameters
None
Description
NOTE: This function is only available on devices using the L2FMC Flash Memory Controller.
This function disables the auto generation of ECC when data is written to the FWPWRITEx registers on
L2FMC devices. The use of this function is primarily intended for those users writing their own
programming functions based on the application note, Advanced F021 Flash API Erase/Program Usage
(SPNA148). The function Fapi_issueProgrammingCommand() Section 3.2.2 will automatically set this bit
depending on the programming mode used (enabled for Fapi_AutoEccGeneration, disabled for all other
modes) and will stay that way when this function returns.
Return Value
• Fapi_Status_Success (success)
3.1.2 Fapi_disableBanksForOtpWrite()
Disables ability to program the Customer OTP on all Flash Banks.
Synopsis
Fapi_StatusType Fapi_disableBanksForOtpWrite(void)
Parameters
None
Description
This function sets OTPPRODIS field in the FBAC register to disable the ability to program the Customer
OTP for all banks.
Return Value
• Fapi_Status_Success (success)
10 SPNU501F – December 2012 – Revised May 2014
Submit Documentation Feedback
Copyright © 2012–2014, Texas Instruments Incorporated

---

www.ti.com API Functions
3.1.3 Fapi_disableFsmDoneEvent()
Disables generation of the FSM_DONE event.
Synopsis
Fapi_StatusType Fapi_disableFsmDoneEvent(void)
Parameters
None
Description
This function disables the generation of the FSM_DONE event. For more information on the FSM_DONE
event, see the device-specific technical reference manual.
Return Value
• Fapi_Status_Success (success)
3.1.4 Fapi_enableAutoEccCalculation()
Enables auto generation of ECC on L2FMC devices
Synopsis
Fapi_StatusType Fapi_enableAutoEccCalculation(void)
Parameters
None
Description
NOTE: This function is only available on devices using the L2FMC Flash Memory Controller.
This function enables the auto generation of ECC when data is written to the FWPWRITEx registers on
L2FMC devices. The use of this function is primarily intended for those users writing their own
programming functions based on Advanced F021 Flash API Erase/Program Usage (SPNA148). The
function Fapi_issueProgrammingCommand() Section 3.2.2 will automatically set this bit depending on the
programming mode used (enabled for Fapi_AutoEccGeneration, disabled for all other modes) and will stay
that way when this function returns.
Return Value
• Fapi_Status_Success (success)
11SPNU501F – December 2012 – Revised May 2014
Submit Documentation Feedback
Copyright © 2012–2014, Texas Instruments Incorporated

---

API Functions www.ti.com
3.1.5 Fapi_enableBanksForOtpWrite()
Enables ability to program the Customer OTP region for the specified banks
Synopsis
Fapi_StatusType Fapi_enableBanksForOtpWrite(
uint8_t u8Banks)
Parameters
u8Banks [in] Bit mask indicating each bank to be enabled for OTP programming
Description
This function sets up the OTPPRODIS field in the FBAC register to enable the ability to program Customer
OTP for the banks specified in the bitfield mask u8Banks. The bitfield mask has Bank 0 as bit 1 up to
Bank 7 as bit 7.
Return Value
• Fapi_Status_Success (success)
3.1.6 Fapi_enableEepromBankSectors()
Sets up the sectors available on EEPROM banks for erase and programming
Synopsis
Fapi_StatusType Fapi_enableEepromBankSectors(
uint32_t u32SectorsEnables_31_0,
uint32_t u32SectorsEnables_63_32)
Parameters
u32SectorsEnables_31_0 [in] Bit mask indicating which of sectors 0-31 are enabled for erase and
programming.
u32SectorsEnables_63_32 [in] Bit mask indicating which of sectors 32-63 are enabled for erase and
programming.
Description
This function sets up the sectors in the EEPROM banks that are available for erase and programming
operations. This function must be called with the EEPROM bank (Flash Bank 7) as the active bank.
Additionally, the function must be called once before performing program and sector erase

*[…only the first 12 of 51 pages extracted…]*
