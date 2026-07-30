---
title: Factory config
layout: default
nav_order: 7
---

# Factory config

**Factory config** locks Easy Inspection to one project on the Run screen for HMI-style use.

Operators pick which routine to start. The robot runs the project master schema and selects the nested routine via Modbus register **Routine** (holding register offset `2`).

## Before enabling factory mode

You need all of the following:

1. At least one project created and selected as the factory project.
2. **Classification** and **Accumulator** Cognex cell names set — those cells are what the HMI reads for pass/fail and part count.
3. End effector / TCP frame configured (final TCP), using the end-effector setup in Factory config.
4. Save factory settings, then enable factory mode (password protected).

If any of those are missing, the app blocks enabling factory mode and shows a notice.

## Operator experience

- Navigation is restricted to the factory Run experience for the locked project.
- Routine selection on the HMI maps through Modbus; keep the Modbus server reachable — see [Modbus](modbus.md).

## Related

- [Projects & routines](projects-and-routines.md)
- [Data & backup](data.md) — factory lock settings also use browser localStorage on this Windows user profile
