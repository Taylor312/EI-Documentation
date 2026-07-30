---
title: Operator overview
layout: default
parent: Operator manual
nav_order: 1
---

# Operator overview

This manual is for running parts on an Easy Inspection station that has already been set up and locked into factory mode.

Everything described here happens on one screen. You do not need to configure anything, and you cannot break the setup from this screen.

{: .warning }
Before your first shift, make sure you know where the **hardwired emergency stop** is. The red button on the screen is a software stop. It is not a substitute for the physical e-stop, and it does not make the cell safe to enter.

## What the station does

The robot carries a camera. It moves to each point on the part in turn, photographs it, and the camera decides whether that feature passes or fails. The screen shows you the result for each feature as the run progresses.

If something is marked bad, or the camera could not decide, you can send the robot back to that feature so you can look at it yourself before making the final call.

## What you see

The station boots straight into the run screen. There is no sidebar and no menu of other screens — that is normal and means the station is locked correctly.

{: .screenshot }
The factory mode run screen at startup, with a red box around the routine selection area.

| Area | What it is |
|---|---|
| **Routine tiles** | The parts this station can inspect. You pick one. |
| **Project name** | Fixed. You cannot change it, and you do not need to. |
| **Factory mode chip** | Top of the screen. Confirms the station is locked. |

Once a run starts, the screen splits into four areas:

| Area | What it shows |
|---|---|
| **3D view** | Where the robot is and the path it is following |
| **Camera view** | What the camera is currently seeing |
| **Parts list** | Each feature and whether it passed or failed |
| **Controls** | Play, Stop, emergency stop, and exit |

{: .screenshot }
An active scan with red boxes around the 3D view, the camera view, the parts list, and the control buttons.

## The controls

| Button | What it does |
|---|---|
| **Start** | Opens a scan session for the routine you picked |
| **Play** / **Resume** | Begins or continues the run |
| **Stop** | Stops the routine in a controlled way |
| **E-STOP** (red) | Software emergency stop; also the `Space` key |
| **Save and exit** | Ends the session and keeps the record |
| **Exit scan** | Leaves the session |

## Before every run

1. The cell is clear. Nobody has a hand, tool, or fixture inside it.
2. The part is loaded and clamped correctly.
3. You know where the hardwired emergency stop is.
4. You have selected the routine that matches the part actually in the fixture.

{: .warning }
Selecting the wrong routine means the robot follows the wrong path. Depending on the part and fixture, it can collide. Check the routine name against the part in front of you every time.

## What to do if something looks wrong

| Situation | What to do |
|---|---|
| Robot moves somewhere unexpected | Hardwired emergency stop |
| Anyone approaches the cell during a run | Hardwired emergency stop |
| Robot stops on its own | Do not enter the cell; call your supervisor |
| Screen shows an error you do not recognize | Do not enter the cell; call your supervisor |
| Everything fails inspection | Stop; call your supervisor — the camera or the setup may need attention |
| Sidebar appears and the screen looks different | Do not use the station; call your supervisor. The station has been unlocked. |

You are not expected to diagnose the station. Stop, keep people out of the cell, and escalate.

## Next

Continue to [Running a scan]({{ site.baseurl }}/operator-running-a-scan.html).
