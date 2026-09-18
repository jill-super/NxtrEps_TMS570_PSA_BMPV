---
title: 'TechnicalReference Stationmanager'
description: 'Converted design document: TechnicalReference Stationmanager'
---

> **Source:** `PSA_BMPV_EPS_TMS570/HLDD/BSW/TechnicalReference_Stationmanager.pdf`  
> **Module:** [hldd](../../../../integration/hldd/)  
> **Note:** Text extracted automatically from PDF (35 pages) with pypdf; layout, figures and formatting are not preserved.

---

Nm_StMgrIndOsek_Ls 
Technical Reference 
Station Manager (Low Speed) 
 
 
 
 
 
 
 
Version 3.05 
Date 2011-07-29 
File TechnicalReference_Stationmanager.doc 
Number of Pages 35

---

Station manager for PSA Technical Reference 1 
1 History ............................................................................................................ 5  
1.1 SM Version................................................................................................ 5  
2 Introduction.................................................................................................... 5  
2.1 Reference Documents............................................................................... 5  
2.2 Abbreviations ............................................................................................ 5  
2.3 Tasks and Aims......................................................................................... 6  
3 Network management states ........................................................................ 6  
3.1 Organ Type 1 ............................................................................................ 6  
3.1.1 Description of internal States for organ type 1:................................... 6 
3.2 Organ Type 2 ............................................................................................ 7  
3.2.1 Description of internal States for organ type 2 :.................................. 7 
3.3 Organ Type 3 ............................................................................................ 7  
3.3.1 Description of internal States for organ type 3 :.................................. 7 
3.4 Organ Type 4 ............................................................................................ 8  
3.4.1 Description of internal States for organ type 4 :.................................. 8 
4 Integration into the application .................................................................... 8  
4.1 Delivery Items ........................................................................................... 8  
4.2 Version Changes....................................................................................... 9  
4.3 Handling of the station-manager ............................................................... 9 
4.4 Particularities if there is no Interaction Layer in the system....................... 9 
4.4.1 Event transmission of the supervised Tx message............................. 9 
4.5 Start delay time of Tx messages ............................................................... 9 
4.5.1 Start delay time without Interaction Layer........................................... 9 
4.6 Reading of Nerr state .............................................................................. 10  
4.7 Handling of the signal Interd_Memo_Def ................................................ 10 
4.8 Handling of Lmin ..................................................................................... 10  
4.8.1 First value and Indication flags ......................................................... 11 
4.8.2 Timeout flags and functions.............................................................. 11 
4.8.3 Impact on the application.................................................................. 11  
4.8.4 Access to the actual DLC ................................................................. 12 
4.9 Cancel of pending transmit messages .................................................... 12 
©2011, Vector Informatik GmbH TechnicalR eference_Stationmanager.doc Version 3.05

---

Station manager for PSA Technical Reference 2 
4.9.1 Configuration of the TP when using CanCanelTransmit()................. 14 
4.9.2 Example Code .................................................................................. 14  
4.10 Handling of the version message......................................................... 14 
4.11 Configuring the Part Offline  mode....................................................... 14 
4.12 Supervision Reset on Request of the Diagnosis.................................. 15 
5 Sleep and Wake Up sequence PSA............................................................ 15 
5.1 Transition from Sleep ( Veille ) to WakeUp ( Reveil ) .............................. 15 
5.1.1 External event ( Organ type 1, 2 and 4 ):.......................................... 16 
5.1.2 Bus event  ( Organ type 1, 2 and 4 )................................................. 16 
5.1.3 +CAN activation Organ type 1 and 2 ................................................ 17 
5.1.4 +CAN activation Organ type 3 .......................................................... 17 
5.2 Transition to Veille................................................................................... 18  
5.2.1 Organ type 1,2 and 4........................................................................ 18  
5.2.2 Organ type 3..................................................................................... 18  
5.3 Setting and Releasing a Request for the network ................................... 19 
5.4 Indication of the +CAN signal to the Station manager............................. 19 
6 API of the station-manager ......................................................................... 19  
6.1 Version of the source code...................................................................... 19  
6.2 station-manager services called by the application ................................. 20 
6.2.1 SmInitPowerOn: Initialisation of the station-manager ....................... 20 
6.2.2 SmTask: cyclic Task......................................................................... 20  
6.2.3 SmGetStatus: Read the internal status of ECU ................................ 20 
6.2.4 SmGetVolCNerr: Read the Value of the volatile Nerr Counter (Macro)
 20 
