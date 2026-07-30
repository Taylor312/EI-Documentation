---
title: Home
layout: home
nav_order: 1
description: Operator documentation for Easy Inspection
---

# Easy Inspection

Operator and setup documentation for **Easy Inspection** — the desktop app for connecting to a Standard Bots controller, teaching inspection routines, and running them on the plant floor.

## Start here

1. Read [Safety](safety.md) before commanding motion.
2. [Connect the robot](connect-robot.md) and verify telemetry.
3. Use [Move](move.md) for finite teach jogs.
4. Build work in [Projects & routines](projects-and-routines.md).
5. Validate with [Test Run](test-run.md).
6. Configure [Factory mode](factory-config.md) when locking the HMI to one project.
7. When needed, set up [Modbus](modbus.md) for plant I/O.
8. Know where [data lives](data.md) (AppData, `.ie` packages).

{: .warning }
This software can command physical industrial machinery. Keep a trained operator at the hardware emergency stop. The in-app red button and Spacebar are a **software** e-stop only — not a substitute for a hardwired safety circuit.
