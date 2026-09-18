---
title: 'TechnicalReference GENy InteractionLayer'
description: 'Converted design document: TechnicalReference GENy InteractionLayer'
---

> **Source:** `PSA_BMPV_EPS_TMS570/HLDD/BSW/TechnicalReference_GENy_InteractionLayer.pdf`  
> **Module:** [hldd](../../../../integration/hldd/)  
> **Note:** Text extracted automatically from PDF (136 pages) with pypdf; layout, figures and formatting are not preserved.

---

Vector Interaction Layer 
Technical Reference 
 
Il_Vector 
Version 2.10.01 
 
 
 
 
 
 
 
 
 
 
 
Authors Klaus Emmert, Gunnar Meiss, Heiko Hübler 
Status Released

---

T echnical Reference Vector Interaction Layer   
2012, Vector Informatik GmbH Version: 2.10.01 
based on template version 3.7 
2 / 136 
1 Document Information 
1.1 History 
Author Date Version Remarks 
P . Jost 2000-05-05 1.0 creation 
P . Jost 2000-06-29 1.1 some corrections 
P . Jost 2000-07-13 1.2 changes in Figure 4 and some further corrections 
P . Jost 2000-08-06 1.3 correction of the First-V alue Class 
P . Jost 2000-09-13 1.4 little corrections in the description of the TxT ask and IlInit 
P . Jost 2001-03-01 1.5 message related transmission modes 
example for timeout monitoring 
multi channel support 
known problems 
integration example 
P . Jost 2001-06-22 1.6 some names of attributes changed 
DataChanged flag 
Tx timeout monitoring 
Rx and Tx default values 
new screen shots of the current Gentool 
changes in the state machine 
and further little corrections 
S. Hoffmann 2001-07-05 1.61 some corrections and branch for an OEM 
P . Jost 2001-07-13 1.62 adapted the corrections of version 1.61 for general IL 
P . Jost 2002-04-05 1.63 Signal groups 
Multiple physical and virtual ECU support 
Multiplex Signals 
Rx timeout monitoring: reload of timer and message 
related notification 
Notification in interrupt and task context (IL Polling) 
IL<Tx/Rx>StateT ask 
Attributes for Rx timeout monitoring updated 
Configuration T ool pictures updated 
P . Jost 2002-08-16 1.7 Name of this document changed from User Manual to 
T echnical Reference 
Multiple Indication Flags per Signal 
Macro to Get and Clear at once 
Chapter for Configuration T ool updated 
”New Style” API  
Data Type Prefix for Signal Access 
Further Callbacks for State Machine 
Initialization – IlInitPowerOn 
ECU Timeout 
H. Hörner 2003-06-16 1.8 Several wording and spelling issues corrected 
List of abbreviations and glossary removed, replaced by

---

T echnical Reference Vector Interaction Layer   
2012, Vector Informatik GmbH Version: 2.10.01 
based on template version 3.7 
3 / 136 
an own document 
Implementation details moved to an Annex 
K. Emmert 2003-09-02 1.9 Some design and link modifications. 
H. Hörner 2004-05-14 2.0 Add usage of VStdLib 
Documented return value of flag get macros 
Difference between GenMsgDelayTime and 
GenMsgStartDelayTime clarified 
Some clarifications about signal groups 
Wording enhanced for multiplexed signals 
Klaus Emmert 
Gunnar Meiss 
2005-06-10 2.01 Added support for GENy 
Added new feature dynamic timeout handling 
Added raw API for multiplex signals 
Reworked dbc attributes chapter 
Added matrix with transmission modes 
Gunnar Meiss 
 
