---
title: 'TechnicalReference CANdesc'
description: 'Converted design document: TechnicalReference CANdesc'
---

> **Source:** `PSA_BMPV_EPS_TMS570/HLDD/BSW/TechnicalReference_CANdesc.pdf`  
> **Module:** [hldd](../../../../integration/hldd/)  
> **Note:** Text extracted automatically from PDF (117 pages) with pypdf; layout, figures and formatting are not preserved.

---

CANdesc 
Technical Reference 
 
 
 
 
Version 2.19.00 
 
 
 
 
 
 
 
 
 
 
Authors: Oliver Garnatz, Mishel Shishmanyan, Stefan 
Hübner, Matthias Heil 
Version: 2.19.00 
Status: released (in preparation/completed/inspected/released)

---

Technical Reference CANdesc  
1 History 
Author Date Version Remarks 
Oliver Garnatz 2003-11-12 2.00.00 Splitting into separate documents 
and general revision 
Oliver Garnatz 2004-01-13 2.00.01 Added chapter ‘Application interface 
flow’ 
Updated format template 
Mishel Shishmanyan 2004-03-09 2.01.00 New application callback convention 
(from CANdesc 2.09.00) 
Mishel Shishmanyan 2004-03-29 2.02.00 New APIs: 
- DescGetActivityState (from 
CANdesc 2.10.00) 
- DescSchedulerTask() (from 
CANdesc 2.09.00) 
Mishel Shishmanyan 2004-04-26 2.03.00 Added more information and 
limitations about the ring-buffer 
mechanism (6.6.8 “Ring Buffer 
Mechanism”) 
New feature: 
- Support for generic user 
service (from CANdesc 
2.11.00) 
- Force CANdesc to send 
RCR-RP response (from 
CANdesc 2.11.00) 
Stefan Hübner 2004-07-16 2.03.01 Editorial revision 
Oliver Garnatz 2004-08-12 2.04.00 Added chapter 4.2 
ReadDataByIdentifier (SID $22) 
within the Single- and the Multiple 
PID mode is described 
Oliver Garnatz 2004-10-08 2.05.00 ESCAN0000982: Description of 
MainHandler structure is not 
readable 
ROE transmission unit is described 
in detail  
Stefan Hübner 
Oliver Garnatz 
2004-10-15 2.06.00 Some additional information are 
provided  
Peter Herrmann 
Klaus Emmert 
2005-06-22 2.07.00 Added: Service $2C description. 
Added: Warning Text added 
Mishel Shishmanyan 
Oliver Garnatz 
2005-08.03 2.08.00 API added:  
- DescStateTask, 
- DescTimerTask,  
©2010, Vector Informatik GmbH Version: 2.19.00 
 
2 / 117

---

Technical Reference CANdesc  
- DescMayCallStateTaskAgai
n. 
- ApplDescFatalError 
API modified:  
- DescTask,  
- ApplDescCheckSessionTran
sition,  
- DescGetActivityState,  
- DescGetStateSession. 
API removed:  
- DescSchedulerTask 
Modified description for 
ReadDataByIdentifier with long data 
and negative response in main-
handler. 
Oliver Garnatz 2006-03-02 2.09.00 Added: ...prevent the ECU going to 
sleep while diagnostic is active 
Mishel Shishmanyan 2006-03-24 2.10.00 Added: document overview 
Mishel Shishmanyan 2006-04-27 2.11.00 Modified:  
-6.6.12 
DynamicallyDefineDataIdentifier  
($2C) (UDS) functions 
-6.6.12.1 
DescMayCallStateTaskAgain() 
 
Mishel Shishmanyan 2007-02-22 2.12.00 Added:  
 - 6.6.8.3 “DescRingBufferCancel()” 
 
Matthias Heil 2008-01-03 2.13.00 Added: 
Caution concerning user main 
handler on protocol level 
Matthias Heil 2008-02-29 2.14.00 Added: 
Handling of read/write memory by 
address: 
 - 5.5 “Read/Write Memory by 
Address” 
- 6.6.7.2 
“DescStartMemByAddrRepeatedCal
l()” 
- 6.6.13 ”Memory Access Callbacks”
Mishel Shishmanyan 2008-06-06 2.15.00 Removed: 
Chapter “ResponseOnEvent 
Transmission Unit” 
Added: 
©2010, Vector Informatik GmbH Version: 2.19.00 
 
3 / 117

---

Technical Reference CANdesc  
 - 6.6.12.3 “Non-volatile memory 
