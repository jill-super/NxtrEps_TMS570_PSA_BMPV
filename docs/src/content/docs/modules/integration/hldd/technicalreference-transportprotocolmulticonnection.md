---
title: 'TechnicalReference TransportProtocolMultiConnection'
description: 'Converted design document: TechnicalReference TransportProtocolMultiConnection'
---

> **Source:** `PSA_BMPV_EPS_TMS570/HLDD/BSW/TechnicalReference_TransportProtocolMultiConnection.pdf`  
> **Module:** [hldd](../../../../integration/hldd/)  
> **Note:** Text extracted automatically from PDF (177 pages) with pypdf; layout, figures and formatting are not preserved.

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
1 / 177 
 
 
 
 
 
 
 
 
 
 
 
Transport Protocol ISO15765-2 
Technical Reference 
 
Single/Multiple Connection 
Version 3.14.00 
 
 
 
 
 
 
 
 
 
 
Authors Oliver Garnatz, Andreas Pick, Peter Herrmann, 
Thomas Dedler 
Status Released

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
2 / 177 
Document Information 
History 
Author Date Version Remarks 
Rein 1999-06-22 1.0 File created 
Baeuerle 1999-11-02 1.42 Description of connection 
specific timing parameters 
added 
Ebner 2000-07-17 1.51 Single connection version 
removed; documents only 
contains multiple connection 
extensions 
Garnatz 2000-09-19 2.03 Adaptation to new 
MultiConnection TP 
Garnatz 2001-02-09 2.07 Added new functionality  
Garnatz 2001-05-11 2.10 Update new Generation Tool 
versions 
Garnatz 2001-09-14 2.17 General improvement;  
Update to version 2.17 of 
tpmc.c module  
Garnatz 2002-01.24 2.27 SingleConnection version is 
added; Protocol-Overview is 
added 
Garnatz 2002-06-18 2.33 Added restrictions for data 
consistency 
Pick / Garnatz 2002-10-16 2.36 Update: CAN Driver in polling 
mode 
Added: Fast transmission of 
ConsecutiveFrames 
Update: Usage of TransmitCF 
parameter 
Garnatz 2002-11-29 2.37 General rework  
Garnatz 2003-01-16 2.39 Update: 
TpTransmit/CopyToCan/Appl
TpCheckTA 
Garnatz 2004-01-13 2.44 Update: ApplTpCopyToCAN 
Pick 2004-03-01 2.52 Update: Mixed 29-bit ID 
addressing 
TpRxGetCanBuffer 
TpRxSetBufferOverrun 
TpRxGetAddressExtension 
TpTxSetAddressExtension 
Pick 2004-05-14 2.60 Multiple ECUs example 
Restriction on 
TpTxStateTask/TpRxStateTas
k 
Tx/Rx message buffer

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
3 / 177 
consistency clarification 
Return value of 
ApplTpPreCopyCheck 
Mixed 11-bit ID addressing 
TpTransmit() return values 
Added TpCanChannelInit() 
Added TpRxSetTransmitID() 
Changed 
TpRxSetBufferOverrun 
Changed 
ApplTpTxCopyToCAN 
Changes in chapter ‘How to 
serve Different  
               Connections (only 
dynamic channels)’. 
Pick 2004-12-01 2.68 Added description for GENy 
configuration tool 
(ESCAN00008734).  
Update of API description 
(ESCAN00008314). 
Feature list added 
(ESCAN00008315). 
Prototype parameter 
corrected (ESCAN00009965) 
 
Pick 2005-04-07 2.72.00 Added description for multiple 
addressing systems. 
C++ access to TPMC. 
Pick 2005-07-14 2.73.00 Added description for GENy 
configuration 
Herrmann 2005-07-19 2.73.00 Added new API functions: 
TpRxSetWaitCorrectSN, 
TpTxSetStrictFlowControlChe
ck 
Herrmann 2005-08-11 2.73.00 Added new API functions: 
TpRxSetTimeoutConfirmation
,  
TpTxSetTimeoutConfirmation, 
TpRxSetTimeoutCF, 
TpTxSetTimeoutCF   
Garnatz 2006-01-13 2.80.00 Added deviation to ISO 
15765-2  
Herrmann 2006-02-08 2.82.00 ISO 15765-2 deviations 
elaborated 
Herrmann 2006-03-03 2.86.00 Cleanup (ESCAN15514) 
Herrmann 2006-03-23 2.86.00 ISO 15765-2 deviations 
elaborated 
Herrmann 2006-04-11 2.87.00 General rework after review 
Herrmann 2006-07-03 2.89.00 Added WaitFrame handling.

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
4 / 177 
Herrmann 2007-02-01 2.90.00 Added OEM feature 
TP_ENABLE_STRICT_DL_C
HECK  
Herrmann 2007-02-23 2.91.00 Added feature 
TP_DISABLE_MF_RECEPTI
ON 
Herrmann 2007-03-14 2.92.00 Added ApplFuncTpPrecopy 
callback description and 
reduced TpRxResetChannel 
API usage to indication point 
in time or after. 
Herrmann 2007-09-20 2.93.00 Completed Multiple ECU 
description (see chapter 
7.3.1). Added TpRxGet-
AddressingFormat / 
AssignedDestination 
description. 
                                                    VERSION 3.xx  
