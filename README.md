# Electric Power Steering (EPS) System for PSA BMPV (Stellantis)

[![Docs build](../../actions/workflows/deploy.yml/badge.svg)](../../actions/workflows/deploy.yml)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
![Language](https://img.shields.io/badge/language-C-blue.svg)
![Platform](https://img.shields.io/badge/platform-TI%20TMS570-red.svg)
![Standard](https://img.shields.io/badge/AUTOSAR-Classic-orange.svg)
![Safety](https://img.shields.io/badge/safety-ASIL--D-critical.svg)

An AUTOSAR-based **Electric Power Steering (EPS)** system for the **PSA BMPV**
platform (now part of Stellantis), running on a **TI TMS570** microcontroller
and developed to **ISO 26262 ASIL-D**.

> **Documentation site:** the full module documentation (Astro v7 + Starlight,
> built from Word/PDF design documents and the sources) is published via
> GitHub Pages — see [.github/workflows/deploy.yml](.github/workflows/deploy.yml)
> and the [`docs/`](docs/) folder. Enable it under *Settings > Pages > Source:
> GitHub Actions*.

## Table of contents

- [Features](#features)
- [Repository structure](#repository-structure)
- [AUTOSAR layers](#autosar-layers)
- [Module inventory](#module-inventory)
- [Vector vs. custom code](#vector-vs-custom-code)
- [Build instructions](#build-instructions)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Key components**:
  - **TMS570**: the microcontroller used for EPS control.
  - **AUTOSAR**: the software development standard for automotive embedded systems.
  - **ISO 26262 ASIL-D**: the functional safety standard for automotive systems.
  - **CAN**: Controller Area Network, a communication protocol for automotive systems.
  - **UDS**: on-board diagnostics protocol.
- **Functionality**:
  - Precise power-assisted steering control.
  - Electric motor power management.

<details>
<summary><strong>PSA BMPV platform vehicles</strong></summary>

The **PSA BMPV** platform, now part of Stellantis, is an advanced electronic
architecture for vehicles produced by PSA Group (Peugeot, Citroën, DS Automobiles)
and now Stellantis. Examples of vehicles based on the BMPV platform:

1. **Citroën C3** · 2. **Citroën C3 Aircross** · 3. **Opel Crossland**
2. **Peugeot 2008** · 5. **Opel Corsa** · 6. **Vauxhall Corsa** · 7. **Citroën Berlingo**

</details>

## Repository structure

```text
<repo root>/
├── Assist/  Damping/  StaMd/  …        # ~60 application SW-C modules (Ap_*)
├── DigMSB/  SpiNxt/  ePWM/  …          # complex device drivers (Sa_*/Cd_*)
├── Adc/  Dma/  Fee/  Fls/              # ECU abstraction / MCAL drivers
├── NxtrLib/  StdDef/  CMS_Common/      # shared libraries
├── DiagMgr/  NvMMgr/  TmprlMon/  Xcp/  # services-side managers
├── GliwaT1/                            # third-party timing executive
├── TMS570_Startup/                     # MCU startup code
├── PSASH/  PSATA/                      # PSA platform adaptation SW-Cs
├── PSA_BMPV_EPS_TMS570/                # ECU project integration
│   ├── HLDD/                           # Vector high-level design references
│   └── SwProject/
│       ├── Source/                     # BSW stack, RTE/GenData, CDD glue, CCS project
│       ├── SrlCom{Driver,Input,Output}/# PSA serial communication
│       ├── DemIf/ DiagSvc/ FaultLog/ … # services wrappers
│       └── Tools/                      # host tooling (QAC, Polyspace, metrics…)
├── docs/                               # documentation site (Astro v7 + Starlight)
│   ├── astro.config.mjs                # site/base auto-derived from git remote
│   ├── package.json
│   └── src/content/docs/               # asw/ cdd/ services/ ecuab/ mcal/ …
├── .github/workflows/                  # Pages deploy + Dependabot auto-merge
├── LICENSE                             # MIT
└── README.md
```

Each module typically contains `src/`, `include/`, `autosar/` (DaVinci model),
`generate/` (generator inputs), `tools/`, `utp/` (TESSY contracts) and `doc/`
(design documents).

## AUTOSAR layers

| Layer | Content | Docs |
| --- | --- | --- |
| Application Software (ASW) | `Ap_*` steering functions, diagnostics, PSA features | `docs/src/content/docs/asw/` |
| Complex Device Drivers (CDD) | `Sa_*/Cd_*` sensor & actuator drivers, SrlCom | `docs/src/content/docs/cdd/` |
| BSW Services | DiagMgr, NvMMgr, DemIf, GliwaT1, Vector BSW stack | `docs/src/content/docs/services/` |
| ECU Abstraction | Adc, IoHwAbstractionUsr | `docs/src/content/docs/ecuab/` |
| MCAL & MCU | Dma, Fee, Fls, TMS570 startup | `docs/src/content/docs/mcal/` |
| Libraries | NxtrLib, StdDef, CMS helpers, NtWrap | `docs/src/content/docs/syslib/` |
| Integration | RTE/GenData, BSW sources, HLDD references | `docs/src/content/docs/integration/` |

## Module inventory

In-house developed components and externally provided components are listed
separately. The component column shows the AUTOSAR software-component / driver
name used in the code (`Ap_*`, `Sa_*`, `Cd_*`, …); Vector artefacts are marked
`AUTOSAR`. Full per-module documentation — including the origin of every
module — is on the documentation site.

<details>
<summary><strong>In-house components (click to expand)</strong></summary>

| Module | Full name | Layer | Software component |
| --- | --- | --- | --- |
| `AbsHwPos_TcI2cVd` | Absolute Handwheel Position – Turns counter, I2C, Vehicle Dynamics | Application Software | `Ap_AbsHwPos` |
| `ActivePull` | Active Pull Compensation | Application Software | `Ap_ActivePull` |
| `Adc` | Analog-to-Digital Converter driver | ECU Abstraction | `Adc, Adc2` |
| `Assist` | Power Steering Assist (base assist) | Application Software | `Ap_Assist` |
| `AssistFirewall` | Assist-path safety firewall | Application Software | `Ap_AssistFirewall` |
| `AstLmt_CM` | Assist Sum and Limit, Current Mode | Application Software | `Ap_AstLmt` |
| `AvgFricLrn` | Average Friction Learning | Application Software | `Ap_AvgFricLrn` |
| `BatteryVoltage` | Battery Voltage acquisition | Application Software | `Ap_BatteryVoltage` |
| `BkCpPc` | Bulk Capacitor Precharge | Application Software | `Sa_BkCpPc` |
| `BVDiag` | Battery Voltage Diagnostics | Application Software | `Ap_BVDiag` |
| `CmMtrCurr` | Common-Mode Motor Current measurement | Application Software | `Sa_CmMtrCurr` |
| `CMS_Common` | CMS common files (diagnostic services; CMS = generator tag, expansion not stated) | Libraries & Shared Code | `EPS_DiagSrvcs` |
| `ComplErr` | Compliance Error monitor | Application Software | `Ap_ComplErr` |
| `CtrldDisShtdn` | Controlled Disable Shutdown | Application Software | `Ap_CtrldDisShtdn` |
| `CtrlTemp` | Controller Temperature | Application Software | `Sa_CtrlTemp` |
| `Damping` | Damping Compensation | Application Software | `Ap_Damping` |
| `DampingFirewall` | Damping-path safety firewall | Application Software | `Ap_DampingFirewall` |
| `DiagMgr` | Diagnostics Manager | BSW Services | `Ap_DiagMgr` |
| `DigHwTrqSENT` | Digital Handwheel Torque over SENT | Complex Device Drivers | `Sa_DigHwTrqSENT` |
| `DigMSB` | Digital Motor Sensor Board interface | Complex Device Drivers | `Sa_DigMSB` |
| `Dma` | Direct Memory Access driver | MCAL & MCU Drivers | `Dma` |
| `ElePwr` | Electric Power Consumption estimation | Application Software | `Ap_ElePwr` |
| `EOTActuatorMng` | End of Travel Actuator Management | Application Software | `Ap_EOTActuatorMng` |
| `ePWM` | Enhanced PWM / NHET driver | Complex Device Drivers | `Ap_ePWM2, Cd_Nhet1` |
| `EtDmpFw` | End of Travel Damping Firewall | Application Software | `Ap_EtDmpFw` |
| `FltInjection` | Fault Injection (safety validation) | Application Software | `Ap_FltInjection` |
| `FrqDepDmpnInrtCmp` | Frequency Dependent Damping and Inertia Compensation | Application Software | `Ap_FrqDepDmpnInrtCmp` |
| `Gsod` | Global Signal Overwrite Detection | Application Software | `Ap_Gsod` |
| `HighFreqAssist` | High Frequency Assist | Application Software | `Ap_HighFreqAssist` |
| `HiLoadStall` | High Load Stall protection | Application Software | `Ap_HiLoadStall` |
| `HwPwUp` | Hardware Power-Up sequencing | Application Software | `Ap_HwPwUp` |
| `HystComp` | Hysteresis Compensation | Application Software | `Ap_HystComp` |
| `LmtCod` | Limiter Conditioning | Application Software | `Ap_LmtCod` |
| `LrnEOT` | Learn End Of Travel (end-stop learning) | Application Software | `Ap_LrnEOT` |
| `MtrCtrl_CM` | Motor Control, Current Mode | Application Software | `Ap_CurrCmd, Ap_CurrParamComp, Ap_PICurrCntrl, Ap_PeakCurrEst, Ap_QuadDet, Ap_TrqCanc, Ap_TrqCmdScl, Ap_MtrCtrl` |
| `MtrTempEst` | Motor Temperature Estimation | Application Software | `Ap_MtrTempEst` |
| `MtrVel_Digi` | Motor Velocity, Digital computation | Application Software | `Sa_MtrVel, Sa_MtrVel2, Sa_MtrVel3` |
| `NvMMgr` | Non-Volatile Memory Manager (Fee interface) | BSW Services | `Cd_FeeIf` |
| `NvMProxy` | Non-Volatile Memory Proxy | Application Software | `Cd_NvMProxy` |
| `NxtrLib` | Nexteer math Library (filters, fixed-point) | Libraries & Shared Code | `NxtrLib` |
| `OvrVoltMon` | Over-Voltage Monitor | Application Software | `Sa_OvrVoltMon` |
| `Polarity` | Signal Polarity alignment | Application Software | `Ap_Polarity` |
| `PosServo` | Position Tracking Servo | Application Software | `Ap_PosServo` |
| `PSA_BMPV_EPS_TMS570` | PSA BMPV EPS ECU project (TMS570) | Project Integration | — |
| `PSASH` | PSA APA Steering Handler (park-assist interface) | Application Software | `Ap_PSASH` |
| `PSATA` | PSA Torque Arbitrator | Application Software | `Ap_PSATA` |
| `PwrLmtFuncCr` | Power Limit Function, Current Mode | Application Software | `Ap_PwrLmtFuncCr` |
| `Return` | Return to Centre | Application Software | `Ap_Return` |
| `ReturnFirewall` | Return-path safety firewall | Application Software | `Ap_ReturnFirewall` |
| `SF46_GCCDiag_Implementation` | SF46 Gross Cross Check Diagnostics | Application Software | `Ap_GCCDiag` |
| `SgnlCond` | Signal Conditioning | Application Software | `Ap_SignlCondn` |
| `ShtdnMech` | Shutdown Mechanisms | Application Software | `Sa_ShtdnMech` |
| `SpiNxt` | Serial Peripheral Interface handler, Nexteer | Complex Device Drivers | `SpiNxt` |
| `StabilityComp` | Stability Compensation | Application Software | `Ap_StabilityComp, Ap_StabilityComp2` |
| `StaMd` | States and Modes management | Application Software | `Ap_StaMd` |
| `StdDef` | Standard Definitions (AUTOSAR platform/compiler types) | Libraries & Shared Code | `StdDef` |
| `StOpCtrl` | State Output Control | Application Software | `Ap_StOpCtrl` |
| `SVDiag` | Space Vector Drive Diagnostics (gate-drive / phase faults) | Complex Device Drivers | `Ap_DigPhsReasDiag, Sa_MtrDrvDiag` |
| `SVDrvr_CM` | Space Vector PWM Driver, Current Mode | Complex Device Drivers | `PwmCdd` |
| `Sweep` | Frequency Sweep test function | Application Software | `Ap_Sweep, Ap_Sweep2` |
| `SwProject/CDDInterface` | Complex Driver Interface (application ↔ driver bridge) | Complex Device Drivers | `Sa_CDDInterface10, Sa_CDDInterface11, Sa_CDDInterface6, Sa_CDDInterface9` |
| `SwProject/ChkPt` | Watchdog Checkpoints | Application Software | `Ap_ChkPtAp10, Ap_ChkPtAp11, Ap_ChkPtAp6, Ap_ChkPtAp9` |
| `SwProject/CustBattDiag` | Customer Battery Diagnostics (PSA) | Application Software | `Ap_CustBattDiag` |
| `SwProject/DemIf` | Diagnostic Event Manager Interface | BSW Services | `Ap_DemIf` |
| `SwProject/DfltConfigData` | Default Configuration Data | Application Software | `Ap_DfltConfigData` |
| `SwProject/DiagSvc` | Diagnostic Services (UDS) | BSW Services | `Ap_DiagSvc` |
| `SwProject/FaultLog` | Fault Log storage | BSW Services | `Ap_FaultLog` |
| `SwProject/Header` | Project integration headers | Libraries & Shared Code | — |
| `SwProject/IoHwAbstractionUsr` | Input/Output Hardware Abstraction, user layer | ECU Abstraction | `IoHwAb9, IoHwAb10` |
| `SwProject/NtWrap` | Non-Trusted RTE call Wrapper | Libraries & Shared Code | `NtWrap` |
| `SwProject/Source` | ECU source integration (BSW, RTE, CDD glue) | Project Integration | `— (integration sources: BSW, RTE, CDD glue)` |
| `SwProject/VehPwrMd` | Vehicle Power Mode management | Application Software | `Ap_VehPwrMd` |
| `ThrmDutyCycle` | Thermal Duty Cycle derating | Application Software | `Ap_ThrmlDutyCycle` |
| `TmprlMon` | Temporal Monitor (execution timing supervision) | Complex Device Drivers | `Sa_TmprlMon, Sa_TmprlMon2` |
| `TMS570_uDiag` | TMS570 Micro Diagnostics (self-tests) | Complex Device Drivers | `Cd_uDiagCCRM, Cd_uDiagClockMonitor, Cd_uDiagECC, Cd_uDiagESM, Cd_uDiagFPU, Cd_uDiagIOMM, Cd_uDiagLossOfExec, Cd_uDiagParity, Cd_uDiagPeriphMPU, Cd_uDiagResetHandler, Cd_uDiagStaticRegs, Cd_uDiagVIM, Cd_uDiagUtility` |
| `TqRsDg` | Torque Reasonableness Diagnostics | Application Software | `Ap_TqRsDg` |
| `TuningSelAuth` | Tuning Select Authority | Application Software | `Ap_TuningSelAuth` |
| `VehDyn` | Vehicle Dynamics input processing | Application Software | `Ap_VehDyn` |
| `VehSpdLmt` | Vehicle Speed Limiting function | Application Software | `Ap_VehSpdLmt` |
| `Xcp` | Universal Measurement and Calibration Protocol (XCP) | Application Software | `Ap_ApXcp` |

</details>

<details>
<summary><strong>External components — Vector, TI, Gliwa (click to expand)</strong></summary>

| Module / path | Layer | Component | Provider |
| --- | --- | --- | --- |
| `PSA_BMPV_EPS_TMS570/SwProject/Source/BSW` | BSW Services + MCAL | `AUTOSAR Can, Il, Tp, Nm, EcuM, Dem, Det, NvM, MemIf, Crc, Dio, Port, Mcu, Gpt, WdgM, Xcp, VStdLib` | Vector MICROSAR |
| `PSA_BMPV_EPS_TMS570/HLDD` | Project Integration | `AUTOSAR Technical References` | Vector |
| `PSA_BMPV_EPS_TMS570/SwProject/Source/GenData*` | Project Integration | `AUTOSAR GenData / GenDataRte / GenDataOS (customised)` | Vector (generated, PSA-configured) |
| `SwProject/SrlComDriver` | Complex Device Drivers | `AUTOSAR Cd_SrlComDriver (customised)` | Vector base, PSA-customised |
| `SwProject/SrlComInput` | Complex Device Drivers | `AUTOSAR Ap_SrlComInput (customised)` | Vector base, PSA-customised |
| `SwProject/SrlComOutput` | Complex Device Drivers | `AUTOSAR Ap_SrlComOutput (customised)` | Vector base, PSA-customised |
| `SwProject/CMS_PSA` | Libraries & Shared Code | `AUTOSAR EPS_DiagSrvcs_* (customised)` | Vector base, PSA-customised |
| `Fee` | MCAL & MCU Drivers | `AUTOSAR Fee` (TI F021) | Texas Instruments |
| `Fls` | MCAL & MCU Drivers | `Fls` (F021 Flash API) | Texas Instruments |
| `TMS570_Startup` | MCAL & MCU Drivers | `TMS570 startup code` (HALCoGen-based) | Texas Instruments (adapted in-house) |
| `GliwaT1` | BSW Services | `T1` executive | Gliwa |

The Vector MICROSAR BSW itself is **Vector-provided, do not modify** — configure
it via DaVinci/GENy and regenerate. See the
[BSW stack page](docs/src/content/docs/services/bsw-stack.md) of the docs site.

</details>

<details>
<summary><strong>External components — Vector, TI, Gliwa (click to expand)</strong></summary>

| Module / path | Layer | Component | Provider |
| --- | --- | --- | --- |
| `PSA_BMPV_EPS_TMS570/SwProject/Source/BSW` | BSW Services + MCAL | `AUTOSAR Can, Il, Tp, Nm, EcuM, Dem, Det, NvM, MemIf, Crc, Dio, Port, Mcu, Gpt, WdgM, Xcp, VStdLib` | Vector MICROSAR |
| `PSA_BMPV_EPS_TMS570/HLDD` | Project Integration | `AUTOSAR Technical References` | Vector |
| `PSA_BMPV_EPS_TMS570/SwProject/Source/GenData*` | Project Integration | `AUTOSAR GenData / GenDataRte / GenDataOS (customised)` | Vector (generated, PSA-configured) |
| `SwProject/SrlComDriver` | Complex Device Drivers | `AUTOSAR Cd_SrlComDriver (customised)` | Vector base, PSA-customised |
| `SwProject/SrlComInput` | Complex Device Drivers | `AUTOSAR Ap_SrlComInput (customised)` | Vector base, PSA-customised |
| `SwProject/SrlComOutput` | Complex Device Drivers | `AUTOSAR Ap_SrlComOutput (customised)` | Vector base, PSA-customised |
| `SwProject/CMS_PSA` | Libraries & Shared Code | `AUTOSAR EPS_DiagSrvcs_* (customised)` | Vector base, PSA-customised |
| `Fee` | MCAL & MCU Drivers | `AUTOSAR Fee` (TI F021) | Texas Instruments |
| `Fls` | MCAL & MCU Drivers | `Fls` (F021 Flash API) | Texas Instruments |
| `TMS570_Startup` | MCAL & MCU Drivers | `TMS570 startup code` (HALCoGen-based) | Texas Instruments (adapted in-house) |
| `GliwaT1` | BSW Services | `T1` executive | Gliwa |

The Vector MICROSAR BSW itself is **Vector-provided, do not modify** — configure
it via DaVinci/GENy and regenerate. See the
[BSW stack page](docs/src/content/docs/services/bsw-stack.md) of the docs site.

</details>

<details>
<summary><strong>External components — Vector, TI, Gliwa (click to expand)</strong></summary>

| Module / path | Layer | Component | Provider |
| --- | --- | --- | --- |
| `PSA_BMPV_EPS_TMS570/SwProject/Source/BSW` | BSW Services + MCAL | `AUTOSAR Can, Il, Tp, Nm, EcuM, Dem, Det, NvM, MemIf, Crc, Dio, Port, Mcu, Gpt, WdgM, Xcp, VStdLib` | Vector MICROSAR |
| `PSA_BMPV_EPS_TMS570/HLDD` | Project Integration | `AUTOSAR Technical References` | Vector |
| `PSA_BMPV_EPS_TMS570/SwProject/Source/GenData*` | Project Integration | `AUTOSAR GenData / GenDataRte / GenDataOS (customised)` | Vector (generated, PSA-configured) |
| `SwProject/SrlComDriver` | Complex Device Drivers | `AUTOSAR Cd_SrlComDriver (customised)` | Vector base, PSA-customised |
| `SwProject/SrlComInput` | Complex Device Drivers | `AUTOSAR Ap_SrlComInput (customised)` | Vector base, PSA-customised |
| `SwProject/SrlComOutput` | Complex Device Drivers | `AUTOSAR Ap_SrlComOutput (customised)` | Vector base, PSA-customised |
| `SwProject/CMS_PSA` | Libraries & Shared Code | `AUTOSAR EPS_DiagSrvcs_* (customised)` | Vector base, PSA-customised |
| `Fee` | MCAL & MCU Drivers | `AUTOSAR Fee` (TI F021) | Texas Instruments |
| `Fls` | MCAL & MCU Drivers | `Fls` (F021 Flash API) | Texas Instruments |
| `TMS570_Startup` | MCAL & MCU Drivers | `TMS570 startup code` (HALCoGen-based) | Texas Instruments (adapted in-house) |
| `GliwaT1` | BSW Services | `T1` executive | Gliwa |

The Vector MICROSAR BSW itself is **Vector-provided, do not modify** — configure
it via DaVinci/GENy and regenerate. See the
[BSW stack page](docs/src/content/docs/services/bsw-stack.md) of the docs site.

</details>

## Vector vs. custom code

- **Custom**: application SW-Cs, CDDs, wrappers and libraries developed by the
  EPS team (RTE scaffolding inside them is generator output — edit logic, not
  scaffolding).
- **Vector-provided**: `SwProject/Source/BSW/*` and `HLDD/` Technical
  References — configure via DaVinci/GENy, never hand-edit.
- **Vector-provided, customised**: generated RTE/BSW configuration
  (`GenData*`), `SrlCom*`, `CMS_PSA` — regenerate from models.
- **Third-party**: `Fee`/`Fls` (TI Flash), `TMS570_Startup` (TI HALCoGen-based),
  `GliwaT1` (Gliwa) — keep vendor files pristine.

Details: [`docs/src/content/docs/general/origin-guide.md`](docs/src/content/docs/general/origin-guide.md).

## Build instructions

### Firmware (TI TMS570)

1. Install **TI Code Composer Studio** with the ARM/Cortex-R toolchain.
2. Open `PSA_BMPV_EPS_TMS570/SwProject/.ccsproject`.
3. Run the DaVinci/GENy generation step to refresh `Source/GenData*`
   (per-module `generate/*_Generate.bat` launchers).
4. Build the CCS project (big-endian Cortex-R4; links the prebuilt
   `Fls/src/F021_API_CortexR4_BE_V3D16.lib`).
5. Flash the image plus default calibration (`SwProject/DfltConfigData`).

More detail: [`docs/src/content/docs/general/build-system.md`](docs/src/content/docs/general/build-system.md).

### Documentation site

Requirements: Node.js 22.12 or later (Astro v7 requires a recent Node —
see `docs/.nvmrc` and the `engines` field in `docs/package.json`).

```sh
cd docs
npm install
npm run build   # output in docs/dist/
npm run dev     # local preview
```

Deployment to GitHub Pages is automated by
[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) on pushes to the
default branch. The Astro `site`/`base` URLs are derived from the git `origin`
remote at build time, so forks work without configuration changes.

## Documentation

- Start at the docs landing page (`docs/src/content/docs/index.md`, deployed to
  GitHub Pages).
- [AUTOSAR overview](docs/src/content/docs/general/autosar-overview.md) ·
  [Build system](docs/src/content/docs/general/build-system.md) ·
  [Safety (ASIL-D)](docs/src/content/docs/general/safety.md) ·
  [Glossary](docs/src/content/docs/general/glossary.md) ·
  [Module names](docs/src/content/docs/general/module-names.md) ·
  [Conversion notes](docs/src/content/docs/general/conversion-notes.md).
- Converted Word/PDF design documents: `docs/src/content/docs/modules/`,
  linked from every module page.

## Contributing

We encourage contributions! If you'd like to improve this project, please submit a pull request.

## License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file.
Third-party vendor components (Vector MICROSAR, TI Flash/HALCoGen, Gliwa T1)
remain subject to their own license terms; see the note in [LICENSE](LICENSE)
and the [origin guide](docs/src/content/docs/general/origin-guide.md).
