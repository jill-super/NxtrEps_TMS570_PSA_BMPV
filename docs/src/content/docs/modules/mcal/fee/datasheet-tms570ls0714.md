---
title: 'DataSheet TMS570LS0714'
description: 'Converted design document: DataSheet TMS570LS0714'
---

> **Source:** `Fee/doc/DataSheet_TMS570LS0714.pdf`  
> **Module:** [Fee](../../../../mcal/fee/)  
> **Note:** Text extracted automatically from PDF (4 pages) with pypdf; layout, figures and formatting are not preserved.

---

Copyright © 2003-2016 Texas Instruments Incorporated.  All rights reserved. 
 
Information in this document is subject to change without notice.  Texas Instruments may have pending 
patent applications, trademarks, copyrights, or other intellectual property rights covering matter in this 
document.  The furnishing of this documents is given for usage with Texas Instruments products only and 
does not give you any license to the intellectual property that might be contained within this document.  
Texas Instruments makes no implied or expressed warranties in this document and is not responsible for 
the products based from this document. 
` 
 Page 1 of 4 
 
 
 
 
 
 
Autosar FEE 01.23.04 
Data Sheet for TMS570LS0714 
19th Aug 2016

---

` 
 
Page 2 of 4  
 
TABLE OF CONTENTS 
 
1 Memory FootPrint ......................................................................................... 3 
2 Performance Numbers on API’s ................................................................... 3

---

` 
 
Page 3 of 4  
 
1 Memory FootPrint 
 
Modules In Bytes 
.text .const .bss .data 
 FEE 19836 640 1124 17 
 
Above readings were taken with following compiler settings: 
 
Compiler version : 5.1.6 
-mv7R4 --code_state=32 --float_support=VFPv3D16 --abi=eabi -O2 -g --
diag_warning=261 --diag_warning=118 --diag_warning=225 --diag_error=189 --
diag_error=994 --diag_error=551 --display_error_number  --enum_type=packed 
2 Performance Numbers on API’s 
  
API Numbers In CPU Cycles @ 160 MHz 
Ticks Comments 
TI FEE 
Fee_Init() 2677045 
Create two active VS, 
one each for   
EEPROM1 and 
EEPROM2. 
Fee_MainFunction() 2093 
Complete Pending 
INIT writes. 
Fee_Write() 11395 
 
Fee_MainFunction() 37074 
Measure time to 
complete write 
job.(block size = 8. 
Total 40 bytes) 
Fee_MainFunction() 751 
When no jobs are 
pending. 
Fee_Read() 3538 
 
Fee_MainFunction() 1942649 
Measure time to 
complete Read job(8 
bytes) 
Fee_InvalidateBlock() 1242 
 
Fee_MainFunction() 2059 
Measure time to 
complete Invalidate 
job. 
Fee_EraseImmediateBlock() 1476 
 
Fee_MainFunction() 2072 
Measure time to 
complete

---

` 
 
Page 4 of 4  
 
EraseImmediate job. 
Fee_Cancel() 318 
 Fee_GetJobResult() 209 
 Fee_GetVersionInfo( ) 73 
 Fee_GetStatus( ) 303 
  
Note: For above readings, 4 physical sectors, each of 4K were combined to one virtual 
sector forming 16K. Two EEPROM’s, each using two 16K virtual sectors.