Herrmann 2007-10-15 3.00.00 Added description for new 
TpClass  
“Dispatched<AddressingType>”  
Herrmann 2007-11-20 3.01.00 Cosmetics / Syntax 
Herrmann 2008-01-14 3.02.00 New API: 
TpTxGetTargetAddress 
Herrmann 2008-02-12 3.03.00 Minor corrections within API 
descriptions 
(ApplTpTxErrorIndication, 
TpRxGetCanBuffer) 
Herrmann 2008-04-17, 
 
2008-07-17 
3.04.00 Added description for 
TP_ENBLE_DYN_CHANNEL_TIM
ING. 
Added description for the usage 
of extended identifiers for 
normal addressing as well at 
configuration time as also 
dynamically at runtime 
(TP_USE_EXT_IDS_FOR_NO
RMAL). 
Herrmann 2008-12-10 3.05.00 Added description for 
GenMsgDelay attribute in 
chapter 3.4.1 
Herrmann 2009-01-25 3.07.00 Adapted version number to 
ALM package number (3.06.00 
skipped) 
Herrmann 2009-11-25 3.08.00 Added description for reception 
and transmission without flow 
control frames for dyn. 
(TpRxWithoutFC, 
TpTxWithoutFC) and static

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
5 / 177 
(TpTxFlowControl, 
TpRxFlowControl 
) Tp classes. 
Herrmann 2010-01-12 3.09.00 Enhanced description for DLC 
checks on the Rx side (see 
2.4.2.5). 
Added API functions for 29-Bit 
ext. Id dynamic handling. 
Heil 2010-11-08 3.10.00 Added more flexibility for DLC 
checks on the Rx side (see 
2.4.2.5) 
Herrmann 2011-01-19 3.11.00 Moved 
TP_MEMORY_MODEL_DATA   
from user config file to GENy  
Herrmann 2011-04-05 3.12 ESCAN00051019: Added new 
(customer specific) pre-compile 
switches:  
TP_ENABLE_IGNORE_FC_RE
S_STMIN,  
TP_ENABLE_IGNORE_FC_OV
FL (see 3.2.3). 
Herrmann 
 
Dedler 
2011-07-11 
 
2011-09-21 
3.13 ESCAN00051019: Added 
support for the dynamic setting 
of  29-bit CAN-IDs (see 
4.2.2.31, 4.2.2.32, 4.2.3.29, 
4.2.3.30). 
Added new pre-compile switch:  
TP_USE_UNEXPECTED_FC_
CANCELATION (see 3.2.3). 
Dedler 2012-04-10 3.13.01 Description of 
TpRxGetCanBuffer modified 
according to ESCAN00057225 
Dedler 2013-04-30 3.14.00 Description for non-standard 
flow control handling updated 
(3.2.3) 
 
