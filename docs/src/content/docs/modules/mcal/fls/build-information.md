---
title: 'build information'
description: 'Converted design document: build information'
---

> **Source:** `Fls/doc/build_information.txt`  
> **Module:** [Fls](../../../../mcal/fls/)  
> **Note:** Plain-text file reproduced verbatim.

---

```text
***************************************************************************

  Build Information Document

  Hercules� ARM� Safety MCUs - F021 Flash API      
  v2.01.01 Build(000830)                           
  Build Date:  2014-08-11                                       

***************************************************************************

---------------------------------------------------------------------------
 1. Introduction
---------------------------------------------------------------------------
This file contains specific infomation relating to this build of the
F021 Flash API.  

---------------------------------------------------------------------------
 2. Function Callgraph / Function Size / Worst Case Stack Usage
---------------------------------------------------------------------------
This section contain a list of all functions within the F021 Flash
API along with the functions they call, function size in bytes, and
worst case stack usage for that function for each delivered library
variant.  Additionally, at the end of the each variants list, is the
function with max worst case stack usage.



---------------------------------------------------------------------------
   2.1 F021 API CortexM3 BE Library
---------------------------------------------------------------------------

---------------------------------------------------------------------------
|                                               |   Worst    |            |
|                                               |   Case     |            |
|                                               |   Stack    |  Function  |
|               Function Call Graph             |   Usage    |    Size    |
---------------------------------------------------------------------------
|  Fapi_calculateEcc                            |          0 |         16 |
---------------------------------------------------------------------------
|  Fapi_calculateFletcherChecksum               |          8 |         56 |
---------------------------------------------------------------------------
|  Fapi_calculatePsa                            |         56 |        120 |
|  |  _Fapi_loopRegionForPsaValue               |         32 |         90 |
|  |  |  Fapi_isAddressEcc                      |          0 |         56 |
|  |  |  _Fapi_checkWdService                   |          0 |         12 |
|  |  |  |  Fapi_serviceWatchdogTimer           | (User Defined Function) |
---------------------------------------------------------------------------
|  Fapi_disableBanksForOtpWrite                 |          0 |         26 |
---------------------------------------------------------------------------
|  Fapi_disableFsmDoneEvent                     |          0 |         38 |
---------------------------------------------------------------------------
|  Fapi_doBlankCheck                            |         96 |        124 |
|  |  Fapi_flushPipeline                        |         16 |         34 |
|  |  |  Fapi_waitDelay                         |          8 |         48 |
|  |  _Fapi_loopRegionForValue                  |         48 |         94 |
|  |  |  Fapi_flushPipeline                     |         16 |         34 |
|  |  |  |  Fapi_waitDelay                      |          8 |         48 |
|  |  |  _Fapi_checkWdService                   |          0 |         12 |
|  |  |  |  Fapi_serviceWatchdogTimer           | (User Defined Function) |
|  |  |  _Fapi_readDword                        |         16 |         44 |
|  |  |  |  Fapi_isAddressEcc                   |          0 |         56 |
---------------------------------------------------------------------------
|  Fapi_doBlankCheckByByte                      |         96 |        124 |
|  |  Fapi_flushPipeline                        |         16 |         34 |
|  |  |  Fapi_waitDelay                         |          8 |         48 |
|  |  _Fapi_loopRegionForValueByByte            |         48 |         84 |
|  |  |  Fapi_flushPipeline                     |         16 |         34 |
|  |  |  |  Fapi_waitDelay                      |          8 |         48 |
|  |  |  _Fapi_checkWdService                   |          0 |         12 |
|  |  |  |  Fapi_serviceWatchdogTimer           | (User Defined Function) |
---------------------------------------------------------------------------
|  Fapi_doMarginRead                            |         64 |        104 |
|  |  Fapi_isAddressEcc                         |          0 |         56 |
|  |  _Fapi_checkWdService                      |          0 |         12 |
|  |  |  Fapi_serviceWatchdogTimer              | (User Defined Function) |
|  |  _Fapi_enterMarginMode                     |         32 |         96 |
|  |  |  Fapi_flushPipeline                     |         16 |         34 |
|  |  |  |  Fapi_waitDelay                      |          8 |         48 |
|  |  _Fapi_exitMarginMode                      |         32 |         38 |
|  |  |  Fapi_flushPipeline                     |         16 |         34 |
|  |  |  |  Fapi_waitDelay                      |          8 |         48 |
---------------------------------------------------------------------------
|  Fapi_doMarginReadByByte                      |         56 |         52 |
|  |  _Fapi_checkWdService                      |          0 |         12 |
|  |  |  Fapi_serviceWatchdogTimer              | (User Defined Function) |
|  |  _Fapi_enterMarginMode                     |         32 |         96 |
|  |  |  Fapi_flushPipeline                     |         16 |         34 |
|  |  |  |  Fapi_waitDelay                      |          8 |         48 |
|  |  _Fapi_exitMarginMode                      |         32 |         38 |
|  |  |  Fapi_flushPipeline                     |         16 |         34 |
|  |  |  |  Fapi_waitDelay                      |          8 |         48 |
---------------------------------------------------------------------------
|  Fapi_doPsaVerify                             |         64 |          4 |
|  |  _Fapi_checkRegionForPsaValue              |         64 |        138 |
|  |  |  Fapi_flushPipeline                     |         16 |         34 |
|  |  |  |  Fapi_waitDelay                      |          8 |         48 |
|  |  |  _Fapi_loopRegionForPsaValue            |         32 |         90 |
|  |  |  |  Fapi_isAddressEcc                   |          0 |         56 |
|  |  |  |  _Fapi_checkWdService                |          0 |         12 |
|  |  |  |  |  Fapi_serviceWatchdogTimer        | (User Defined Function) |
|  |  |  _Fapi_setReadMargin0                   |         32 |         52 |
|  |  |  |  Fapi_flushPipeline                  |         16 |         34 |
|  |  |  |  |  Fapi_waitDelay                   |          8 |         48 |
---------------------------------------------------------------------------
|  Fapi_doVerify                                |         96 |         18 |
|  |  _Fapi_checkRegionForValue                 |         80 |        122 |
|  |  |  _Fapi_enterMarginMode                  |         32 |         96 |
|  |  |  |  Fapi_flushPipeline                  |         16 |         34 |
|  |  |  |  |  Fapi_waitDelay                   |          8 |         48 |
|  |  |  _Fapi_exitMarginMode                   |         32 |         38 |
|  |  |  |  Fapi_flushPipeline                  |         16 |         34 |
|  |  |  |  |  Fapi_waitDelay                   |          8 |         48 |
|  |  |  _Fapi_loopRegionForValue               |         48 |         94 |
|  |  |  |  Fapi_flushPipeline                  |         16 |         34 |
|  |  |  |  |  Fapi_waitDelay                   |          8 |         48 |
|  |  |  |  _Fapi_checkWdService                |          0 |         12 |
|  |  |  |  |  Fapi_serviceWatchdogTimer        | (User Defined Function) |
|  |  |  |  _Fapi_readDword                     |         16 |         44 |
|  |  |  |  |  Fapi_isAddressEcc                |          0 |         56 |
---------------------------------------------------------------------------
|  Fapi_doVerifyByByte                          |         96 |         18 |
|  |  _Fapi_checkRegionForValueByByte           |         80 |        122 |
|  |  |  _Fapi_enterMarginMode                  |         32 |         96 |
|  |  |  |  Fapi_flushPipeline                  |         16 |         34 |
|  |  |  |  |  Fapi_waitDelay                   |          8 |         48 |
|  |  |  _Fapi_exitMarginMode                   |         32 |         38 |
|  |  |  |  Fapi_flushPipeline                  |         16 |         34 |
|  |  |  |  |  Fapi_waitDelay                   |          8 |         48 |
|  |  |  _Fapi_loopRegionForValueByByte         |         48 |         84 |
|  |  |  |  Fapi_flushPipeline                  |         16 |         34 |
|  |  |  |  |  Fapi_waitDelay                   |          8 |         48 |
|  |  |  |  _Fapi_checkWdService                |          0 |         12 |
|  |  |  |  |  Fapi_serviceWatchdogTimer        | (User Defined Function) |
---------------------------------------------------------------------------
|  Fapi_enableBanksForOtpWrite                  |          0 |         26 |
---------------------------------------------------------------------------
|  Fapi_enableEepromBankSectors                 |         16 |        122 |
|  |  Fapi_getNumberOfBankSectors               |          0 |         12 |
|  |  _Fapi_EnableSectors                       |          0 |         60 |
---------------------------------------------------------------------------
|  Fapi_enableFsmDoneEvent                      |          0 |         38 |
---------------------------------------------------------------------------
|  Fapi_enableMainBankSectors                   |         16 |        100 |
|  |  Fapi_getNumberOfBankSectors               |          0 |         12 |
---------------------------------------------------------------------------
|  Fapi_flushPipeline                           |         16 |         34 |
|  |  Fapi_waitDelay                            |          8 |         48 |
---------------------------------------------------------------------------
|  Fapi_getBankSectors                          |         32 |        242 |
|  |  _Fapi_scaleSectorSize                     |          0 |         20 |
---------------------------------------------------------------------------
|  Fapi_getDeviceInfo                           |         32 |         60 |
---------------------------------------------------------------------------
|  Fapi_getLibraryInfo                          |         24 |         64 |
---------------------------------------------------------------------------
|  Fapi_getNumberOfBankSectors                  |          0 |         12 |
---------------------------------------------------------------------------
|  Fapi_initializeFlashBanks                    |        136 |        566 |
|  |  Fapi_calculateFletcherChecksum            |          8 |         56 |
|  |  _Fapi_divideUnsignedLong                  |          8 |         38 |
|  |  _scaleEEFclk                              |          0 |         12 |
|  |  _scaleMainFclk                            |          0 |         12 |
---------------------------------------------------------------------------
|  Fapi_isAddressEEPROM                         |          0 |         20 |
---------------------------------------------------------------------------
|  Fapi_isAddressEcc                            |          0 |         56 |
---------------------------------------------------------------------------
|  Fapi_issueAsyncCommand                       |          8 |         40 |
|  |  _Fapi_issueFsmCommand                     |          0 |         58 |
---------------------------------------------------------------------------
|  Fapi_issueAsyncCommandWithAddress            |         16 |         42 |
|  |  _Fapi_issueFsmCommand                     |          0 |         58 |
---------------------------------------------------------------------------
|  Fapi_issueProgrammingCommand                 |         56 |        292 |
|  |  Fapi_calculateEcc                         |          0 |         16 |
|  |  _Fapi_issueFsmCommand                     |          0 |         58 |
---------------------------------------------------------------------------
|  Fapi_issueProgrammingCommandForEccAddresses  |         80 |         38 |
|  |  Fapi_issueProgrammingCommand              |         56 |        292 |
|  |  |  Fapi_calculateEcc                      |          0 |         16 |
|  |  |  _Fapi_issueFsmCommand                  |          0 |         58 |
|  |  Fapi_remapEccAddress                      |         16 |         90 |
|  |  |  _Fapi_compareAddresses                 |          0 |         18 |
---------------------------------------------------------------------------
|  Fapi_remapEccAddress                         |         16 |         90 |
|  |  _Fapi_compareAddresses                    |          0 |         18 |
---------------------------------------------------------------------------
|  Fapi_remapMainAddress                        |         16 |        100 |
|  |  _Fapi_compareAddresses                    |          0 |         18 |
---------------------------------------------------------------------------
|  Fapi_setActiveFlashBank                      |         32 |        332 |
|  |  _scaleEEFclk                              |          0 |         12 |
|  |  _scaleMainFclk                            |          0 |         12 |
---------------------------------------------------------------------------
|  Fapi_waitDelay                               |          8 |         48 |
---------------------------------------------------------------------------
|  _Fapi_EnableSectors                          |          0 |         60 |
---------------------------------------------------------------------------
|  _Fapi_checkRegionForPsaValue                 |         64 |        138 |
|  |  Fapi_flushPipeline                        |         16 |         34 |
|  |  |  Fapi_waitDelay                         |          8 |         48 |
|  |  _Fapi_loopRegionForPsaValue               |         32 |         90 |
|  |  |  Fapi_isAddressEcc                      |          0 |         56 |
|  |  |  _Fapi_checkWdService                   |          0 |         12 |
|  |  |  |  Fapi_serviceWatchdogTimer           | (User Defined Function) |
|  |  _Fapi_setReadMargin0                      |         32 |         52 |
|  |  |  Fapi_flushPipeline                     |         16 |         34 |
|  |  |  |  Fapi_waitDelay                      |          8 |         48 |
---------------------------------------------------------------------------
|  _Fapi_checkRegionForValue                    |         80 |        122 |
|  |  _Fapi_enterMarginMode                     |         32 | 
```