6.2.5 SmSetVolCNerr: Set the Value of the volatile Nerr Counter (Macro) 21 
6.2.6 SmGetVolCPerteCom: R ead the Value of the volatile PerteCom 
Counter (Macro)............................................................................................. 21  
6.3 SmSetVolCPerteCom: Set the Value of  the volatile PerteCom Counter 
(Macro).............................................................................................................. 21  
6.3.1 SmGetVolCBoff: Read the Value of  the volatile BusOff Counter 
(Macro) 21 
6.3.2 SmSetVolCBoff: Set the Value of the volatile BusOff Counter (Macro)
 22 
©2011, Vector Informatik GmbH TechnicalR eference_Stationmanager.doc Version 3.05

---

Station manager for PSA Technical Reference 3 
6.3.3 SmSetWakeUpRequest: A CAN frame was received and woke up the 
ECU 22 
6.3.4 SmSetNetworkRequest: Release a Network Request to the network 
management.................................................................................................. 22  
6.3.5 SmReleaseNetworkRequest: Release a Network Request to the 
network management .................................................................................... 22  
6.3.6 SmSetPlusCanState(state)............................................................... 23 
6.3.7 SmTransmitNmMessage: Tranmsit the supervised Tx message on 
next call of SmTask() ..................................................................................... 23  
6.4 Application functions required by the station-manager............................ 24 
6.4.1 ApplSmStatusIndicationTx: Status of transmission indication .......... 24 
6.4.2 ApplSmStatusIndicationRx: Status of reception indication ............... 24 
6.4.3 ApplSmStatusIndicationNerr: Status of Nerr Pin indication .............. 24 
6.4.4 ApplSmStatusIndication: State of ECU has changed ....................... 25 
6.4.5 ApplCanErrorPin: Get Status of Transceiver Error Pin ..................... 25 
6.4.6 ApplSmGetInterdMemoDef: Get Status  of filtered Interd_Memo_Def 
Bit 25 
6.4.7 ApplSmSetNVAbsentCount: Set the non volatile Rx counter ........... 25 
6.4.8 ApplSmSetNVMuteCount: Set the non volatile Tx counter ............... 26 
6.4.9 ApplSmSetNVNerrCount: Set the non volatile Nerr counter ............. 26 
6.4.10 ApplSmGetNVAbsentCount: Get the non volatile Rx counter ....... 26 
6.4.11 ApplSmGetNVMuteCount: Get the non volatile Tx counter........... 26 
6.4.12 ApplSmGetNVNerrCount: Get the non volatile Nerr counter......... 27 
6.4.13 ApplSmTrcvOn: Switch on the transceiver .................................... 27 
6.4.14 ApplSmTrcvOff: Switch off the transceiver .................................... 27 
6.4.15 ApplNwmBusOff: Bus off indication............................................... 27 
6.4.16 ApplNwmBusOffEnd: Bus off recovery ended ............................... 28 
6.4.17 ApplSmFatalError: Error in assertion occurred.............................. 28 
7 Configuration of the station-manager........................................................ 29 
7.1 General Configuration ............................................................................. 29  
7.2 Status Callback functions........................................................................ 29  
7.2.1 ECU StateChange Callback: ............................................................ 29 
7.2.2 Fault State Support:.......................................................................... 29  
©2011, Vector Informatik GmbH TechnicalR eference_Stationmanager.doc Version 3.05

---

Station manager for PSA Technical Reference 4 
7.2.3 Fault Storage Support:...................................................................... 30  
7.2.4 Bus Off Callback Support : ............................................................... 30 
7.2.5 Bus Off End Callback Support: ......................................................... 30 
7.2.6 Use Flag InterdMemoDef.................................................................. 30  
7.2.7 ECU State Change in Task Context ................................................. 30 
7.2.8 N_as Timeout Handling .................................................................... 30  
7.2.9 Sleep Management........................................................................... 30  
7.2.10 Task cycle ..................................................................................... 30  
7.2.11 Debug Support .............................................................................. 31  
8 Database attributes ..................................................................................... 32  
8.1 Receive Message Attribute ..................................................................... 32  
8.2 Signal Attribute........................................................................................ 33  
9 Precautions .................................................................................................. 34  
9.1 Calling CanSleep(…); wit hin status callback ........................................... 34 
 
©2011, Vector Informatik GmbH TechnicalR eference_Stationmanager.doc Version 3.05

---

Station manager for PSA Technical Reference 5 
1 History 
 
