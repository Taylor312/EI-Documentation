---
title: Safety
layout: default
parent: Reference
nav_order: 5
---

# Safety

{: .warning }
Easy Inspection commands a physical industrial robot. It is **not** a safety system and provides **no** functional safety. Every stop it offers is a software stop. Safety comes from the cell's guarding, the robot's own safety configuration, and a hardwired emergency stop circuit.

## Non-negotiables

- A **hardwired emergency stop** must be within reach of anyone operating or teaching the station.
- The work cell must be **guarded and clear** before any command that moves the arm.
- Only **trained personnel** should teach, commission, or run the station.
- The robot's own **safety configuration** — speed and force limits, safe zones, protective stops — is set on the controller and is what actually constrains the machine. Easy Inspection does not modify it and cannot compensate for it being wrong.

## The software stop

The red **E-STOP** button in the app, and the `Space` shortcut, call the robot's software emergency stop.

{: .screenshot }
The jog HUD with a red box around the E-STOP button.

What it does: stops commanded motion promptly.

What it does not do:

- Make the cell safe to enter
- Remove power or engage a safety-rated stop
- Function if the PC, the network, or the app is not responding

{: .warning }
Never rely on the on-screen button as your only means of stopping the machine. If a person is at risk, use the hardwired emergency stop.

Stopping abruptly at speed can damage the robot, the end effector, or the part. After a software stop the arm stays locked until it is unbraked and recovered — see [Connect the robot]({{ site.baseurl }}/connect-robot.html).

In offline mode the stop only cancels simulated motion. Nothing about offline mode reaches real hardware.

## Teaching safely

Teaching is the highest-risk activity, because you are deliberately moving the arm close to fixtures with a path that has never run before.

- Verify the correct tooltip **before** capturing anything. A wrong tooltip puts every waypoint and every no-go volume in the wrong place — see [End effector and tooltip]({{ site.baseurl }}/end-effector.html).
- Start with **small steps and low speed**. Defaults are 1 mm and 40%; drop to 0.5 mm for final approach.
- Confirm axis directions in **clear space** on every new cell before working near the part.
- Capture **no-go volumes first**, and set a safety margin that covers teaching error and part variation — see [Teaching a routine]({{ site.baseurl }}/teach-routine.html).
- **Simulate** the planned path before executing it on hardware.
- Remember that jogging is stepwise. If nothing happens, the previous move may still be running. Do not repeatedly press the control; check the status message.

## Commissioning safely

- The first hardware run of a new routine is the riskiest moment in the whole process. Clear the cell and station someone at the hardwired e-stop.
- Watch the first run in full rather than checking the results afterwards.
- Verify approach and retract clearances at every feature, not just the ones that look tight.
- Re-validate after **any** change to waypoints, volumes, home points, or routine ordering.

## Production safely

- Operators need the hardwired e-stop location, the guarding rules, and the stop procedure before their first shift. Give them the [Operator manual]({{ site.baseurl }}/operator/).
- Never reach into the cell during a run, including during a review pass. The arm moves to the feature under review under program control.
- Change the factory-mode unlock password from its default so the locked screen actually restricts access — see [Factory mode setup]({{ site.baseurl }}/factory-config.html).
- Treat a stopped-but-not-recovered robot as still live. It has not been made safe.

## What this software is not responsible for

| Concern | Owned by |
|---|---|
| Guarding, light curtains, interlocks | The cell's safety system |
| Emergency stop circuit | The cell's electrical design |
| Robot speed and force limits, safe zones | The Standard Bots controller configuration |
| Operator training and authorization | Your organization |
| Compliance with local machinery regulations | Your organization |

Easy Inspection is a teaching and inspection interface layered on top of all of the above. It assumes those are already correct.