2005-08-02 2.02 Adapted GenMsgFastOnStart 
Added GENy Multiplex Support 
Klaus Emmert 
Gunnar Meiss 
2005-11-04 2.03 Added AUTOSAR API for GENy, configuration and signal 
access. 
Added GenMsgFastOnStart for multiplex messages in 
GENy 
Added ESCAN00014120 CANGen 
Added ESCAN00008602 CANGen 
Added ESCAN00008604 CANGen 
Reworked ESCAN00010718 
Gunnar Meiss 2006-02-16 2.04 Added GENy Multiple ECU Reference 
Added ESCAN00013633 
DynRxTimeout API postfix and data types have changed. 
Klaus Emmert 2006-03-13 2.05 Signal Groups for GENy 
Gunnar Meiss 2006-04-06 2.06 Added Indexed API discontinuation for GENy. 
Corrected ApplIlFatalError Prototype 
Improved GenSigTimeoutMsg_<ECU> 
Corrected GenSigSendType description 
Removed GenSigTimeoutMsg_<ECU> for GENy 
Gunnar Meiss 2007-05-16 2.07 Opaque Data Types ESCAN00016935 GENy 
Improved documentation of call contexts of API functions 
ESCAN00017472, ESCAN00018014, ESCAN00014156, 
ESCAN00013962, ESCAN00013423, ESCAN00008047, 
ESCAN00008755 
Gunnar Meiss 2007-12-17 2.08 Added GenSigSuprvResp, GenSigSuprvRespSubV alue 
and GenSigTimeoutMsg_<ECU> for GENy 
Updated API descriptions 
Updated GenMsgStartDelayTime

---

T echnical Reference Vector Interaction Layer   
2012, Vector Informatik GmbH Version: 2.10.01 
based on template version 3.7 
4 / 136 
Updated GenMsgIlSupport 
ESCAN00024092 
Gunnar Meiss 2008-04-21 2.08.01 ESCAN00024091 
Gunnar Meiss 2008-07-17 2.09.00 Reworked Document Structure 
ESCAN00024902 Added Node Mapped dbc Attributes 
Updated Abbreviations and Glossary with CIWI 
ESCAN00028781 Added IlTxRepetitionsAreActive and 
IlTxSignalsAreActive 
ESCAN00028787 Reset Timeout Flags On Release 
Added Geny attribute descriptions 
ESCAN00023799 Added Limitation 
ESCAN00025371 Updated Dynamic Timeout Monitoring 
ESCAN00029109 Added Documentation of Generated 
APIs 
Gunnar Meiss 2008-10-17 2.09.01 ESCAN00030172 The description of IlRxWait() is 
incorrect 
Gunnar Meiss 2011-05-19 2.09.02 ESCAN00049272 
3-6 "Send Type Matrix" 
ESCAN00049615 Incorrect Enumeration V alues of the 
dbc attribute "ILUsed" 
ESCAN00048272 Incorrect Timing Diagram of the 
Transmit Fast if Signal Active Transmission Mode 
Heiko Hübler 2012-03-13 2.10.00 Added Signal status information (UpdateBits) 
Heiko Hübler 2012-05-14 2.10.00 Added description for the GENy GUI attribute “timeout 
time” 
Heiko Hübler 2012-09-13 2.10.01 Added description for PreConfig Switch “Enable  
UpdateBit Support” 
Changed “Send on Init” description  
T able 1-1  History of the Document 
1.2 Reference Documents 
No. Source Title V ersion 
[1]  V ector V ector CAN driver. T echnical Reference  
[2]  V ector V ector Multiple ECUs. T echnical Reference 1.00.00 
[3]  V ector V ector Configuration T ool. Online Documentation. 
(no printed manual available) 
 
[4]  OSEK OSEK/COM, V ersion 3.0.3 3.00.03 
[5]   Z.120 (1996). Message Sequence Chart (MSC). 
ITU-T , Geneva 
April.1996 
[6]  V ector Interaction Layer User Manual

---

T echnical Reference Vector Interaction Layer   
2012, Vector Informatik GmbH Version: 2.10.01 
based on template version 3.7 
5 / 136 
[7]  AUTOSAR AUTOSAR Specification of Module COM 2.0.0 2.00.00 
[8]  AUTOSAR AUTOSAR Specification of Module COM 3.1.0 3.1.0 
T able 1-2  Reference Documents 
 