Author Date Version Remarks 
Dieter Schaufelberger 2008-01-29 3.00 creation of this document 
Dieter Schaufelberger 2008-02-12 3.01 Firest corrections 
Dieter Schaufelberger 2008-03-14 3.02 Added new API, modify Sleep/WakeUp 
Dieter Schaufelberger 2008-06-25 3.03 Minor corrections 
Dieter Schaufelberger 2008-07-11 3.04 Added support of start delay time  
Marco Pfalzgraf 2011-07-28 3.05 Update of user specification [INM PSA] 
1.1 SM Version 
This document refers to version 3.03.00 of the station-manager for the PSA Low Speed 
Fault Tolerant bus.  
2 Introduction 
The aim of this document is to describe the handling of the station-manager for PSA. 
This document contains 
 a short description of the station-manager 
 the condition for using the station-manager 
 the interfaces of the user program for the station-manager 
This chapter gives a brief overview of the tasks and aims of the station-manager. 
Please refer also to the specification of the Indirect Network Management [INM PSA]. 
2.1 Reference Documents 
For understanding and using this manual, it is very important to know the listed docu-
ments. 
Abbreviation Document Document 
[INM PSA] 
 
96 649 896 99 Ind[OR] Phases de vie reseau   
96 649 897 9B Ind[OR]  Specification de regles communication 
[CANdriver] User manual of the Vector CAN Driver 
[INM_OSEK] User manual of the Vector OSEK_INM 
2.2 Abbreviations 
Instead of using complete expressions, the following abbreviations are used in the text. 
Abbreviation Complete expression 
ECU  Electronic Control Units 
INM Indirect Network Management 
IL Interaction Layer 
©2011, Vector Informatik GmbH TechnicalR eference_Stationmanager.doc Version 3.05

---

Station manager for PSA Technical Reference 6 
SM station-manager 
 
2.3 Tasks and Aims 
The SM provides services for a user program operating on a CAN-Bus. 
These services contain: 
 Handling of network management states  
 Handling of states of the supervised ECU’s 
 Handling of non volatile storage of error counters/states 
 Monitoring and handling of “Perte_Com” situation (Limp Home) 
3 Network management states 
This  chapter gives a brief description about the different ECU states and the ECU behav-
iour in those states according to [INM PSA].  
3.1 Organ Type 1  
Organ Type 1 is able to wake up the CAN communication in case of an external event 
(e.g. door control ).  In case of Limp Home ( non reception of message “Commande_BSI”) 
it enters state “Perte Com”. 
3.1.1 Description of internal States for organ type 1: 
 
State Description 
VEILLE  Physical Layer in Sleep mode. Detection of Bus activity. 
No transmission possible. 
REVEIL Transient state in which the communication is initialised.  
If the organ itself wakes up the bus a periodic wake up message 
must be send.  
Supervision of the Commande_BSI. 
NORMAL Transmission of the wake up message is stopped. 
Transmission of the version message. 
Transmission and reception of functional messages. 
Netmanagement diagnosis. 
Supervision of the Commande_BSI. 
MIS EN  VEILLE Transmission of functional messages interrupted. 
Supervision of the Commande_BSI. 
COM OFF Transmission of functional messages interrupted. 
Supervision of the Commande_BSI. 
Perte Com Transmission of functional messages. 
 
©2011, Vector Informatik GmbH TechnicalR eference_Stationmanager.doc Version 3.05

---

Station manager for PSA Technical Reference 7 
3.2 Organ Type 2 
Organ Type 2 is able to wake up the CAN communication in case of an external event 
(e.g. door control ). In case of Limp Home ( non reception of message “Commande_BSI”) 
it enters state “MIS EN VEILLE”. 
3.2.1 Description of internal States for organ type 2 : 
 
State Description 
VEILLE Physical Layer in Sleep mode. Detection of Bus activity. 
No transmission possible. 
REVEIL Transient state in which the communication is initialised.  
If the organ itself wakes up the bus a periodic wake up message 
must be send. 
Supervision of the Commande_BSI. 
NORMAL Transmission of the wake up message is stopped. 
Transmission of the version message. 
Transmission and reception of functional messages. 
Netmanagement diagnosis. 
Supervision of the Commande_BSI. 
MIS EN VEILLE Transmission of functional messages interrupted. 
Supervision of the Commande_BSI. 
COM OFF Transmission of functional messages interrupted. 
Supervision of the Commande_BSI. 
3.3 Organ Type 3 
ECUs Organ Type 3 are supplied by +CAN which is switched off by the BSI when going 
into the state VEILLE. Therefore these ECUs aren’t able to wake up the CAN communica-
tion.  In case of Limp Home ( non reception of message “Commande_BSI”) it enters state 
“Perte Com”. 
3.3.1 Description of internal States for organ type 3 : 
 
