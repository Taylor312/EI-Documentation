---
title: Test Run
layout: default
nav_order: 6
---

# Test Run

**Test Run** is where you validate a taught routine before relying on it on the plant floor.

## Before you start

- Robot connected with valid telemetry (or use offline schema play when you only need path checks).
- Workcell clear; hardware e-stop reachable.
- Start at low speed / conservative settings.
- Confirm Modbus is healthy if the routine depends on holding registers — see [Modbus](modbus.md).

## Suggested checks

1. Open the correct project and routine.
2. Run once while watching TCP / joint feedback and the 3D path where available.
3. Confirm expected homes, clearance moves, and any camera / Cognex steps fire as taught.
4. Exercise software e-stop at low speed once so operators know the path.
5. Only then enable [Factory mode](factory-config.md) for locked HMI operation.

Expand this page with site-specific pass/fail criteria and who signs off a routine for production.
