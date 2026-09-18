---
title: 'Module Name Glossary'
description: 'What every abbreviated EPS module name stands for.'
---

# Module Name Glossary

Every software-module directory in this repository uses an abbreviated name. This page expands each one to its full meaning.
Entries marked with * are inferred from design evidence (port names, fault flags, file banners, MDD titles) rather than stated outright — see the notes below.

## Application Software (ASW)

| Module | Full name |
| --- | --- |
| `AbsHwPos_TcI2cVd` | Absolute Handwheel Position – Turns counter, I2C, Vehicle Dynamics |
| `ActivePull` | Active Pull Compensation |
| `Assist` | Power Steering Assist (base assist) |
| `AssistFirewall` | Assist-path safety firewall |
| `AstLmt_CM` | Assist Sum and Limit, Current Mode |
| `AvgFricLrn` | Average Friction Learning |
| `BVDiag` | Battery Voltage Diagnostics |
| `BatteryVoltage` | Battery Voltage acquisition |
| `BkCpPc` | Bulk Capacitor Precharge |
| `CmMtrCurr` | Common-Mode Motor Current measurement * |
| `ComplErr` | Compliance Error monitor |
| `CtrlTemp` | Controller Temperature |
| `CtrldDisShtdn` | Controlled Disable Shutdown |
| `Damping` | Damping Compensation |
| `DampingFirewall` | Damping-path safety firewall |
| `EOTActuatorMng` | End of Travel Actuator Management |
| `ElePwr` | Electric Power Consumption estimation |
| `EtDmpFw` | End of Travel Damping Firewall |
| `FltInjection` | Fault Injection (safety validation) |
| `FrqDepDmpnInrtCmp` | Frequency Dependent Damping and Inertia Compensation |
| `Gsod` | Global Signal Overwrite Detection * |
| `HiLoadStall` | High Load Stall protection |
| `HighFreqAssist` | High Frequency Assist |
| `HwPwUp` | Hardware Power-Up sequencing |
| `HystComp` | Hysteresis Compensation |
| `LmtCod` | Limiter Conditioning |
| `LrnEOT` | Learn End Of Travel (end-stop learning) |
| `MtrCtrl_CM` | Motor Control, Current Mode |
| `MtrTempEst` | Motor Temperature Estimation |
| `MtrVel_Digi` | Motor Velocity, Digital computation |
| `NvMProxy` | Non-Volatile Memory Proxy |
| `OvrVoltMon` | Over-Voltage Monitor |
| `PSASH` | PSA APA Steering Handler (park-assist interface) * |
| `PSATA` | PSA Torque Arbitrator |
| `Polarity` | Signal Polarity alignment |
| `PosServo` | Position Tracking Servo |
| `PwrLmtFuncCr` | Power Limit Function, Current Mode |
| `Return` | Return to Centre |
| `ReturnFirewall` | Return-path safety firewall |
| `SF46_GCCDiag_Implementation` | SF46 Gross Cross Check Diagnostics |
| `SgnlCond` | Signal Conditioning |
| `ShtdnMech` | Shutdown Mechanisms |
| `StOpCtrl` | State Output Control |
| `StaMd` | States and Modes management |
| `StabilityComp` | Stability Compensation |
| `SwProject/ChkPt` | Watchdog Checkpoints |
| `SwProject/CustBattDiag` | Customer Battery Diagnostics (PSA) |
| `SwProject/DfltConfigData` | Default Configuration Data |
| `SwProject/VehPwrMd` | Vehicle Power Mode management |
| `Sweep` | Frequency Sweep test function |
| `ThrmDutyCycle` | Thermal Duty Cycle derating |
| `TqRsDg` | Torque Reasonableness Diagnostics |
| `TuningSelAuth` | Tuning Select Authority |
| `VehDyn` | Vehicle Dynamics input processing |
| `VehSpdLmt` | Vehicle Speed Limiting function |
| `Xcp` | Universal Measurement and Calibration Protocol (XCP) |

## Complex Device Drivers (CDD)

