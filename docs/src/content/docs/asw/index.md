---
title: 'Application Software (ASW)'
description: 'AUTOSAR application software components (Ap_ SW-Cs): steering functions, diagnostics helpers,dw state management and PSA-specific features.'
sidebar: { order: 0 }
---

# Application Software (ASW)

AUTOSAR application software components (Ap_ SW-Cs): steering functions, diagnostics helpers,dw state management and PSA-specific features.

## Modules in this layer

| Module | Component | Summary |
| --- | --- | --- |
| [AbsHwPos_TcI2cVd](./abshwpos_tci2cvd/) | Ap_AbsHwPos | Absolute handwheel-position sensing over a TCI2C vehicle-dynamics interface; conditions and plausibilises the  |
| [ActivePull](./activepull/) | Ap_ActivePull | Active-pull compensation: learns and counteracts vehicle pull/drift by adding a corrective torque overlay. |
| [Assist](./assist/) | Ap_Assist | Core power-assist function: computes the base assist torque command from handwheel torque and vehicle speed. |
| [AssistFirewall](./assistfirewall/) | Ap_AssistFirewall | Safety firewall that limits and plausibilises the assist torque command before it reaches the motor control. |
| [AstLmt_CM](./astlmt_cm/) | Ap_AstLmt | Assist summation and current-mode limiter: arbitrates torque contributions and enforces current limits. |
| [AvgFricLrn](./avgfriclrn/) | Ap_AvgFricLrn | Average-friction learning: estimates column/road friction over time to adapt compensation. |
| [BVDiag](./bvdiag/) | Ap_BVDiag | Battery-voltage diagnostics: monitors supply rails and reports under/over-voltage conditions. |
| [BatteryVoltage](./batteryvoltage/) | Ap_BatteryVoltage | Battery-voltage acquisition and conditioning for supply-dependent scaling and diagnostics. |
| [BkCpPc](./bkcppc/) | Sa_BkCpPc | Bulk-capacitor precharge control: sequences and supervises precharge of the inverter bulk capacitor. |
| [CmMtrCurr](./cmmtrcurr/) | Sa_CmMtrCurr | Common-mode motor-current processing used by current measurement and diagnostics. |
| [ComplErr](./complerr/) | Ap_ComplErr | Compliance-error monitor: detects excessive deviation between commanded and achieved states. |
| [CtrlTemp](./ctrltemp/) | Sa_CtrlTemp | Controller-temperature acquisition and derating input for thermal protection. |
| [CtrldDisShtdn](./ctrlddisshtdn/) | Ap_CtrldDisShtdn | Controlled-disable and shutdown sequencing: brings the EPS to a safe state on faults or power-down. |
| [Damping](./damping/) | Ap_Damping | Damping compensation: adds speed-dependent damping torque for stability and steering feel. |
| [DampingFirewall](./dampingfirewall/) | Ap_DampingFirewall | Safety firewall for the damping torque path. |
| [EOTActuatorMng](./eotactuatormng/) | Ap_EOTActuatorMng | End-of-travel actuator management: soft end-stop behavior near rack travel limits. |
| [ElePwr](./elepwr/) | Ap_ElePwr | Electric-power-consumption estimation for energy management and load monitoring. |
| [EtDmpFw](./etdmpfw/) | Ap_EtDmpFw | End-of-travel damping firewall: bounds damping action inside the end-of-travel region. |
| [FltInjection](./fltinjection/) | Ap_FltInjection | Fault-injection SW-C for safety validation: injects controlled faults during HIL/test builds. |
| [FrqDepDmpnInrtCmp](./frqdepdmpninrtcmp/) | Ap_FrqDepDmpnInrtCmp | Frequency-dependent damping and inertia compensation for steering feel across the vibration spectrum. |
| [Gsod](./gsod/) | Ap_Gsod | Generic shut-off and degradation (GSOD) handling for fault-induced operating-mode reduction. |
| [HiLoadStall](./hiloadstall/) | Ap_HiLoadStall | High-load/stall protection: limits motor effort during sustained stall to protect hardware. |
| [HighFreqAssist](./highfreqassist/) | Ap_HighFreqAssist | High-frequency assist shaping for NVH-relevant steering response. |
| [HwPwUp](./hwpwup/) | Ap_HwPwUp | Hardware power-up sequencing and initialisation of supplies and peripherals. |
| [HystComp](./hystcomp/) | Ap_HystComp | Hysteresis compensation for column friction feel around centre. |
| [LmtCod](./lmtcod/) | Ap_LmtCod | Limiter conditioning: pre-conditions torque/current requests before limit enforcement. |
| [LrnEOT](./lrneot/) | Ap_LrnEOT | Learned end-of-travel: learns mechanical rack end-stops during operation. |
| [MtrCtrl_CM](./mtrctrl_cm/) | Ap_CurrCmd, Ap_CurrParamComp, Ap_PICurrCntrl, Ap_PeakCurrEst, Ap_QuadDet, Ap_TrqCanc, Ap_TrqCmdScl, Ap_MtrCtrl | Motor control in current mode: current command, PI current control, torque scaling, quadrant detection and can |
| [MtrTempEst](./mtrtempest/) | Ap_MtrTempEst | Motor-temperature estimation model feeding thermal protection. |
| [MtrVel_Digi](./mtrvel_digi/) | Sa_MtrVel, Sa_MtrVel2, Sa_MtrVel3 | Digital motor-velocity computation from position-sensor signals. |
| [NvMProxy](./nvmproxy/) | Cd_NvMProxy | NVRAM proxy SW-C exposing simplified NVRAM services to application components. |
| [OvrVoltMon](./ovrvoltmon/) | Sa_OvrVoltMon | Over-voltage monitor with shutdown interlock for load-dump protection. |
| [PSASH](./psash/) | Ap_PSASH | PSA-specific steering-angle handling (PSASH) SW-C for the BMPV platform interface. |
| [PSATA](./psata/) | Ap_PSATA | PSA-specific torque-angle/turn-signal adaptation (PSATA) SW-C for the BMPV platform interface. |
| [Polarity](./polarity/) | Ap_Polarity | Polarity management: aligns sensor/actuator signs across build variants. |
| [PosServo](./posservo/) | Ap_PosServo | Position-servo control used for service/return-to-centre positioning functions. |
| [PwrLmtFuncCr](./pwrlmtfunccr/) | Ap_PwrLmtFuncCr | Power-limit function (current mode): derates assist under electrical/thermal power constraints. |
| [Return](./return/) | Ap_Return | Return-to-centre function: generates torque guiding the wheel back to centre. |
| [ReturnFirewall](./returnfirewall/) | Ap_ReturnFirewall | Safety firewall for the return torque path. |
| [SF46_GCCDiag_Implementation](./sf46_gccdiag_implementation/) | Ap_GCCDiag | GCC-level diagnostics implementation for the SF46 safety concept. |
| [SgnlCond](./sgnlcond/) | Ap_SignlCondn | Signal conditioning for sensor inputs (filtering, scaling, plausibility). |
| [ShtdnMech](./shtdnmech/) | Sa_ShtdnMech | Shutdown mechanisms: hardware/software paths that force a safe (de-energised) state. |
| [StOpCtrl](./stopctrl/) | Ap_StOpCtrl | State-output control: gates function outputs by operating state. |
| [StaMd](./stamd/) | Ap_StaMd | State and mode management: EPS operating states/modes and transitions. |
| [StabilityComp](./stabilitycomp/) | Ap_StabilityComp, Ap_StabilityComp2 | Stability compensation shaping of the torque loop for robustness. |
| [SwProject/ChkPt](./swproject-chkpt/) | Ap_ChkPtAp10, Ap_ChkPtAp11, Ap_ChkPtAp6, Ap_ChkPtAp9 | Watchdog-checkpoint SW-Cs (one per application partition) for alive supervision. |
| [SwProject/CustBattDiag](./swproject-custbattdiag/) | Ap_CustBattDiag | Customer (PSA) battery diagnostic SW-C for platform-specific supply monitoring. |
| [SwProject/DfltConfigData](./swproject-dfltconfigdata/) | Ap_DfltConfigData | Default configuration/calibration data set flashed when NVRAM is invalid. |
| [SwProject/VehPwrMd](./swproject-vehpwrmd/) | Ap_VehPwrMd | Vehicle power-mode management (wake/sleep, KL15 handling). |
| [Sweep](./sweep/) | Ap_Sweep, Ap_Sweep2 | Sweep (frequency-sweep) test function for validation and characterisation. |
| [ThrmDutyCycle](./thrmdutycycle/) | Ap_ThrmlDutyCycle | Thermal duty-cycle derating: reduces assist duty as controller/motor temperature rises. |
| [TqRsDg](./tqrsdg/) | Ap_TqRsDg | Torque reasonableness diagnostics: plausibility of measured vs expected handwheel torque. |
| [TuningSelAuth](./tuningselauth/) | Ap_TuningSelAuth | Tuning-select authority: arbitrates which calibration/tuning set is active. |
| [VehDyn](./vehdyn/) | Ap_VehDyn | Vehicle-dynamics input processing for stability-relevant EPS functions. |
| [VehSpdLmt](./vehspdlmt/) | Ap_VehSpdLmt | Vehicle-speed limiter interface influencing speed-dependent assist. |
| [Xcp](./xcp/) | Ap_ApXcp | Application-side XCP (Ap_ApXcp): measurement/calibration access to application variables. |