State Description 
VEILLE +CAN absent => no power supply 
Detection of Bus activity not possible. 
Transmission of any message impossible. 
REVEIL Transient state in which the communication is initialised.  
Supervision of the Commande_BSI. 
NORMAL Transmission of the wake up message is stopped. 
Transmission of the version message. 
Transmission and reception of functional messages. 
Netmanagement diagnosis. 
Supervision of the Commande_BSI. 
MIS EN  VEILLE Transmission of functional messages interrupted. 
Supervision of the Commande_BSI. 
COM OFF Transmission of functional messages interrupted. 
Supervision of the Commande_BSI. 
©2011, Vector Informatik GmbH TechnicalR eference_Stationmanager.doc Version 3.05

---

Station manager for PSA Technical Reference 8 
Perte Com Transmission of functional messages. 
 
3.4 Organ Type 4  
Organ Type 4 is able to wake up the CAN communication in case of an external event 
(e.g. door control ). In case of Limp Home ( non reception of message “Commande_BSI”) 
it enters state “MIS EN VEILLE”. 
3.4.1 Description of internal States for organ type 4 : 
 
State Description 
VEILLE  Physical Layer in Sleep mode. Detection of Bus activity. 
No transmission possible. 
REVEIL Transient state in which the communication is initialised.  
Supervision of the Commande_BSI. 
NORMAL Transmission of the wake up message is stopped. 
Transmission of the version message. 
Transmission and reception of functional messages. 
Netmanagement diagnosis. 
Supervision of the Commande_BSI. 
MIS EN  VEILLE Transmission of functional messages interrupted. 
Supervision of the Commande_BSI. 
COM OFF Transmission of functional messages interrupted. 
Supervision of the Commande_BSI. 
 
4 Integration into the application 
This chapter describes the steps for the integration of the SM in the application of an 
ECU. 
4.1  Delivery Items 
The SM is always combined with the indirect network management OSEK_INM. Never-
theless it is an own module which could be used stand-alone ( not recommended ).  
The delivery includes 
- Header files     Stat_mgr.h 
- Source code file (includes the SM itself)    Stat_mgr.c 
-     Source code file GenericPrecopy.c 
this user manual   Technical Reference station-manager. 
©2011, Vector Informatik GmbH TechnicalR eference_Stationmanager.doc Version 3.05

---

Station manager for PSA Technical Reference 9 
4.2 Version Changes 
Changes and bug fixes in the SM are listed at the beginning of the header and source 
code file. 
4.3 Handling of the station-manager 
Please include the header file of the SM in all modules in which you require services of 
the SM. In this file all available services including prototypes of the required interfaces and 
symbolic constants are defined. 
Add Stat_mgr.c , GenericPrecopy.c  and the generated file  StMgrLs_par.c to your make 
file/project file. 
Before the SM can be used, it must be initialised once after power on reset. Therefore the 
function SmInitPowerOn() has to be called.  
After the SM was initialized, the function SmTask(…)  must be called cyclically with the 
period time defined in the Generation tool.  
All other services of the SM have to be called by the application when they are required. A 
more detailed description of every function is found in the chapter “API of the station-
manager”. 
4.4 Particularities if there is no Interaction Layer in the system 
If there is no Interaction Layer present in the system, the Station manager takes care 
about the cyclic sending of the supervised Tx message. 
4.4.1 Event transmission of the supervised Tx message 
On some systems this message has to be send also on event. Therefore an interface is 
provided to handle this: 
SmTransmitNmMessage: Tranmsit the supervised Tx message on next call of 
SmTask() 
 
Prototype   Void SmTransmitNmMessage( channel)  
Parameter  Channel Channel on which the supervised message must be sent 
Return code   
Function de-
scription 
This function checks for the minimum send delay and sets the internal Tx cycle counter 
to the appropriate value to transmit the  supervised Tx message as soon as possible 
(keeping the minimum send delay).  
Particularities   
and Limitations 
 
