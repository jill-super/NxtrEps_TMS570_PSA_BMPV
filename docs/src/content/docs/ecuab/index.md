---
title: 'ECU Abstraction'
description: 'ECU-abstraction drivers that hide MCU specifics behind a uniform I/O API.'
sidebar: { order: 0 }
---

# ECU Abstraction

ECU-abstraction drivers that hide MCU specifics behind a uniform I/O API.

## Modules in this layer

| Module | Component | Summary |
| --- | --- | --- |
| [Adc](./adc/) | Adc, Adc2 | ECU-abstraction ADC driver (ADC, ADC2 and common services) used by current, voltage and temperature sensing pa |
| [SwProject/IoHwAbstractionUsr](./swproject-iohwabstractionusr/) | IoHwAb9, IoHwAb10 | User I/O hardware abstraction (IoHwAb9/10) mapping signals to pins/peripherals. |