| Module | Full name |
| --- | --- |
| `DigHwTrqSENT` | Digital Handwheel Torque over SENT |
| `DigMSB` | Digital Motor Sensor Board interface * |
| `SVDiag` | Space Vector Drive Diagnostics (gate-drive / phase faults) |
| `SVDrvr_CM` | Space Vector PWM Driver, Current Mode |
| `SpiNxt` | Serial Peripheral Interface handler, Nexteer |
| `SwProject/CDDInterface` | Complex Driver Interface (application ↔ driver bridge) |
| `SwProject/SrlComDriver` | Serial Communication Driver |
| `SwProject/SrlComInput` | Serial Communication Input |
| `SwProject/SrlComOutput` | Serial Communication Output |
| `TMS570_uDiag` | TMS570 Micro Diagnostics (self-tests) |
| `TmprlMon` | Temporal Monitor (execution timing supervision) |
| `ePWM` | Enhanced PWM / NHET driver |

## BSW Services

| Module | Full name |
| --- | --- |
| `DiagMgr` | Diagnostics Manager |
| `GliwaT1` | Gliwa T1 timing executive |
| `NvMMgr` | Non-Volatile Memory Manager (Fee interface) |
| `SwProject/DemIf` | Diagnostic Event Manager Interface |
| `SwProject/DiagSvc` | Diagnostic Services (UDS) |
| `SwProject/FaultLog` | Fault Log storage |
| `bsw-stack` | AUTOSAR Basic Software stack (Vector MICROSAR) |

## ECU Abstraction

| Module | Full name |
| --- | --- |
| `Adc` | Analog-to-Digital Converter driver |
| `SwProject/IoHwAbstractionUsr` | Input/Output Hardware Abstraction, user layer |

## MCAL & MCU Drivers

| Module | Full name |
| --- | --- |
| `Dma` | Direct Memory Access driver |
| `Fee` | Flash EEPROM Emulation (AUTOSAR memory stack) |
| `Fls` | Flash Driver (TI F021 Flash API) |
| `TMS570_Startup` | TMS570 Startup Code (reset, clocks, vectors) |

## Libraries & Shared Code

| Module | Full name |
| --- | --- |
| `CMS_Common` | CMS common files (diagnostic services; CMS = generator tag, expansion not stated *) |
| `NxtrLib` | Nexteer math Library (filters, fixed-point) |
| `StdDef` | Standard Definitions (AUTOSAR platform/compiler types) |
| `SwProject/CMS_PSA` | CMS PSA files (diagnostic services; CMS = generator tag, expansion not stated *) |
| `SwProject/Header` | Project integration headers |
| `SwProject/NtWrap` | Non-Trusted RTE call Wrapper |

## Project Integration

| Module | Full name |
| --- | --- |
| `PSA_BMPV_EPS_TMS570` | PSA BMPV EPS ECU project (TMS570) |
| `hldd` | High-Level Design documents (Vector Technical References) |
| `rte-gendata` | Generated RTE/BSW configuration (GenData) |

## Notes on inferred (*) expansions

- **Gsod → Global Signal Overwrite Detection**: `Ap_Gsod` raises `*_OverwriteFlt` flags for handwheel torque, motor position and torque command when a global signal disagrees with its redundantly stored copy (see the converted Gsod MDD).
- **PSASH → PSA APA Steering Handler**: `Ap_PSASH` reads `ApaEna`, `ApaCmdReq`, `ApaAuthn`, `ApaRelaxReq` and `HandwheelAuthority` ports — i.e. it is the automated park-assist (APA) steering interface. Sibling module PSATA is documented as the “PSA Torque Arbitrator”.
- **DigMSB → Digital Motor Sensor Board**: the digital rotor-position sensor interface; MSB is the project term for the motor sensor board.
- **CmMtrCurr → Common-Mode Motor Current**: phase-current measurement via shunt resistors and differential amplifiers (see the converted CmMtrCurr MDD).
- **CMS (CMS_Common, CMS_PSA)**: tag found in `BEGIN CMS GENERATION` file banners — the generator that produces the `EPS_DiagSrvcs_*` diagnostic-service files. No source states what CMS abbreviates, so it is left unexpanded.