support” 
Mishel Shishmanyan 2008-11-09 2.16.00 Modified: 
- 6.6.8 and 6.6.8.1: Added limitation 
for UDS and SPRMIB with the ring 
buffer usage. 
- 7.6 …work with the ring-buffer 
mechanism 
Added: 
- 6.6.14 Flash Boot Loader Support 
- 7.8 …send a positive response 
without request after FBL flash job  
Mishel Shishmanyan 2009-05-18 2.17.00 Modified: 
6.6.5.1ApplDescCheckSessionTran
sition() 
Added: 
6.6.5.3DescIsSuppressPosResBitS
et () 
Mishel Shishmanyan 2009-08-11 2.18.00 Modified: 
Minor editorial changes 
5.2 Configure Handlers using 
CANdela attributes – added new 
data object attributes 
Added: 
7.9 …enforce CANdesc to use 
ANSI C instead of hardware 
optimized bit type 
5.1 Configure DBC attributes for 
diagnostics 
 
Mishel Shishmanyan 2010-12-21 2.19.00 Modified: 
6.6.8.2 DescRingBufferWrite() 
6.6.13.1 
ApplDescReadMemoryByAddress() 
6.6.13.2 
ApplDescWriteMemoryByAddress() 
 
 
©2010, Vector Informatik GmbH Version: 2.19.00 
 
4 / 117

---

Technical Reference CANdesc  
Contents 
1 History............................................................................................................ 2 
2 Introduction ................................................................................................. 10 
3 Documents this one refers to…................................................................. 11  
4 Architecture Overview ................................................................................ 12 
4.1 CANdesc – Internal processing..................................................... 12 
4.1.1 Diagnostic protocol........................................................................ 12 
4.1.2 How does this flow actually work? ................................................ 13 
4.2 Application interface flow .............................................................. 16 
4.2.1 Session- and CommunicationControl............................................ 16 
5 Advanced Configuration ............................................................................ 17 
5.1 Configure DBC attributes for diagnostics ...................................... 17 
5.2 Configure Handlers using CANdela attributes .............................. 17 
5.3 ReadDataByIdentifier (SID $22).................................................... 23 
5.3.1 Limitations of the service............................................................... 24 
5.3.2 Single PID mode ........................................................................... 25 
5.3.2.1 Sending a positive response using linear buffer access ............... 25 
5.3.2.2 Sending a positive response using ring buffer access .................. 26 
5.3.2.3 Sending a negative response........................................................ 27 
5.3.3 Multiple PID mode......................................................................... 27 
5.3.3.1 Pure linear buffer configuration ..................................................... 28 
5.3.3.1.1 Sending a positive response ......................................................... 28 
5.3.3.1.2 Sending a negative response........................................................ 29 
5.3.3.2 Ring buffer active configuration..................................................... 29 
5.3.3.2.1 Sending a positive response ......................................................... 32 
5.3.3.2.2 Sending a negative response........................................................ 33 
5.3.3.2.3 PostHandler execution rule ........................................................... 34 
5.4 DynamicallyDefineDataIdentifier (SID $2C) (UDS) ....................... 35 
5.4.1 Feature set.................................................................................... 35 
5.4.2 API Functions................................................................................ 35 
5.4.3 Sequence Charts .......................................................................... 36 
5.5 Read/Write Memory by Address (SID $23/$3D) (UDS) ................ 39 
5.5.1 Tasks performed by CANdesc ...................................................... 39 
5.5.2 Task to be performed by the Application....................................... 39 
5.5.3 Repeated service calls .................................................................. 39 
©2010, Vector Informatik GmbH Version: 2.19.00 
 
5 / 117

---

Technical Reference CANdesc  
6 CANdesc API ............................................................................................... 41 
6.1 API Categories .............................................................................. 41 
6.1.1 Single Context............................................................................... 41 
6.1.2 Multiple Context (only CANdesc) .................................................. 41 
6.2 Data Types.................................................................................... 41 
6.3 Global Variables............................................................................ 41 
6.4 Constants ...................................................................................... 41 
6.4.1 Component Version ...................................................................... 41 
6.5 Macros .......................................................................................... 42 
6.5.1 Data exchange .............................................................................. 42 
6.5.1.1 Splitting 16 bit data........................................................................ 42 
6.5.1.2 Splitting 32 bit data........................................................................ 42 
6.5.1.3 Assembling 16 bit data.................................................................. 43 
6.5.1.4 Assembling 32 bit data.................................................................. 43 
6.6 Functions....................................................................................... 44 
6.6.1 Administrative Functions ............................................................... 44 
6.6.1.1 DescInitPowerOn()........................................................................ 44 
6.6.1.2 DescInit()....................................................................................... 45 
6.6.1.3 DescTask().................................................................................... 46 
6.6.1.4 DescStateTask() ........................................................................... 47 
6.6.1.5 DescTimerTask()........................................................................... 48 
6.6.1.6 DescGetActivityState() .................................................................. 49 
6.6.2 Service Functions.......................................................................... 50 
6.6.2.1 DescSetNegResponse() ............................................................... 50 
6.6.2.2 DescProcessingDone() ................................................................. 51 
6.6.3 Service Call-Back functions .......................................................... 52 
6.6.3.1 Service PreHandler ....................................................................... 52 
6.6.3.2 Service MainHandler..................................................................... 53 
6.6.3.3 Service PostHandler ..................................................................... 55 
6.6.4 User (Unknown) Service Handling ................................................ 56 
6.6.4.1 How it works.................................................................................. 56 
6.6.4.2 ApplDescCheckUserService()....................................................... 57 
6.6.4.3 DescGetServiceId()....................................................................... 58 
6.6.4.4 Generic User Service MainHandler............................................... 59 
6.6.4.5 Generic User Service PostHandler ............................................... 60 
6.6.5 Session Handling .......................................................................... 61 
6.6.5.1 ApplDescCheckSessionTransition().............................................. 61 
6.6.5.2 DescSessionTransitionChecked()................................................. 62 
6.6.5.3 DescIsSuppressPosResBitSet () .................................................. 63 
6.6.5.4 ApplDescOnTransitionSession() ................................................... 64 
6.6.5.5 DescSetStateSession() ................................................................. 65 
©2010, Vector Informatik GmbH Version: 2.19.00 
 