Reference Documents 
No. Title 
[1]  /ISO/TF2/:  ISO FDIS 15765-2; Road vehicles — Diagnostics on CAN — Part 2: Network 
layer services; 
Date 2004-07-16 
[2]  /OSEK-COM/:  OSEK/VDX Communication Version 2.1, revision 1 17th June 1998 
[3]  /CANDrv/:  Manual for CAN Driver in used version 
[4]  ISO15765-2:  ISO TC 22/SC 3;  ISO 15765-2:2003(E); Road vehicles — Diagnostics on 
controller area network (CAN) — Part 2: Part 2: Network layer services

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
6 / 177 
  
 
Caution 
We have configured the programs in accordance with your specifications in the 
questionnaire. Whereas the programs do support other configurations than the one 
specified in your questionnaire, Vector´s release of the programs delivered to your 
company is expressly restricted to the configuration you have specified in the 
questionnaire.

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
7 / 177 
Contents 
1 Introduction ................................ ................................ ................................ .................. 15 
1.1 Relation between general component and shipped version capability .................... 15 
1.2 Name Conventions ................................ ................................ ................................ . 16 
1.3 Abbreviations ................................ ................................ ................................ ......... 17 
1.4 Channel vs. Connection ................................ ................................ ......................... 17 
1.5 TP classes................................ ................................ ................................ .............. 18 
1.5.1 SingleTP classes ................................ ................................ ........................... 18 
1.5.2 Static MultiTP classes ................................ ................................ ................... 18 
1.5.3 Dynamic MultiTP classes ................................ ................................ .............. 18 
1.5.4 Dispatched MultiTP classes ................................ ................................ .......... 18 
1.6 SingleConnection vs. MultipleConnection ................................ ...............................  19 
1.7 Features ................................ ................................ ................................ ................. 19 
1.7.1 Feature List ................................ ................................ ................................ ... 19 
2 Architecture Overview ................................ ................................ ................................ . 23 
2.1 Requirements ................................ ................................ ................................ ......... 23 
2.1.1 Protocol-Overview ................................ ................................ ......................... 23 
2.1.1.1 Construction of unsegmented messages ................................ ................ 23 
2.1.1.2 Construction of segmented messages ................................ .................... 23 
2.1.2 Addressing modes ................................ ................................ ........................ 24 
2.1.2.1 Normal Addressing ................................ ................................ ................. 25 
2.1.2.2 Mixed 11-bit ID Addressing ................................ ................................ ..... 25 
2.1.2.3 Normal Fixed Addressing ................................ ................................ ....... 25 
2.1.2.4 Extended Addressing................................ ................................ .............. 25 
2.1.2.5 Mixed 29-bit ID Addressing ................................ ................................ ..... 26 
2.1.2.6 Structure of TPCI-Byte ................................ ................................ ........... 26 
2.2 Transmission ................................ ................................ ................................ .......... 28 
2.3 Reception ................................ ................................ ................................ ............... 29 
2.4 Working behaviors ................................ ................................ ................................ .. 30 
2.4.1 Timings ................................ ................................ ................................ ......... 30 
2.4.2 Error detection................................ ................................ ...............................  31 
2.4.2.1 Reception of a SingleFrame ................................ ................................ ... 31 
2.4.2.2 Reception of a FirstFrame ................................ ................................ ...... 31 
2.4.2.3 Reception of a FlowControl ................................ ................................ .... 31 
2.4.2.4 Reception of a ConsecutiveFrame................................ .......................... 32 
2.4.2.5 Observing CAN frame DLC (Data Length Code) ................................ .... 32 
2.4.3 Buffer consistency ................................ ................................ ......................... 33 
2.4.4 Function re-entrancy ................................ ................................ ..................... 33 
2.5 Restriction ................................ ................................ ................................ .............. 34

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
8 / 177 
2.5.1 Restrictions to ISO/TF2 specification ................................ ............................. 34 
2.5.2 Limitations of Transport Protocol Implementation ................................ .......... 34 
2.5.3 Deviations to ISO/TF2 specification ................................ ...............................  37 
2.5.3.1 Handling of unexpected FlowControl / ConsecutiveFrame frames .......... 37 
3 Settings for the MultiTP & SingleTP (multi-based) ................................ .................... 38 
3.1 General settings with CANgen / DBKOMgen / GENy ................................ ............. 38 
3.1.1 Timing ................................ ................................ ................................ ........... 39 
3.1.1.1 Transmission timing ................................ ................................ ................ 39 
3.1.1.2 Reception timing ................................ ................................ ..................... 39 
3.1.1.3 Common timing ................................ ................................ ...................... 40 
3.1.2 Flow Control ................................ ................................ ................................ .. 40 
3.1.2.1 Transmission ................................ ................................ .......................... 40 
3.1.2.2 Reception ................................ ................................ ...............................  40 
3.1.3 Misc ................................ ................................ ................................ .............. 41 
3.2 General settings with Generation Tool GENy ................................ .......................... 43 
3.2.1 Configuration of Addressing Information ................................ ........................ 44 
3.2.2 Usage of Far RAM buffers ................................ ................................ ............. 44 
3.2.3 Non standard handling of Flow Control frames ................................ .............. 44 
3.2.3.1 Reserved STmin Handling ................................ ................................ ...... 44 
3.2.3.2 Ignore Flow Control Overflow ................................ ................................ . 45 
3.2.3.3 Do not ignore unexpected Flow Control frames ................................ ...... 45 
3.2.3.4 Use STmin of FC ................................ ................................ .................... 45 
3.2.3.5 Analyze first FC only ................................ ................................ .............. 45 
3.3 Additional settings via user-configuration file ................................ .......................... 45 
3.3.1 Dynamic Timing API ................................ ................................ ...................... 45 
3.4 TP classes: SingleTP (multi-based) ................................ ................................ ........ 46 
3.4.1 Database Attributes ................................ ................................ ....................... 46 
3.4.2 TP class SingleTP (multi-based): Normal Addressing ................................ .... 47 
3.4.3 TP class SingleTP (multi-based): Extended Addressing ................................  47 
3.4.4 TP class SingleTP (multi-based):Normal Fixed Addressing ........................... 47 
3.4.4.1 Database Attributes ................................ ................................ ................ 47 
3.5 TP classes Static MultiTP ................................ ................................ ....................... 47 
3.5.1 Database Attributes ................................ ................................ ....................... 47 
3.5.2 TP class specific settings ................................ ................................ .............. 48 
3.5.3 Connection specific timing parameters ................................ .......................... 48 
3.5.4 Functions ................................ ................................ ................................ ...... 49 
3.6 TP classes Dynamic MultiTP ................................ ................................ .................. 49 
3.6.1 Properties ................................ ................................ ................................ ...... 49 
3.6.2 Hook Functions ................................ ................................ ............................. 50 
3.6.3 Dynamic Objects ................................ ................................ ........................... 50

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
9 / 177 
3.6.4 TP class Dynamic MultiTP: Normal Addressing ................................ ............. 51 
3.6.4.1 CANdriver settings ................................ ................................ ................. 51 
3.6.5 TP class Dynamic MultiTP: Extended Addressing ................................ ......... 51 
3.6.5.1 TP class specific settings................................ ................................ ........ 51 
3.6.5.2 Database Attributes ................................ ................................ ................ 52 
3.6.5.3 Multiple Base Addresses ................................ ................................ ........ 52 
3.6.6 TP class Dynamic MultiTP: Normal Fixed Addressing ................................ ... 52 
3.6.6.1 Database Attributes ................................ ................................ ................ 52 
3.6.7 TP class Dynamic MultiTP: Mixed 29-bit Addressing ................................ ..... 53 
3.6.8 TP class Dynamic MultiTP: Multiple Addressing ................................ ............ 53 
3.6.8.1 Addressing mode ................................ ................................ ................... 53 
3.6.8.2 CAN Driver settings ................................ ................................ ................ 53 
3.7 TP class Dispatched MultiTP ................................ ................................ .................. 55 
3.7.1 “Dynamic MultiTP” versus “Dispatched MultiTP” – a short analogy ............... 56 
3.7.1.1 Solution based on “Dynamic MultiTP”: ................................ .................... 56 
3.7.1.2 Solution based on “Dispatched MultiTP” ................................ ................. 57 
3.7.2 Dispatched MultiTP API ................................ ................................ ................. 60 
3.7.2.1 Reception side................................ ................................ ........................ 60 
3.7.2.2 Transmission side ................................ ................................ ................... 61 
4 API ................................ ................................ ................................ ................................ . 63 
4.1 Use of ISO15765-Transport Protocol ................................ ................................ ...... 63 
4.2 Functions of the Transport Protocol ................................ ................................ ........ 63 
4.2.1 Administrative Functions ................................ ................................ ............... 64 
4.2.1.1 TpInitPowerOn: Initialization ................................ ................................ ... 64 
4.2.1.2 TpInit: Re-initialization ................................ ................................ ............ 65 
4.2.1.3 TpTask:  Observing timing conditions ................................ ..................... 65 
4.2.1.4 TpCanChannelInit: CAN channel specifiic re-initialization ....................... 66 
4.2.1.5 TpRxTask: time base for reception timeouts ................................ ........... 67 
4.2.1.6 TpTxTask: time base for timeouts/transmission ................................ ...... 68 
4.2.1.7 TpRxStateTask: optional transmission retry ................................ ............ 69 
4.2.1.8 TpRxAllStateTask: optional transmission retry ................................ ........ 69 
4.2.1.9 TpTxStateTask: optional transmission retry ................................ ............ 70 
4.2.1.10 TpTxAllStateTask: optional transmission retry ................................ ........ 71 
4.2.2 Receive Functions ................................ ................................ ......................... 72 
4.2.2.1 TpRxSetConnectionNumber: Assign a Connection-Number to a 
channel ................................ ................................ ................................ .. 72 
4.2.2.2 TpRxGetConnectionNumber: Get the Corresponding Connection-
Number ................................ ................................ ................................ .. 72 
4.2.2.3 TpRxGetAddressingFormat:  Get the current addressing type ................ 73 
4.2.2.4 TpRxGetAssignedDestination:  Get the currently assigned destination .. 74

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
10 / 177 
4.2.2.5 TpRxResetChannel: Free Rx-TpChannel ................................ ............... 75 
4.2.2.6 TpRxGetStatus: Rx-Channel Status ................................ ....................... 76 
4.2.2.7 TpRxSetBS: Setting up BlockSize on Reception Side ............................ 77 
4.2.2.8 TpRxGetBS: Get BlockSize on Reception Side ................................ ...... 78 
4.2.2.9 TpRxSetSTMIN: Setting up STMin time on Reception Side .................... 78 
4.2.2.10 TpRxGetSTMIN: Get STMin time on Reception Side.............................. 79 
4.2.2.11 TpRxGetChannelID: Get Received CAN-Id ................................ ............ 80 
4.2.2.12 TpRxGetChannelExtID: Get Received Extended CAN-Id ....................... 81 
4.2.2.13 TpRxGetCanChannel: Get physical CAN channel ................................ .. 81 
4.2.2.14 TpRxGetSourceAddress: Get received Source Address ......................... 82 
4.2.2.15 TpRxGetReceivedTargetAddress: Get received Target Address ............. 83 
4.2.2.16 TpRxGetEcuNumber: Get ECU Number................................ ................. 84 
4.2.2.17 TpRxGetParameterGroupIdentification: Get Identification of PGN .......... 84 
4.2.2.18 TpRxSetBufferOverrun:   Enable partial acceptance...............................  85 
4.2.2.19 TpRxSetTransmitID:   Set transmission CAN-Id................................ ...... 86 
4.2.2.20 TpRxSetTransmitExtID:   Set transmission Extended CAN-Id................. 87 
4.2.2.21 TpRxGetChannelIDType:   Get the type of the received CAN-Id ............. 88 
4.2.2.22 TpRxGetAddressExtension:  Get address extension information ............ 88 
4.2.2.23 TpRxGetCanBuffer:  Get CAN buffer pointer ................................ .......... 89 
4.2.2.24 TpRxSetWaitCorrectSN:  Force to wait for a correct sequence 
number ................................ ................................ ................................ ... 90 
4.2.2.25 TpRxSetTimeoutConfirmation:  Set CAN confirmation timeout ............... 91 
4.2.2.26 TpRxSetTimeoutCF:  Set Consecutive Frame confirmation timeout ....... 92 
4.2.2.27 TpRxSetFCStatus:  set up Flow Control on reception side ..................... 92 
4.2.2.28 TpRxGetFCStatus:  get the Flow Control setup on reception side .......... 93 
4.2.2.29 TpRxSetClearToSend:  proceed with the transmission after FC wait 
frames ................................ ................................ ................................ .... 94 
4.2.2.30 TpRxWithoutFC:  suppress FC frame usage at the Rx side .................... 95 
4.2.2.31 TpRxSetPGN: Set Parameter Group Number ................................ ........ 96 
4.2.2.32 TpRxSetPriorityBits: Set Priority, Data Page and Reserved bits ............. 97 
4.2.3 Transmit Functions ................................ ................................ ........................ 98 
4.2.3.1 TpTxGetFreeChannel: Assign Channel to Connection ........................... 98 
4.2.3.2 TpTxGetConnectionNumber: Get the assigned Connection-Number ...... 99 
4.2.3.3 TpTxGetConnectionStatus: Get the Connection Status .......................... 99 
4.2.3.4 TpTxGetTargetAddress:  Get the target address used for transmission 100 
4.2.3.5 TpTxGetDataBuffer: Get the assigned Data Buffer ...............................  101 
4.2.3.6 TpTxGetDataIndex: Get the assigned Data Index ................................  102 
4.2.3.7 TpTxSetChannelID: Set the CAN Transmit Id ................................ ....... 102 
4.2.3.8 TpTxSetChannelExtID: Set the CAN Transmit  Extended Id ................. 103 
4.2.3.9 TpTxSetCanChannel: Set physical CAN Channel ................................  104 
4.2.3.10 TpTxSetTargetAddress: Set Target Address ................................ ......... 105

---

Technical Reference Transport Protocol ISO15765-2 
2013, Vector Informatik GmbH Version: 3.14.00 
based on template version 5.1.0 
11 / 177 
4.2.3.11 TpTxSetEcuNumber: Set ECU Number ................................ ................ 106 
4.2.3.12 TpTxSetBaseAddress: Set Base Address................................ ............. 106 
4.2.3.13 TpTxSetParameterGroupIdentificati

*[…only the first 12 of 177 pages extracted…]*
