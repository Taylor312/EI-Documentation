---
title: Move
layout: default
nav_order: 4
---

# Move

The **Move** workspace issues **finite** six-axis Cartesian teach steps (not continuous hold-to-jog).

## Basics

- Use small increments first and watch live TCP telemetry.
- Speed scaling is operator-selected; teach increments are mapped across a limited TCP speed ceiling.
- Cartesian commands use a base reference frame, line movement, meters, and normalized quaternions.

## Control and recovery

- Assert API control before jogging when the cell requires it.
- Use software e-stop (red button / Spacebar) only as a software path — keep the hardware e-stop ready.
- Recovery may still require the Standard Bots Recovery Panel, wrist button, manual recovery, or a restart, depending on controller state.

## Related screens

| Nav item | Purpose |
|----------|---------|
| Robot settings | Connection, token, network helpers |
| SB Controller | Controller-oriented controls |
| Home | Session overview / dashboard |
