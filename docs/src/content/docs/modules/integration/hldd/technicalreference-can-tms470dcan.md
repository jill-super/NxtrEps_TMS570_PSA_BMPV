---
title: 'TechnicalReference CAN TMS470DCAN'
description: 'Converted design document: TechnicalReference CAN TMS470DCAN'
---

> **Source:** `PSA_BMPV_EPS_TMS570/HLDD/BSW/TechnicalReference_CAN_TMS470DCAN.pdf`  
> **Module:** [hldd](../../../../integration/hldd/)  
> **Note:** Text extracted automatically from PDF (28 pages) with pypdf; layout, figures and formatting are not preserved.

---

Vector CAN Driver 
Technical Reference 
 
Texas Instruments 
TMS470 
DCAN 
 
 
 
 
 
 
 
 
Authors Georg Pflügel, Karol Kostolny, Sebastian Gaertner, Arthur Jendrusch 
Versions: 1.05.00 
Status: Released

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
2 /28  
Contents 
1 Introduction ................................ ................................ ................................ ................... 5 
2 Important References ................................ ................................ ................................ ... 6 
2.1 Known Compatible Derivatives ................................ ................................ ........ 6 
3 Usage of Controller Features ................................ ................................ ....................... 8 
3.1 [#hw_comObj] - Communication Objects ................................ ......................... 8 
3.2 Miscellaneous ................................ ................................ ................................ . 9 
4 [#hw_sleep] - SleepMode and WakeUp ................................ ................................ ...... 10 
4.1 Global Power down mode ................................ ................................ ............. 10 
4.2 Local Power down mode ................................ ................................ ............... 11 
5 [#hw_loop] - Hardware Loop Check ................................ ................................ ........... 12 
6 [#hw_busoff] - Bus off ................................ ................................ ................................  13 
7 CAN Driver Features ................................ ................................ ................................ ... 14 
7.1 [#hw_feature] - Feature List ................................ ................................ ........... 14 
7.2 Description of Hardware related features ................................ ...................... 16 
7.2.1 [#hw_status] – Status ................................ ................................ .................... 16 
7.2.2 [#hw_stop] - Stop Mode ................................ ................................ ................. 16 
7.2.3 [#hw_int] - Control of CAN Interrupts ................................ ............................. 16 
7.2.4 [#hw_cancel] - Cancel in Hardware ................................ ...............................  17 
7.2.5 Polling Mode ................................ ................................ ................................ . 18 
8 [#hw_assert] - Assertions ................................ ................................ ........................... 19 
9 API ................................ ................................ ................................ ................................  20 
9.1 Category ................................ ................................ ................................ ....... 20 
10 Implementations Hints ................................ ................................ ................................  21 
10.1 Important Notes ................................ ................................ ............................. 21 
11 Configuration ................................ ................................ ................................ .............. 22 
11.1 Configuration by GENy ................................ ................................ .................. 22 
11.1.1 Compiler and Chip Selection ................................ ................................ ......... 22 
11.1.2 Bus Timing ................................ ................................ ................................ .... 23 
11.1.3 Acceptance Filtering ................................ ................................ ...................... 24

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
3 /28  
12 Known Issues / Limitations ................................ ................................ ........................ 27 
13 Contact................................ ................................ ................................ ......................... 28

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
4 /28  
History 
 
Author Date Version Remarks 
Georg Pflügel 12.06.2007 1.00 creation 
Karol Kostolny 28.08.2007 1.01 Low level message transmit feature added 
Sebastian Gärtner 28.07.2009 1.02 Support new derivative TMS470MSF542 
Georg Pflügel 25.10.2010 1.03 Add description for DCAN Issue#22 workaround 
Support new derivative TMS570PSFC66 
Georg Pflügel 09.12.2010 1.03.01 Add description for the already supported derivatives 
TMS570PSFC61, TMS570LS1x and TMS570LS2x 
Georg Pflügel 29.09.2011 1.03.02 Add description for the already supported derivatives 
TMS470MSF542, TMS470MF03107, TMS470MF04207 
and TMS470MF06607. 
Arthur Jendrusch 20.12.2011 1.03.03 CAN Driver Version changed to V1.14.01 
Support new derivative TMS570LS30316U 
Arthur Jendrusch 16.04.2012 1.03.04 Support new derivative TMS570LS12004U 
Georg Pflügel 04.06.2012 1.04.00 Support of local dower down mode 
Support of wakeup polling 
Georg Pflügel 06.12.2012 1.05.00 Support new derivatives TMS570LS0322 and 
TMS470PSF764

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
5 /28  
1 Introduction 
The concept of the CAN driver and the standardized interface between the CAN driver and 
the application is described  in the document TechnicalReference_CANDriver.pdf. The CAN 
driver interface to the hardware is designed in a way that capabilities of the special CAN 
chips can be utilized optimally. The interface to the application was made identical for the 
different CAN chips, so that the "higher" layers such as network management, transport 
protocols and especially the application would essentially be independent of the particular 
CAN chip used. 
 
This document describes the hardware dependent special features and implem entation 
specifics of the CAN Chip D-CAN on the microcontrollers TMS470 and TMS570.

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
6 /28  
2 Important References 
The following table summarizes information about the CAN Driver. It gives you detailed 
information about the versions, derivatives and compilers. As a very important information 
the documentations of the hardware manufacturers are listed. The CAN Driver is based 
upon these documents in the given version.  
 
Drivers RI Derivative Compiler Hardware Manufacturer   
Document Name Version 
1.14.01 1.5 TMS470PSF761 
TMS570PSF762 
TMS470PSF764 
TMS470MSF542 
 
TMS570PSFC66 
 
TMS570PSFC61 
TMS570LS30316U 
TMS570LS12004U 
TMS570LS0322 
 
Texas 
Instruments 
ARM 
TMS470PSF761 DesignSpec.pdf 
TMS570PSF762_1.5.pdf 
TMS470PSF764 Delphinus datasheet .pdf 
TMS470MSF54x TRM (Draft) 
TMS470MSF542PZ DesignSpec.pdf 
TMS570PSFC66_design_specification_22.pdf 
TMS570PSFC66_device_datasheet.pdf 
TMS570PSFC61_Specification_044.pdf 
Gladiator_design_specification_GM_Auto.pdf 
 
SPNS186_TMS570LS0x32_DataSheet.pdf 
 
DCAN_reference_guide_v0_23.pdf 
Rev 0.8 
Rev 1.5 
SPNS146 
02/2009 
Rev 1.01 
Rev 2.2 
SPNS141 
Rev 0.44 
V2.5.1 
 
SPNS186 
 
V 0.23 
 
Drivers: This is the current version of the CAN Driver 
RI: Shows the version of the Reference Implementation and therefore the functional scope of the CAN Driver  
Derivative: This can be a single information or a list of derivatives, the CAN Driver can be used on.  
Compiler: List of Compilers the CAN Driver is working with 
Hardware Manufacturer Document Name: List of hardware documentation the CAN Driver is based on.  
Version: To be able to reference to this hardware documentation its version is very important. 
 
2.1 Known Compatible Derivatives 
Texas Instruments has established a new name space for the TMS570 derivatives. With 
this name space it is possible to rename existing derivatives. Future planed derivatives will 
named up to now with this name space too.

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
7 /28  
Old name supported 
by Geny: 
With this selection this derivatives 
from new name space will run too: 
Comment: 
 
TMS570PSFC66 TMS570LS101xx 
TMS570LS102xx 
TMS570LS202xx 
1M Flash  128k RAM 
1M Flash  160k RAM 
2M Flash  160k RAM 
TMS470MSF542 
 
TMS470MF03107 
TMS470MF04207 
TMS470MF06607 
320k Flash  16k RAM 
448k Flash  24k RAM 
640k Flash  64k RAM

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
8 /28  
3 Usage of Controller Features 
3.1 [#hw_comObj] - Communication Objects 
 
Depending of the controller the CAN cells provide a specific number of mailboxes. 
Controller #Objects of CAN cell 1  #Objects of CAN cell 2 #Objects of CAN cell 3 
TMS470PSF761 64 32 - 
TMS570PSF762 64 32 - 
TMS470PSF764 64 32 - 
TMS470MSF542 16 32 - 
TMS570PSFC61 64 64 32 
TMS570PSFC66 64 64 32 
TMS570LS30316U 64 64 64 
TMS570LS12004U 64 64 64 
TMS570LS0322 32 16 - 
 
The generation tool supports a flexible allocation of message buffers. In the following 
tables the configuration variant s of the CAN driver are listed.  The message buffers are 
allocated in the following order for each channel: 
 
Obj number  Obj type No. of Objects comment 
     
1 – n 
 
Tx Full CAN 
0-nmsg These objects are used by CanTransmit() to send 
a certain message. The user must define 
statically (Generation Tool) which CAN messages 
are located in such Tx FullCAN objects. The 
Generation Tool distributes the messages to the 
FullCAN objects according  to their identifier 
priority. 
m 
 
Tx Normal 
1 This object is used by CanTransmit() to send 
several messages. If the transmit message object 
is busy, the transmit request is stored in a queue 
o 
 
Low Level 
Tx 
0-1 This object is used by CanMsgTransmit() to send 
it’s messages, if the low level transmit 
functionality is selected. 
p – q 
 
unused 
0-nmsg These objects are not used. It depends on the 
configuration of receive and tr ansmit objects if 
unused objects are available.

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
9 /28  
r – x 
 
Rx Full CAN 
0-nmsg These objects are used to receive specific CAN 
messages. The user defines statically 
(Generation Tool) that a CAN message should be 
received in a FullCAN  message object. The 
Generation Tool distributes the message to the 
FullCAN objects. 
y – z 
  
Basic CAN 
2-4 All other CAN messages (Application, 
Diagnostics, Network Management) are received 
via the Basic CAN message object.  
 
nmsg = (Max number of objects) – (number of Tx Normal objects) – (number of Basic CAN objects) 
 
 
 
Example 
 
For a CAN cell with 32 objects the following values are assumed: 
Configurations with Standard Id or Extended Id:   x = 30, y = 31, z = 32 
Configurations with Mixed Id:            x = 28, y = 29, z = 32 
If the configuration contains Standard Ids and Extended Ids (configuration with 
Mixed Id), the Basic CAN use 4 hardware message objects. Two of them will be 
used for the reception of the Standard Ids and two will be used for the r eception 
of the Extended Ids. 
 
3.2 Miscellaneous 
The CAN driver was designed to run in  privileged mode only. There is no support for user 
mode.

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
10 /28  
4 [#hw_sleep] - SleepMode and WakeUp 
The CAN module can be switched into sleep mode by  calling the function CanSleep and 
from sleep into operation mode by calling the function CanWakeUp. There are two power-
down modes available, the global power-down mode and the local power-down mode. The 
first is supported by all TMS570 DCAN derivates, the second only if it is documented in the 
datasheet. This is because the CAN controller has not initially supported the local power -
down mode. It was added to the DCAN cell since documented in the reference g uide 
revision 0.30. 
 
4.1 Global Power down mode 
 
The configuration-bits to set and reset the hardware of the D_CAN into and from global 
power down  mode are not inside the CAN -controller. I t is part of the Power -down-
management of the CPU. To mak e the driver independent of access to the configuration 
bits, there are two callback-functions inside CanSleep and CanWakeUp. 
 
ApplCanGoToSleepModeRequest 
 
This function will be called from CanSleep. The user has to add this function to the 
application with some code i nside to set the CAN -controller into sleep mode. Pa rameter 
CAN_CHANNEL_CANTYPE_ONLY is void for Single Receive Channels (SRC)  and 
channel for Multiple Receive Channel (MRC). 
 
Example: 
 
vuint8 ApplCanGoToSleepModeRequest(CAN_CHANNEL_CANTYPE_ONLY) 
{ 
  /* Quadrants are 256 bytes each, so DCAN1 is QUAD0 and QUAD1, DCAN2 is QUAD2 
and QUAD3 */ 
  if (channel == 0) 
  { 
    *((vuint32 *)0xFFFFE084 /* Peripheral Power-Down Set Register 1 */) = 0x00000003; /* 
QUAD0 and QUAD1 */ 
  } 
  else if (channel == 1) 
  { 
    *((vuint32 *)0xFFFFE084 /* Peripheral Power-Down Set Register 1 */) = 0x0000000C; /* 
QUAD2 and QUAD3 */ 
  } 
  return kCanOk; 
}

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
11 /28  
 
ApplCanWakeUpFromSleepModeRequest 
 
This function will be called from CanWakeUp. The user has to add this function to the 
application with some code inside to reset the CAN -controller from sleep mode. Parameter 
CAN_CHANNEL_CANTYPE_ONLY is void for Single channel and channel for Multiple 
channel. 
 
Example: 
 
vuint8 ApplCanWakeUpFromSleepModeRequest(CAN_CHANNEL_CANTYPE_ONLY) 
{ 
  /* Quadrants are 256 bytes each, so DCAN1 is QUAD0 and QUAD1, DCAN2 is QUAD2 
and QUAD3 */ 
  if (channel == 0) 
  { 
    *((vuint32 *)0xFFFFE0A4 /* Peripheral Power-Down Clear Register 1 */) = 0x00000003; 
/* QUAD0 and QUAD1 */ 
  } 
  else if (channel == 1) 
  { 
    *((vuint32 *)0xFFFFE0A4 /* Peripheral Power-Down Clear Register 1 */) = 0x0000000C; 
/* QUAD2 and QUAD3 */ 
  } 
 
  return kCanOk; 
} 
 
 
 
 
4.2 Local Power down mode 
 
If the local power down mode is selected, the PDR bit inside the CAN cell will  be used to 
set the CAN cell into the sleep mode. With this there are no cal lback functions necessary 
and the application has not to handle some additional hardware register.

---

Vector CAN Driver Technical Reference TMS470 DCAN  
2012, Vector Informatik GmbH Version: 1.05.00  
based on template version 3.2 
 
12 /28  
5  [#hw_loop] - Hardware Loop Check 
For the feature Hardware Loop Check (see TechnicalReference_CANDriver in the chapter 
Hardware Loop Check) this CAN Driver provides the following timer identifications: 
KCanLoopIrqReq 
Where is the loop implemented?  
 CAN Interrupt service routine. 
What is the loop for?   
 Loop over all pending interrupts (Rx, Tx). 
Is the loop channel dependent? Can this timer identification be called reentrant?   
 One loop for each channel, no reentrant call. 
How often is ApplCanTimerLoop called?   
Once with every pending interrupt request or permanently until loop exit. 
Maximum expected duration of the loop or maximum expected calls of the loop 
 Depend on interrupt occurrence. 
Reasons for a delay - why is the maximum expected duration exceeded?  
Defect in hardware (what leads to a longer duration than the maximum expected time)  
If the loop does not end and the application has to terminate the loop, what has to be done 
then?   
Exit loop and retrigger interrupt after application action is done. 
 
kCanLoopBusyReq 
Where is the loop implemented?  
CanCopyDataAndStartTransmission, CanBasicCanMsgReceived, CanFullCanMsgReceived 
CanHL_TxConfirmation, CanMsgTransmit 
What is the loop for?   
 Check that the CAN-cell leaves the busy state. 
Is the loop channel dependent? Can this timer identification be called reentrant?   
One loop for each channel, reentrant call. 
How often is ApplCanTimerLoop called?   
Permanently until CAN-cell leaves the busy state. 
Maximum expected duration of the loop or maximum expected calls of the loop 
The busy state need 3-6 CAN_CLK periods. 
Reasons for a delay  - why is the maximum expected duration exceeded?  
Defect  in hardware (what leads to a longer duration than the maximum expected time)  
If the loop does not end and the application has to terminate the loop, what has to be done 
then?   
If the loop does not end and the application has to terminate the loop, CanInit has to be called.

*[…only the first 12 of 28 pages extracted…]*