Please note 
We have configured the programs in accordance with your specifications in the 
questionnaire. Whereas the programs do support other configurations than the one 
specified in your questionnaire, V ector´s release of the programs delivered to your 
company is expressly restricted to the configuration you have specified in the 
questionnaire.

---

T echnical Reference Vector Interaction Layer   
2012, Vector Informatik GmbH Version: 2.10.01 
based on template version 3.7 
6 / 136 
Contents 
1 Document Information ....................................................................................................... 2 
1.1 History.................................................................................................................. 2 
1.2 Reference Documents......................................................................................... 4 
2 Introduction ....................................................................................................................... 11 
2.1 Architecture Overview ....................................................................................... 12 
2.2 Data Access Concept ........................................................................................ 13 
2.3 Adapt the V ector Interaction Layer.................................................................... 15 
3 Functional Description ..................................................................................................... 17 
3.1 Features............................................................................................................. 17 
3.2 Initialization ........................................................................................................ 18 
3.1 Interaction Layer State Machine........................................................................ 19 
3.1.1 States ................................................................................................................. 20 
3.1.1.1 Uninit.................................................................................................................. 20 
3.1.1.2 Running ............................................................................................................. 20 
3.1.1.3 Waiting ............................................................................................................... 20 
3.1.2 State Transitions ................................................................................................ 20 
3.1.2.1 Init ...................................................................................................................... 20 
3.1.2.2 Start.................................................................................................................... 21 
3.1.2.3 Stop .................................................................................................................... 21 
3.1.2.4 Wait .................................................................................................................... 22 
3.1.2.5 Release.............................................................................................................. 22 
3.2 Main Functions .................................................................................................. 23 
3.3 Interaction Layer Communication Concept....................................................... 24 
3.3.1 Interface Concept .............................................................................................. 24 
3.3.2 Notification Mechanisms ................................................................................... 24 
3.4 Data Access ....................................................................................................... 25 
3.4.1 Data Consistency .............................................................................................. 25 
3.4.2 Signal Interface.................................................................................................. 26 
3.4.3 AUTOSAR Signal Interface ............................................................................... 26 
3.4.4 Example: Writing and reading a signal value.................................................... 27 
3.4.5 Signal Groups .................................................................................................... 28 
3.4.5.1 Il API................................................................................................................... 28 
3.4.5.2 AUTOSAR API................................................................................................... 30 
3.4.5.3 GENy configuration ........................................................................................... 30 
3.4.6 Default V alues.................................................................................................... 30 
3.5 Data Transmission ............................................................................................. 31

---

