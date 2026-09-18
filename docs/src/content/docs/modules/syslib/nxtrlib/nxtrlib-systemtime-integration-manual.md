---
title: 'NxtrLib Systemtime Integration Manual'
description: 'Converted design document: NxtrLib Systemtime Integration Manual'
---

> **Source:** `NxtrLib/doc/NxtrLib_Systemtime Integration_Manual.docx`  
> **Module:** [NxtrLib](../../../../syslib/nxtrlib/)  
> **Note:** Converted automatically from Word (.docx) with python-docx (headings, lists and tables preserved; images/embedded objects omitted).

---

# Integration Manual – NxtrLib_SystemTime

## Dependencies

## Configuration

### Build Time Config

### Generator Config

#### System

## Integration

The following import steps must be completed:

- Place CBD project structure to appropriate integration folder

- Copy SystemTime_Cfg.h.tt into the Header folder and remove the .tt extension.

- Configure the constant D_TickRate_Cnt_u32 to the appropriate Os system tick time.

## Runnable Scheduling

This section specifies the required runnable scheduling.

## Memory Mapping

### Mapping

* Each …START_SEC… constant is terminated by a …STOP_SEC… constant as specified in the AUTOSAR Memory Mapping requirements.

### Usage

Table 1: ARM Cortex R4 Memory Usage

## Revision Control Log

| Module | Required Feature |

| --- | --- |

|  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

|  |  |  |

| Constant | Notes | SWC |

| --- | --- | --- |

|  |  |  |

| Runnable | Scheduling Requirements | Trigger |

| --- | --- | --- |

|  |  |  |

| Constant | Notes |

| --- | --- |

|  |  |

| Feature | RAM | ROM |

| --- | --- | --- |

| Full driver |  |  |

| Item # | Rev # | Change Description | Date | Author Initials |

| --- | --- | --- | --- | --- |

| 1 |  | Initial version | 26Jul13 | SAH |
