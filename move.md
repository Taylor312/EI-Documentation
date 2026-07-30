---
title: Move and jogging
layout: default
parent: Setup and integration
nav_order: 4
---

# Move and jogging

**Prerequisites:** telemetry connected and API control asserted — see [Connect the robot]({{ site.baseurl }}/connect-robot.html). Offline mode also works for practice.

**Move** is the full-screen 3D workspace where you drive the arm. It is also the view underneath the Routine Editor phases that need motion, so the controls described here are the ones you will use during teaching.

{: .screenshot }
The Move screen with red boxes around the 3D viewport, the jog HUD, the telemetry dock, and the camera button.

## Why the app has its own jog

The robot's built-in jog waits before each move commits, so teaching a part with dozens of closely spaced features becomes slow and imprecise — you overshoot, wait, correct, wait again.

Easy Inspection instead sends **finite Cartesian steps** through the robot's REST API. Each press produces one bounded move that starts immediately, which makes fine positioning feel direct. The trade-off is that it is stepwise rather than continuous: the app deliberately does not offer hold-to-jog, and each step is serialized so a new command is not sent until the previous one finishes.

In practice this means:

- Tap for a single step; the arm moves that increment and stops.
- If you press again before the previous move completes, the app tells you motion is already in progress.
- To cover distance, increase the step size rather than mashing the button.

## The jog HUD

The HUD is draggable, so position it wherever it does not cover the feature you are teaching.

| Control | Purpose |
|---|---|
| **Direction pad** | Jog along the current axis set |
| **XYZ / Angle toggle** | Switch the pad between linear translation and rotation |
| **Linear step** | Distance per press, roughly 0.5 mm to 200 mm |
| **Rotational step** | Degrees per press, roughly 0.5 to 45 |
| **Speed** | Percentage of the teach speed ceiling |
| **Keyboard control** | Enable or disable the jog keys |
| **Reset tooltip orientation** | Snap the tool to a known orientation, keeping position |
| **E-STOP** | Software emergency stop |

Motion is commanded in the robot's base reference frame.

### Default keyboard shortcuts

| Action | Key |
|---|---|
| Jog X | `A` / `D` |
| Jog Y | `W` / `S` |
| Jog Z | `Q` / `E` |
| Toggle XYZ / Angle | `P` |
| Capture waypoint | `Enter` |
| Software emergency stop | `Space` |

All of these are rebindable in **Settings** then **User preferences** — see [Settings reference]({{ site.baseurl }}/settings.html).

### Sensible starting values

| Setting | Default | Notes |
|---|---|---|
| Speed | 40% | Lower it near fixturing |
| Linear step | 1 mm | Start at 0.5 mm for final approach |
| Rotational step | 1 degree | |

{: .warning }
Begin every new cell with small increments in clear space. Confirm that X, Y, and Z move the way you expect in the base frame, and confirm the rotation axes, *before* jogging near fixtures or the part.

## Telemetry and the 3D view

The left dock shows live tooltip position, orientation, and joint angles, plus an indicator when the camera trigger output fires. The 3D viewport supports orbit, pan, and zoom, and draws the taught path once a routine has waypoints.

Use the telemetry readout, not the 3D model, as the source of truth for position.

## Camera while jogging

**Open camera** shows the live Cognex feed in a floating panel, which you can detach to its own window on a second monitor. This is how you confirm the part is actually framed at a candidate waypoint before capturing it.

{: .screenshot }
The Move screen with the floating camera panel open and a red box around the Open camera button.

## The software stop

The red **E-STOP** button and the `Space` shortcut call the robot's software emergency stop.

{: .warning }
This is a software stop. It is not a replacement for the hardwired emergency stop circuit, and it does not make the cell safe to enter. It stops motion abruptly, which at speed can damage the robot or tooling, and movement stays locked until the robot is unbraked and recovered.

In offline mode the stop only cancels simulated motion.

## Next

Continue to [End effector and tooltip]({{ site.baseurl }}/end-effector.html).