6 / 117

---

Technical Reference CANdesc  
6.6.5.6 DescGetStateSession()................................................................. 66 
6.6.6 CommunicationControl Handling .................................................. 67 
6.6.6.1 ApplDescCheckCommCtrl() .......................................................... 67 
6.6.6.2 DescCommCtrlChecked() ............................................................. 68 
6.6.7 Periodic call of ‘Service MainHandler’........................................... 69 
6.6.7.1 DescStartRepeatedServiceCall() .................................................. 69 
6.6.7.2 DescStartMemByAddrRepeatedCall() .......................................... 70 
6.6.8 Ring Buffer Mechanism................................................................. 71 
6.6.8.1 DescRingBufferStart() ................................................................... 72 
6.6.8.2 DescRingBufferWrite() .................................................................. 73 
6.6.8.3 DescRingBufferCancel() ............................................................... 74 
6.6.8.4 DescRingBufferGetFreeSpace() ................................................... 75 
6.6.8.5 DescRingBufferGetProgress() ...................................................... 76 
6.6.9 Signal Interface of CANdesc ......................................................... 77 
6.6.9.1 ApplDesc<Signal-Handler>() ........................................................ 77 
6.6.9.2 Configuration of direct signal access ............................................ 78 
6.6.10 State Handling (CANdesc only) .................................................... 78 
6.6.10.1 DescGetState<StateGroup>()....................................................... 78 
6.6.10.2 DescSetState<StateGroup>() ....................................................... 79 
6.6.10.3 ApplDescOnTransition«StateGroup»() ......................................... 80 
6.6.11 Force “Response Correctly Received - Response Pending” transmission 81  
6.6.11.1 DescForceRcrRpResponse() ........................................................ 82 
6.6.11.2 ApplDescRcrRpConfirmation()...................................................... 83 
6.6.12 DynamicallyDefineDataIdentifier  ($2C) (UDS) functions.............. 84 
6.6.12.1 DescMayCallStateTaskAgain() ..................................................... 85 
6.6.12.2 ApplDescCheckDynDidMemoryArea().......................................... 86 
6.6.12.3 Non-volatile memory support ........................................................ 87 
6.6.12.3.1 DescDynDefineDidPowerUp()....................................................... 90 
6.6.12.3.2 DescDynIdMemContentRestored () .............................................. 91 
6.6.12.3.3 DescDynDefineDidPowerDown () ................................................. 92 
6.6.12.3.4 ApplDescStoreDynIdMemContent ()............................................. 93 
6.6.12.3.5 ApplDescRestoreDynIdMemContent ()......................................... 94 
6.6.13 Memory Access Callbacks ............................................................ 95 
6.6.13.1 ApplDescReadMemoryByAddress() ............................................. 95 
6.6.13.2 ApplDescWriteMemoryByAddress().............................................. 96 
6.6.14 Flash Boot Loader Support ........................................................... 96 
6.6.14.1 DescSendPosRespFBL() .............................................................. 97 
6.6.14.2 ApplDescInitPosResFblBusInfo().................................................. 98 
6.6.15 Debug Interface / Assertion........................................................... 99 
6.6.15.1 ApplDescFatalError() .................................................................... 99 
©2010, Vector Informatik GmbH Version: 2.19.00 
 
7 / 117

---