T echnical Reference Vector Interaction Layer   
2012, Vector Informatik GmbH Version: 2.10.01 
based on template version 3.7 
7 / 136 
3.5.1 Transmission Concept ....................................................................................... 31 
3.5.2 Signal Related Transmission Modes................................................................. 36 
3.5.2.1 Cyclic Transmission........................................................................................... 36 
3.5.2.2 OnEvent (OnWrite, OnChange) ........................................................................ 37 
3.5.2.3 OnEvent with Repetition (OnWrite, OnChange) ............................................... 38 
3.5.2.4 Transmit Fast if Signal is Active ........................................................................ 39 
3.5.2.5 Transmit Fast if Signal is Active with Repetition ............................................... 41 
3.5.3 Mixed Transmission Mode................................................................................. 41 
3.5.3.1 Cyclic (Message) Transmission OR Cyclic (Signal) Transmission ................... 41 
3.5.3.2 Cyclic (Message) Transmission OR OnEvent [Write] ....................................... 42 
3.5.3.3 Cyclic (Message) Transmission OR OnEvent [Write] with Repetition .............. 42 
3.5.3.4 Cyclic (Message) Transmission OR OnEvent [Change]................................... 43 
3.5.3.5 Cyclic (Message) Transmission OR OnEvent [Change] with Repetition.......... 43 
3.5.3.6 Cyclic (Message) Transmission OR Transmit Fast If Signal is Active .............. 44 
3.5.3.7 Cyclic (Message) Transmission OR Transmit Fast If Signal is Active with 
Repetition........................................................................................................... 45 
3.5.3.8 Cyclic (Message) Transmission OR NoSigSendType ...................................... 45 
3.5.4 Advanced Transmission Modes ........................................................................ 45 
3.5.5 Notification Classes ........................................................................................... 46 
3.5.6 Reduction of Transmission Bursts..................................................................... 46 
3.5.7 Delimitation of the Bus Load ............................................................................. 47 
3.5.8 Transmission Timeout Monitoring ..................................................................... 47 
3.5.9 Transmission of Initialization Messages ........................................................... 48 
3.6 Data Reception .................................................................................................. 49 
3.6.1 Reception Concept ............................................................................................ 49 
3.6.2 Notification Classes ........................................................................................... 50 
3.6.3 Timeout Monitoring ............................................................................................ 51 
3.6.4 Dynamic Timeout Monitoring............................................................................. 52 
3.7 Signal status information (UpdateBits).............................................................. 54 
3.7.1 Configuration ..................................................................................................... 54 
3.7.1.1 DBC File ............................................................................................................ 54 
3.7.2 UpdateBit Transmission .................................................................................... 54 
3.7.3 UpdateBit Reception ......................................................................................... 55 
3.7.3.1 Timeout .............................................................................................................. 55 
3.8 Multiple Channel Support .................................................................................. 56 
3.8.1 Overview ............................................................................................................ 56 
3.8.2 Idx (Indexed) Interaction Layer ......................................................................... 56 
3.9 Advanced Communication Features ................................................................. 57 
3.9.1 Physical Multiple and Multiple Configuration ECU ........................................... 57 
3.9.2 Multiplexed Signals............................................................................................ 58 
3.9.2.1 Standard API...................................................................................................... 58

---

T echnical Reference Vector Interaction Layer   
2012, Vector Informatik GmbH Version: 2.10.01 
based on template version 3.7 
8 / 136 
3.9.2.2 Raw API ............................................................................................................. 58 
3.9.3 Manipulation of the Notification Frequency....................................................... 61 
4 Integration.......................................................................................................................... 62 
4.1 Include structure ................................................................................................ 62 
4.2 Scope of Delivery .............................................................................................. 62 
4.2.1 Static Files ......................................................................................................... 62 
4.2.2 Dynamic Files .................................................................................................... 63 
4.3 Operating Systems Requirements .................................................................... 64 
5 Configuration..................................................................................................................... 65 
5.1 Configuration in Data Base ............................................................................... 65 
5.1.1 Send Type.......................................................................................................... 67 
5.1.2 Send Type Dependent....................................................................................... 68 
5.1.3 Advanced Attributes .......................................................................................... 70 
5.1.4 Timeout Supervision Attributes.......................................................................... 71 
5.1.5 Former Attributes ............................................................................................... 73 
5.1.6 Example ............................................................................................................. 75 
5.2 Configuration with GENy ................................................................................... 77 
6 API Description ................................................................................................................. 95 
6.1.1 TypeDefinitions .................................................................................................. 95 
6.1.2 Services provided by Interaction Layer............................................................. 96 
6.1.2.1 IlInitPowerOn ..................................................................................................... 96 
6.1.2.2 IlInit .................................................................................................................... 96 
6.1.2.3 IlRxStart ............................................................................................................. 97 
6.1.2.4 IlTxStart.............................................................................................................. 97 
6.1.2.5 IlRxStop ............................................................................................................. 98 
6.1.2.6 IlTxStop .............................................................................................................. 99 
6.1.2.7 IlRxWait.............................................................................................................. 99 
6.1.2.8 IlTxWait ............................................................................................................ 100 
6.1.2.9 IlRxRelease ..................................................................................................... 100 
6.1.2.10 IlTxRelease ...................................................................................................... 101 
6.1.2.11 IlRxT ask ........................................................................................................... 101 
6.1.2.12 IlTxT ask............................................................................................................ 102 
6.1.2.13 IlRxStateT ask ................................................................................................... 102 
6.1.2.14 IlTxStateT ask ................................................................................................... 103 
6.1.2.15 IlSendOnInitMsg .............................................................................................. 103 
6.1.2.16 IlGetStatus ....................................................................................................... 104 
6.1.2.17 IlTxRepetitionsAreActive ................................................................................. 105 
6.1.2.18 IlTxSignalsAreActive ....................................................................................... 105

