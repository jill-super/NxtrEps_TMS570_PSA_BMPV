---
title: 'SPNZ210'
description: 'Converted design document: SPNZ210'
---

> **Source:** `Fls/doc/SPNZ210.pdf`  
> **Module:** [Fls](../../../../mcal/fls/)  
> **Note:** Text extracted automatically from PDF (11 pages) with pypdf; layout, figures and formatting are not preserved.

---

Hercules™ F021
Flash API
Errata
Literature Number: SPNZ210
July 2013

---

Contents
1 All Errata Listed With Software Version Numbers ................................................................... 4
2 Revision History ................................................................................................................. 5
3 Known Design Exceptions to Function Specifications ............................................................. 5
2 Table of Contents SPNZ210 – July 2013
Submit Documentation Feedback
Copyright © 2013, Texas Instruments Incorporated

---

www.ti.com
List of Tables
1 Overview ..................................................................................................................... 4
2 Revision History ............................................................................................................. 5
3 Known Design Exceptions to Function Specifications ................................................................. 5
3SPNZ210 – July 2013 List of Tables
Submit Documentation Feedback
Copyright © 2013, Texas Instruments Incorporated

---

Errata
SPNZ210 –July 2013
Hercules™ F021 Flash API
This document describes the known exceptions to the functional specifications for the software.
1 All Errata Listed With Software Version Numbers
Table 1. Overview
Advisory ID v01.50.00 v01.51.00 v02.00.00 v02.00.01
SDOCM00086402 X - - -
SDOCM00086405 X - NA NA
SDOCM00094147 X X - -
SDOCM00102084 NA NA X -
SDOCM00102399 - - X -
LEGEND: X = Advisory applies to this version, NA = Not Applicable to this version of the library, - = Advisory does not affect this
version
4 Hercules™ F021 Flash API SPNZ210 – July 2013
Submit Documentation Feedback
Copyright © 2013, Texas Instruments Incorporated

---

www.ti.com Revision History
2 Revision History
This software errata revision history highlights the technical changes made from the previous to the
current revision.
Table 2. Revision History
Advisory Changes in Advisory List Advisory ID
SDOCM00086402, SDOCM00086405, SDOCM00094147, SDOCM00102084,Added advisory(s) SDOCM00102399
Removed advisory(s) None
Modified advisory(s) None
Other None
3 Known Design Exceptions to Function Specifications
Table 3. Known Design Exceptions to Function Specifications
Title ...................................................................................................................................... Page
SDOCM00086402 — Fapi_doMarginRead() does not read all requested data .................................................. 6
SDOCM00086405 — Fapi_UserDefinedFunctions.c needs FSM unlock/lock sequence for FSM_SECTOR/1/2 writes.... 7
SDOCM00094147 — Incorrect read in Verify functions in ECC regions on LE devices ........................................ 8
SDOCM00102084 — Typo in CGT.CCS.H in GNU attribute check................................................................ 9
SDOCM00102399 — FEDACSDIS and FEDACSDIS2 are missing from Fapi_FmcRegistersType definition.............. 10
5SPNZ210 – July 2013 Hercules™ F021 Flash API
Submit Documentation Feedback
Copyright © 2013, Texas Instruments Incorporated

---

SDOCM00086402 — Fapi_doMarginRead() does not read all requested data www.ti.com
SDOCM00086402 Fapi_doMarginRead() does not read all requested data
Severity S2 - Major
Expected Behavior To read all data for the given range.
Issue The function Fapi_doMarginRead() only returns 3/4 of the data requested on ECC
regions.
Conditions Using this function on ECC region will exhibit this behavior.
Implications Wrong data or invalid reads may occur.
Workaround(s) None
6 Hercules™ F021 Flash API SPNZ210 – July 2013
Submit Documentation Feedback
Copyright © 2013, Texas Instruments Incorporated

---

