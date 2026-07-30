---
title: Safety
layout: default
nav_order: 2
---

# Safety

Easy Inspection can move a live industrial robot.

## Rules

- Guard the workcell and keep a trained operator at the **hardware** emergency stop.
- Prefer a simulated robot before connecting to live hardware.
- The red button and **Spacebar** call the documented software emergency-stop endpoint. They are **not** replacements for a hardwired safety circuit.
- Software e-stop stops motion immediately and can damage the robot or surroundings at speed. Movement stays locked until the robot is unbraked / recovered per your cell procedure.

## Before first motion

- Confirm the controller URL and token against the robot Developer API screen.
- Confirm the physical e-stop is reachable and tested.
- Begin with small increments (for example 0.5 mm / 0.5°) in a clear workspace.
- Confirm X/Y/Z directions in the base frame before larger moves.
- Exercise software e-stop at zero or very low speed first.
