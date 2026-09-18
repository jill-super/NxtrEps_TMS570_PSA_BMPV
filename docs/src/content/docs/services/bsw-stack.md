---
title: 'Vector MICROSAR BSW Stack'
description: 'Vector-provided AUTOSAR Basic Software stack integrated in SwProject/Source/BSW.'
---

# Vector MICROSAR BSW Stack

:::caution[Origin: Vector-provided]
Delivered as part of the Vector MICROSAR BSW stack / Vector documentation. Do not modify; configure only through the DaVinci/GENy generation workflow.
:::

## Purpose

Standard AUTOSAR Basic Software (BSW) from Vector MICROSAR, integrated under
`PSA_BMPV_EPS_TMS570/SwProject/Source/BSW/`. It provides communication,
memory, system and diagnostic services to the application. Evidence: source
files carry `Copyright (c) ... by Vector Informatik GmbH` headers, and the
high-level design is captured in the Vector Technical References
(see [HLDD references](../../integration/hldd/)).

## Modules present in this repository

| Directory | AUTOSAR role |
| --- | --- |
| `BSW/Can` | CAN driver (TMS470 DCAN) |
| `BSW/Il` | Interaction layer (GENy-generated signal handling) |
| `BSW/Tp` | Transport protocol (multi-connection) |
| `BSW/Nm` | Network management (OSEK indirect) |
| `BSW/EcuM` | ECU state manager |
| `BSW/Dem` | Diagnostic event manager |
| `BSW/Det` | Development error tracer |
| `BSW/NvM` + `BSW/MemIf` | NVRAM manager and memory abstraction |
| `BSW/Crc` | CRC library |
| `BSW/Dio`, `BSW/Port`, `BSW/Mcu`, `BSW/Gpt` | MCAL drivers |
| `BSW/IoHwAb` | I/O hardware abstraction base |
| `BSW/Wdg`, `BSW/WdgIf`, `BSW/WdgM` | Watchdog driver/interface/manager |
| `BSW/Os` | Operating system glue |
| `BSW/Xcp` | XCP slave (BSW side; application side: `Ap_ApXcp`) |
| `BSW/VStdLib` | Vector standard library |
| `BSW/SipVersionCheck`, `BSW/_Common` | Version checks and shared files |

## Configuration

The stack is configured with Vector DaVinci/GENy tooling; outputs land in
`SwProject/Source/GenData*` (see [RTE & generated configuration](../../integration/rte-gendata/)).
Application access goes through the RTE and the project wrapper layers
(`DemIf`, `DiagMgr`, `IoHwAbstractionUsr`, `NtWrap`).
