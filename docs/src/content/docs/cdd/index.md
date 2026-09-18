---
title: 'Complex Device Drivers (CDD)'
description: 'Complex device drivers and sensor/actuator SW-Cs (Sa_/Cd_) that access hardware directly outside the standard MCAL/ECU-abstraction path.'
sidebar: { order: 0 }
---

# Complex Device Drivers (CDD)

Complex device drivers and sensor/actuator SW-Cs (Sa_/Cd_) that access hardware directly outside the standard MCAL/ECU-abstraction path.

## Modules in this layer

| Module | Component | Summary |
| --- | --- | --- |
| [DigHwTrqSENT](./dighwtrqsent/) | Sa_DigHwTrqSENT | Digital handwheel-torque acquisition over SENT protocol including signal validation. |
| [DigMSB](./digmsb/) | Sa_DigMSB | Digital motor-sensor-board (MSB) interface: rotor position/speed acquisition from the digital position sensor. |
| [SVDiag](./svdiag/) | Ap_DigPhsReasDiag, Sa_MtrDrvDiag | Space-vector/motor-driver diagnostics: phase-reasonableness and power-stage fault detection. |
| [SVDrvr_CM](./svdrvr_cm/) | PwmCdd | Space-vector PWM driver CDD (current mode) driving the inverter power stage. |
| [SpiNxt](./spinxt/) | SpiNxt | Nexteer SPI handler (CDD) with interrupt service for external devices (sensors, SBC). |
| [SwProject/CDDInterface](./swproject-cddinterface/) | Sa_CDDInterface10, Sa_CDDInterface11, Sa_CDDInterface6, Sa_CDDInterface9 | CDD interface layer (Sa_CDDInterface*) bridging application SW-Cs and complex drivers. |
| [SwProject/SrlComDriver](./swproject-srlcomdriver/) | AUTOSAR Cd_SrlComDriver (customised) | Serial-communication driver CDD (PSA BMPV vehicle bus interface). |
| [SwProject/SrlComInput](./swproject-srlcominput/) | AUTOSAR Ap_SrlComInput (customised) | Serial-communication input layer: receives/decodes vehicle signals for application SW-Cs. |
| [SwProject/SrlComOutput](./swproject-srlcomoutput/) | AUTOSAR Ap_SrlComOutput (customised) | Serial-communication output layer: encodes/transmits EPS signals to the vehicle bus. |
| [TMS570_uDiag](./tms570_udiag/) | Cd_uDiagCCRM, Cd_uDiagClockMonitor, Cd_uDiagECC, Cd_uDiagESM, Cd_uDiagFPU, Cd_uDiagIOMM, Cd_uDiagLossOfExec, Cd_uDiagParity, Cd_uDiagPeriphMPU, Cd_uDiagResetHandler, Cd_uDiagStaticRegs, Cd_uDiagVIM, Cd_uDiagUtility | Micro-level diagnostics CDD: FPU, flash-test, OS-error callouts and utility self-tests. |
| [TmprlMon](./tmprlmon/) | Sa_TmprlMon, Sa_TmprlMon2 | Temporal monitor (safety, ASIL-D): independent timing plausibility of software execution. |
| [ePWM](./epwm/) | Ap_ePWM2, Cd_Nhet1 | ePWM/NHET driver CDD (ePWM, NHET programs incl. SENT) for PWM generation and capture on TMS570. |