---

T echnical Reference Vector Interaction Layer   
2012, Vector Informatik GmbH Version: 2.10.01 
based on template version 3.7 
9 / 136 
6.1.3 Generated Services provided by the Interaction Layer .................................. 107 
6.1.3.1 Read and Write Signals and Signal Groups ................................................... 107 
6.1.3.2 Read and Write Signals and SignalGroups in the RDS Buffer. ...................... 115 
6.1.3.3 Notification Flags of Signals, Signal Groups and Grouped Signals ............... 118 
6.1.3.4 Dynamic Rx Timeout ....................................................................................... 121 
6.1.4 Callback Functions .......................................................................................... 124 
6.1.4.1 ApplIlInit ........................................................................................................... 124 
6.1.4.2 ApplIlRxStart .................................................................................................... 124 
6.1.4.3 ApplIlTxStart .................................................................................................... 125 
6.1.4.4 ApplIlRxStop .................................................................................................... 125 
6.1.4.5 ApplIlTxStop..................................................................................................... 126 
6.1.4.6 ApplIlFatalError................................................................................................ 126 
6.1.5 Generated Callback Functions ........................................................................ 127 
7 Limitations ....................................................................................................................... 130 
7.1 CANgen Compatibility ..................................................................................... 130 
7.1.1 Database attributes ......................................................................................... 130 
7.1.2 Application Code ............................................................................................. 130 
7.1.3 Generator......................................................................................................... 130 
8 Glossary and Abbreviations .......................................................................................... 132 
8.1 Glossary........................................................................................................... 132 
8.2 Abbreviations ................................................................................................... 134 
9 Contact ............................................................................................................................. 136

---

T echnical Reference Vector Interaction Layer   
2012, Vector Informatik GmbH Version: 2.10.01 
based on template version 3.7 
10 / 136 
Illustrations 
Figure 2-1 Example for Some ECU’s in a Modern V ehicle............................................ 11 
Figure 2-2 Layer model of the V ector CAN communication components 
CANbedded .................................................................................................. 13 
Figure 2-3 Signal-oriented Access to Data provided by the Interaction Layer .............. 14 
Figure 2-4 Usage of the network database to generate parts of the Interaction Layer 15 
Figure 3-1 Rx and Tx State Machines............................................................................ 19 
Figure 3-2 State Machine of the Interaction Layer......................................................... 19 
Figure 3-3 Call of the Interaction Layer cyclic function.................................................. 23 
Figure 3-4 Synchronization Problem of Data Access .................................................... 25 
Figure 3-5 Timing Diagram of the Periodic Transmission Mode ................................... 36 
Figure 3-6 Timing Diagram of the Transmission Mode OnEvent – OnWrite ................. 37 
Figure 3-7 Timing Diagram of OnEvent with Repetition - OnWrite............................... 38 
Figure 3-8 Timing Diagram of the Transmit Fast if Signal Active Transmission Mode . 39 
Figure 3-9 Example for Combining Signals Related of the Send Fas

*[…only the first 12 of 136 pages extracted…]*