4.5 Start delay time of Tx messages 
If the Tx messages have to keep a defined start delay time, the database attribute 
GenMsgStartDelayTime has to be set for each Tx message to the corresponding delay 
time. 
4.5.1 Start delay time without Interaction Layer 
If there is no Interaction Layer in the system , the start delay time has to be kept by the 
application.  
©2011, Vector Informatik GmbH TechnicalR eference_Stationmanager.doc Version 3.05

---

Station manager for PSA Technical Reference 10 
For the supervised Tx messages, which is transmitted by the Station manager (s. chap. 
4.4), the start delay time has to be provided by the application using the following array: 
V_MEMROM0 V_MEMROM1 vuint16 V_MEMROM2 bSmInmMsgDelayTime[SM_CHANNELS]= {x}; 
The delay time “x” has to be given normalized, which means “Delay Time / Task cycle”. 
A delay time of 25ms using a task cycle of the Stationmanager of 5ms gives x= 25/5 = 5. 
V_MEMROM0 V_MEMROM1 vuint16 V_MEMROM2 bSmInmMsgDelayTime[SM_CHANNELS]= {5}; 
 
4.6 Reading of Nerr state 
The state of the Bit Nerr is read by the station-manager using the callback function 
ApplCanErrorPin(). In this callback function the application has to read the Nerr pin of the 
transceiver. According to the requirement GEN-RESEAU-ST-RCCANLS.0095 (1) the state of 
the Bit Nerr must be read maximum 88μ s after the reception of the Commande_BSI. This require-
ment can not be met under all circumstances.  Depending on the system design (platform, hard-
ware clock, polling mode, … ) this time may be exceeded. Therefore this timing ** must ** be 
measured using the real target on customer side.  
If the requirement isn’t met, the following solution has to be implemented: 
Activate callback function ApplCanMsgReceived in the CanDriver folder of the Gentool. In this call-
back function the application has to read the state of the Nerr pin and store it in a variable. If later 
on the callback function ApplCanErrorPin() is called, return the stored value.  
This will ensure that the Nerr pin is read immediately after the reception of the message.  
Disadvantage: 
State of Nerr pin is read with every message not only Commande_BSI. 
4.7 Handling of the signal Interd_Memo_Def 
To activate the handling of the signal Interd_Memo_Def select the switch InterdMemoDef 
support  in the Generation tool. 
If the handling is activated, the application has to provide the callback function 
ApplSmGetInterdMemoDef( ) which return 0 if the signal is not set and >0 if the signal is 
set. 
If the signal is set, the SM keeps all volatile counters unchanged ( absent, mute, nerr,) 
when in mode Normal or ComOff.  
The PerteCom supervision is still active.    
4.8 Handling of Lmin 
If there are messages where the Lmin value is smaller as the specified DLC, special care 
has to be taken when reading signals of those messages. Lmin gives the minimal length 
of a message until its still accepted by the ECU. Lmin can be equal to message DLC or 
smaller. To ensure the correct functionality of the stack please set the database message 
attribute GenMsgMinAcceptLength to Lmin or DLC if there is no Lmin value given ( s. 
6.1 )  
For messages with Lmin < DLC special care has to be taken by the application. First of all 
a short description how the available signal flags are handled by the IL. 
©2011, Vector Informatik GmbH TechnicalR eference_Stationmanager.doc Version 3.05

---

Station manager for PSA Technical Reference 11 
4.8.1 First value and Indication flags 
If the received DLC is >= Lmin the firstvalue, and indication  flags are only set for the 
signals which are entirely contained in the message. Also the indication function is only 
called for these signals. 
4.8.2 Timeout flags and functions 
If the message is missing but was received before with a DLC > Lmin, timeout  flags and 
functions are only called for the signals entirely contained in the DLC received last time. If 
the message was never received, the flags and functions are set and called for all signals. 
4.8.3 Impact on the application 
Before accessing a signal the application has to prove if the signal was received by check-
ing the corresponding indication flag. If the indication flag is set, the signal was entirely 
received and can be used. Otherwise the default value must be used. For the further han-
dling two cases must be treated: 
1. The DLC will not change during a session ( Init -> Stop ) 
This means the message is always received with the same DLCmessage where Lmin <= 
DLCmessage <= DLC. In this case the indication flags are set once and don’t need to be 
cleared by the application. The signal can be accessed whenever needed (of course the 
indication flag still has to be checked !).  
2. The DLC may change with every message 
This means the message may have a different DLC on every reception. In this case the 
application must clear the indication flags when a new message is received before they 
are set by the IL. This ensures that the indication fl

*[…only the first 12 of 35 pages extracted…]*