www.ti.com SDOCM00086405 — Fapi_UserDefinedFunctions.c needs FSM unlock/lock sequence for FSM_SECTOR/1/2
writes
SDOCM00086405 Fapi_UserDefinedFunctions.c needs FSM unlock/lock sequence for
FSM_SECTOR/1/2 writes
Severity S3 - Minor
Expected Behavior Set sectors enabled for programming and erasing.
Issue The example versions of the user defined functions Fapi_setupEepromSectorEnable()
and Fapi_setupBankSectorEnable() does not show unlock the registers
FSM_SECTOR/1/2.
Conditions When trying to do an erase a bank after it has already been erased once after power on
reset.
Implications The bank will not erase.
Workaround(s) As this is intended for the customer to modify, the unlock code can be added by them.
Fapi_GlobalInit.m_poFlashControlRegisters-
>FsmWrEna.FSM_WR_ENA_BITS.WR_ENA = 0x5U; /* Unlock the regtisters */
Fapi_GlobalInit.m_poFlashControlRegisters-
>FsmWrEna.FSM_WR_ENA_BITS.WR_ENA = 0x2U; /* Lock the registers */
7SPNZ210 – July 2013 Hercules™ F021 Flash API
Submit Documentation Feedback
Copyright © 2013, Texas Instruments Incorporated

---

SDOCM00094147 — Incorrect read in Verify functions in ECC regions on LE devices www.ti.com
SDOCM00094147 Incorrect read in Verify functions in ECC regions on LE devices
Severity S2 - Major
Expected Behavior Verification will work on ECC regions on Little Endian devices.
Issue The read functions, Fapi_doVerify(), Fapi_doPsaVerify(), and Fapi_calculatePsa() will fail
on Little Endian devices in the ECC regions do to a byte swap issue.
Conditions When trying to use the functions Fapi_doVerify(), Fapi_doPsaVerify(), and
Fapi_calculatePsa() on ECC regions on Little Endian devices.
Implications This will cause false failures for Fapi_doVerify() and Fapi_doPsaVerify() and cause
incorrect return value for Fapi_calculatePsa() on ECC regions on Little Endian devices.
Workaround(s) For the function Fapi_doVerify(), use the byte variant Fapi_doVerifyByByte().
For the functions Fapi_doPsaVerify() and Fapi_calculatePsa(), none.
8 Hercules™ F021 Flash API SPNZ210 – July 2013
Submit Documentation Feedback
Copyright © 2013, Texas Instruments Incorporated

---

www.ti.com SDOCM00102084 — Typo in CGT.CCS.H in GNU attribute check
SDOCM00102084 Typo in CGT.CCS.H in GNU attribute check
Severity S3 - Minor
Expected Behavior if --gcc option is enabled, ATTRIBUTE_PACKED will be defined.
Issue In this code segment in CGT.CCS.h, __TI_GNU_ATTRIBUTE_SUPPORT__ is missing
the R:
#if defined(__TI_GNU_ATTIBUTE_SUPPORT__)
/* --gcc option enabled so we can specify this */
#define ATTRIBUTE_PACKED __attribute__((packed))
#else
Conditions On CCS compilers, ATTRIBUTE_PACKED will always be an empty definition.
Implications On builds expecting --gcc option to use attributes defined in code, enums will not be
packed if the compile option to pack enums is not explicitly set.
Workaround(s) Add the R to __TI_GNU_ATTIBUTE_SUPPORT__.
9SPNZ210 – July 2013 Hercules™ F021 Flash API
Submit Documentation Feedback
Copyright © 2013, Texas Instruments Incorporated

---

SDOCM00102399 — FEDACSDIS and FEDACSDIS2 are missing from Fapi_FmcRegistersType definition www.ti.com
SDOCM00102399 FEDACSDIS and FEDACSDIS2 are missing from Fapi_FmcRegistersType definition
Severity S3 - Minor
Expected Behavior It is expected theat Fapi_FmcRegistersType contains all registers defined in the devices
TRM and SPNA148/
Issue In the register update for v2.00.00, these registers were unintentionally removed.
Conditions The registers do not exist in the Fapi_FmcRegistersType.
Implications User cannot reference the FEDACSDIS and FEDACSDIS2 registers through the API
reference.
Workaround(s) Directly address the registers.
10 Hercules™ F021 Flash API SPNZ210 – July 2013
Submit Documentation Feedback
Copyright © 2013, Texas Instruments Incorporated

---

