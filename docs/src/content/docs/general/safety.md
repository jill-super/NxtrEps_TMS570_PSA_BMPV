---
title: Functional Safety (ASIL-D)
description: Safety concept elements visible in the codebase — firewalls, monitors and diagnostics.
---

# Functional Safety (ASIL-D)

The EPS is developed to **ISO 26262 ASIL-D**. The safety concept is visible
directly in the software structure:

## Safety architecture elements

- **Firewall components** bound safety-relevant torque paths:
  `AssistFirewall`, `DampingFirewall`, `ReturnFirewall`, `EtDmpFw` (end-of-travel
  damping firewall). Each has its own module page and MDD.
- **Temporal monitor** (`TmprlMon`, `Sa_TmprlMon`/`Sa_TmprlMon2`) provides
  independent timing/execution supervision.
- **Plausibility diagnostics**: torque reasonableness (`TqRsDg`), compliance
  error (`ComplErr`), signal conditioning plausibility (`SgnlCond`), motor
  phase reasonableness and driver diagnostics (`SVDiag`).
- **Controlled disable & shutdown** (`CtrldDisShtdn`, `ShtdnMech`, `Gsod`)
  bring the system to a safe state on faults.
- **Fault injection** (`FltInjection`) supports safety validation testing.
- **Micro-level self-tests** (`TMS570_uDiag`): FPU test, flash test
  (`FlsTst`), OS-error callouts.
- **Watchdog supervision**: Vector WdgM plus application checkpoints
  (`ChkPt`: `Ap_ChkPtAp6/9/10/11`).
- **Fail-action handling** in the diagnostics manager (`DiagMgr_FailAction`).

## Where to read more

- Module pages for each component above (all cross-linked from
  [ASW](../../asw/) and [CDD](../../cdd/)).
- Converted MDD / integration manuals under
  [Converted Design Documents](../../modules/).
- `SF46_GCCDiag_Implementation` documents GCC-level diagnostics for the SF46
  safety concept.