Technical Reference CANdesc  
7 How To….................................................................................................... 104  
7.1 …implement a protocol service MainHandler ............................. 104  
7.2 …implement a service MainHandler ........................................... 107  
7.3 …implement a Signal Handler .................................................... 108  
7.4 …implement a Packet Handler ................................................... 109  
7.5 …implement a state transition function ....................................... 109  
7.6 …work with the ring-buffer mechanism....................................... 110  
7.6.1 with asynchronous write.............................................................. 110 
7.6.2 with synchronous write................................................................ 112 
7.7 …prevent the ECU going to sleep while diagnostic is active ...... 113  
7.8 …send a positive response without request after FBL flash job . 114  
7.9 …enforce CANdesc to use ANSI C instead of hardware optimized bit type 114  
8 Related documents ................................................................................... 115 
9 Glossary..................................................................................................... 116 
10 Contact....................................................................................................... 117 
 
©2010, Vector Informatik GmbH Version: 2.19.00 
 
8 / 117

---

Technical Reference CANdesc  
Illustrations 
Figure 3-1: Manuals and References for CANdesc ........................................................................ 11 
Figure 4-1: General request flow .................................................................................................... 12 
Figure 4-2: DESC run diagram ....................................................................................................... 13 
Figure 4-3: Request message mapping.......................................................................................... 14  
Figure 4-4: Request processing stages .......................................................................................... 15 
Figure 5-1: Dependency of CANdesc Handler configuration .......................................................... 22 
Figure 5-2: Linearly written positive response on single PID request ............................................. 25 
Figure 5-3: “On the fly” response data writing.................................................................................26 
Figure 5-4: Negative response on single PID ................................................................................. 27 
Figure 5-5: Linearly written positive response on multiple PIDs (global ring buffer option is off).... 28 
Figure 5-6: Negative response on multiple PIDs (global ring buffer option is off)........................... 29  
Figure 5-7: Linearly written response data on multiple PIDs (global ring buffer option is on)......... 32  
Figure 5-8: Negative response on multiple PIDs (global ring buffer option is on)........................... 33  
Figure 5-9: Post-Handler execution sequence................................................................................ 34 
Figure 5-10: Defining a DDID.......................................................................................................... 37 
Figure 5-11: Reading a DDID. ........................................................................................................ 38 
Figure 6-1 DynDID definition restore and tester interaction............................................................ 88  
Figure 6-2 Store DynDID definitions ............................................................................................... 89 
 
©2010, Vector Informatik GmbH Version: 2.19.00 
 
9 / 117

---

Technical Reference CANdesc  
2 Introduction 
This document has not the job to describe the diagnostic itself. The focus of this document 
is the technical aspects of the CANdesc component. 
 
 
Please note 
We have configured the programs in accordance with your specifications in the 
questionnaire. Whereas the programs do support other configurations than the one 
specified in your questionnaire, Vector’s release of the programs delivered to your 
company is expressly restricted to the configuration you have specified in the 
questionnaire. 
 
©2010, Vector Informatik GmbH Version: 2.19.00 
 
10 / 117

---

Technical Reference CANdesc  
3 Documents this one refers to… 
 User Manuals CANdesc and CANdescBasic (one for both) 
 Docu OEM 
 
You are here
User Manual
Technical
Reference
General
Technical
Reference
OEM
 
Figure 3-1: Manuals and References for CANdesc 
All common topics with CANdes c and CANdescBasic are descr ibed within this technical 
reference very detailed.  
Read all about OEM-specific differences in the TechnicalReference_OEM. 
For faster integration, refer to the product’s corresponding user manual CANdesc or 
CANdescBasic. 
 
©2010, Vector Informatik GmbH Version: 2.19.00 
 
11 / 117

---

Technical Reference CANdesc  
©2010, Vector Informatik GmbH Version: 2.19.00 
 
12 / 117
4 Architecture Overview 
This chapter should describe the internal  structure and behavior of the CANdesc 
component.  
 
4.1 CANdesc – Internal processing 
4.1.1 Diagnostic protocol 
The communication described in the diagnos tic protocol consists of a ping-pong 
communication between a tester (client) and an ECU (server). The tester requests a 
service in the ECU by transmitting a reques t to him. The ECU should response with a 
positive response, if the result of this service is valid or the action is prepared to be done. 
Is the result negative or t he action could not be executed, the ECU should respond 
negative.  
The validity checks have typically the same pattern for all services (as shown in Figure 
4-1: General request flow). These components which are included in this flow, build up the 
main base of the CANdesc component. 
 
t
Diagnostics - CANdesc
Application
Check Svc
Check Session
Check SvcInst
Check Format
Mainhandler
{
....
DescProcessingDone( );
}
Prehandler optional
{
}
Posthandler optional
{
}
Request
negative Response
Tester
positive Response
ACK
 
Figure 4-1: General request flow

*[…only the first 12 of 117 pages extracted…]*