IMPORTANT NOTICE
Texas Instruments Incorporated and its subsidiaries (TI) reserve the right to make corrections, enhancements, improvements and other
changes to its semiconductor products and services per JESD46, latest issue, and to discontinue any product or service per JESD48, latest
issue. Buyers should obtain the latest relevant information before placing orders and should verify that such information is current and
complete. All semiconductor products (also referred to herein as “components”) are sold subject to TI’s terms and conditions of sale
supplied at the time of order acknowledgment.
TI warrants performance of its components to the specifications applicable at the time of sale, in accordance with the warranty in TI’s terms
and conditions of sale of semiconductor products. Testing and other quality control techniques are used to the extent TI deems necessary
to support this warranty. Except where mandated by applicable law, testing of all parameters of each component is not necessarily
performed.
TI assumes no liability for applications assistance or the design of Buyers’products. Buyers are responsible for their products and
applications using TI components. To minimize the risks associated with Buyers’products and applications, Buyers should provide
adequate design and operating safeguards.
TI does not warrant or represent that any license, either express or implied, is granted under any patent right, copyright, mask work right, or
other intellectual property right relating to any combination, machine, or process in which TI components or services are used. Information
published by TI regarding third-party products or services does not constitute a license to use such products or services or a warranty or
endorsement thereof. Use of such information may require a license from a third party under the patents or other intellectual property of the
third party, or a license from TI under the patents or other intellectual property of TI.
Reproduction of significant portions of TI information in TI data books or data sheets is permissible only if reproduction is without alteration
and is accompanied by all associated warranties, conditions, limitations, and notices. TI is not responsible or liable for such altered
documentation. Information of third parties may be subject to additional restrictions.
Resale of TI components or services with statements different from or beyond the parameters stated by TI for that component or service
voids all express and any implied warranties for the associated TI component or service and is an unfair and deceptive business practice.
TI is not responsible or liable for any such statements.
Buyer acknowledges and agrees that it is solely responsible for compliance with all legal, regulatory and safety-related requirements
concerning its products, and any use of TI components in its applications, notwithstanding any applications-related information or support
that may be provided by TI. Buyer represents and agrees that it has all the necessary expertise to create and implement safeguards which
anticipate dangerous consequences of failures, monitor failures and their consequences, lessen the likelihood of failures that might cause
harm and take appropriate remedial actions. Buyer will fully indemnify TI and its representatives against any damages arising out of the use
of any TI components in safety-critical applications.
In some cases, TI components may be promoted specifically to facilitate safety-related applications. With such components, TI’s goal is to
help enable customers to design and create their own end-product solutions that meet applicable functional safety standards and
requirements. Nonetheless, such components are subject to these terms.
No TI components are authorized for use in FDA Class III (or similar life-critical medical equipment) unless authorized officers of the parties
have executed a special agreement specifically governing such use.
Only those TI components which TI has specifically designated as military grade or “enhanced plastic”are designed and intended for use in
military/aerospace applications or environments. Buyer acknowledges and agrees that any military or aerospace use of TI components
which have not been so designated is solely at the Buyer's risk, and that Buyer is solely responsible for compliance with all legal and
regulatory requirements in connection with such use.
TI has specifically designated certain components as meeting ISO/TS16949 requirements, mainly for automotive use. In any case of use of
non-designated products, TI will not be responsible for any failure to meet ISO/TS16949.
Products Applications
Audio www.ti.com/audio Automotive and Transportation www.ti.com/automotive
Amplifiers amplifier.ti.com Communications and Telecom www.ti.com/communications
Data Converters dataconverter.ti.com Computers and Peripherals www.ti.com/computers
DLP® Products www.dlp.com Consumer Electronics www.ti.com/consumer-apps
DSP dsp.ti.com Energy and Lighting www.ti.com/energy
Clocks and Timers www.ti.com/clocks Industrial www.ti.com/industrial
Interface interface.ti.com Medical www.ti.com/medical
Logic logic.ti.com Security www.ti.com/security
Power Mgmt power.ti.com Space, Avionics and Defense www.ti.com/space-avionics-defense
Microcontrollers microcontroller.ti.com Video and Imaging www.ti.com/video
RFID www.ti-rfid.com
OMAP Applications Processors www.ti.com/omap TI E2E Community e2e.ti.com
Wireless Connectivity www.ti.com/wirelessconnectivity
Mailing Address: Texas Instruments, Post Office Box 655303, Dallas, Texas 75265
Copyright © 2013, Texas Instruments Incorporated
