---
title: EPS TMS570 PSA BMPV Documentation
description: Technical documentation for the AUTOSAR-based Electric Power Steering system (TI TMS570, PSA BMPV platform).
template: splash
hero:
  tagline: AUTOSAR-based Electric Power Steering for the PSA BMPV platform (TI TMS570, ASIL-D).
  actions:
    - text: Browse the modules
      link: general/autosar-overview/
      icon: right-arrow
    - text: Vector vs. custom code
      link: general/origin-guide/
      icon: document
---

import { Card, CardGrid } from '@astrojs/starlight/components';

## AUTOSAR layers

<CardGrid stagger>
  <Card title="Application Software (ASW)" icon="puzzle">
    Steering functions as AUTOSAR software components (`Ap_*`): assist, damping,
    return, learning, monitoring and PSA platform features.
    [Open ASW docs](asw/)
  </Card>
  <Card title="Complex Device Drivers (CDD)" icon="setting">
    Sensor/actuator drivers (`Sa_*`, `Cd_*`): SENT torque, digital MSB, SPI,
    ePWM/NHET, serial communication and micro diagnostics.
    [Open CDD docs](cdd/)
  </Card>
  <Card title="BSW Services" icon="layers">
    Diagnostics manager, NVRAM manager, Gliwa T1 executive and the
    Vector MICROSAR BSW stack (CAN, Dem, EcuM, NvM, …).
    [Open Services docs](services/)
  </Card>
  <Card title="ECU Abstraction" icon="random">
    ADC driver and user I/O hardware abstraction.
    [Open ECUAb docs](ecuab/)
  </Card>
  <Card title="MCAL & MCU Drivers" icon="cpu">
    DMA, TI FEE/Flash API and TMS570 startup code.
    [Open MCAL docs](mcal/)
  </Card>
  <Card title="Libraries & Shared Code" icon="open-book">
    Fixed-point math library, AUTOSAR platform types, diagnostic-service helpers.
    [Open library docs](syslib/)
  </Card>
</CardGrid>

## How to read this documentation

- Every module page states its **origin**: in-house custom code, Vector-provided
  MICROSAR artefacts, customised Vector artefacts, or third-party vendor code.
  See [Vector vs. custom](general/origin-guide/).
- Module design documents (MDD) and integration manuals converted from the
  original Word/PDF files live under
  [Converted Design Documents](modules/) and are linked from each module page.
- Build, safety and glossary notes live under [General](general/build-system/).
