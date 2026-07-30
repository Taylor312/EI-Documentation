---
title: Test run and validation
layout: default
parent: Setup and integration
nav_order: 11
---

# Test run and validation

**Prerequisites:** a routine taught, compiled, and deployed — see [Compile and deploy the schema]({{ site.baseurl }}/deploy-schema.html).

**Test Run** is the same run screen operators use in factory mode, with the rest of the application still available. This is where you prove a routine works before locking the station down.

## Before you press anything

The run screen enforces these, and will tell you which one is missing:

| Requirement | Where to fix it |
|---|---|
| Robot connected, or offline mode on | [Connect the robot]({{ site.baseurl }}/connect-robot.html) |
| Final Cognex tooltip active | [End effector and tooltip]({{ site.baseurl }}/end-effector.html) |
| Master schema compiled and on the robot | [Compile and deploy the schema]({{ site.baseurl }}/deploy-schema.html) |
| Modbus server running and reachable | [Modbus setup]({{ site.baseurl }}/modbus.html) |
| A routine selected that has waypoints | [Teaching a routine]({{ site.baseurl }}/teach-routine.html) |

{: .warning }
The cell must be clear and someone must be at the hardwired emergency stop. A validation run moves the arm at production speed through a path that has never executed on hardware before.

## Run a validation scan

1. Open **Test Run**.
2. Select the routine from the routines grid. Each tile shows the Modbus routine index it maps to — confirm it is the index you expect.
3. Select **Start**.
4. In the session, select **Play**.

{: .screenshot }
The Test Run lobby with red boxes around the routines grid, the routine index label on a tile, and the Start button.

The session shows four things at once: the 3D path with the current phase, the live camera, the parts list, and the run controls.

| Control | Purpose |
|---|---|
| **Play** / **Resume** | Start or continue the run |
| **Stop** | Stop the routine |
| **E-STOP** | Software emergency stop |
| **Save and exit** / **Exit scan** | End the session, with or without keeping the record |

{: .screenshot }
An active scan session with red boxes around the 3D view, the camera panel, the parts list, and the Play and E-STOP buttons.

## What to check on the first run

Work through these deliberately rather than watching the whole run and hoping.

**Motion**

- The arm reaches every taught feature with the camera framed as it was during teaching.
- Approach and retract moves respect the no-go volumes.
- The arm returns through the intended home points.

**Triggering**

- The camera fires at every feature, not just some.
- The tower light indicator matches what you see on the cell.

**Results**

- The parts list advances by exactly one entry per feature.
- Verdicts land on the correct feature, not shifted by one.
- A known-bad feature is reported bad, and a known-good one good.

{: .warning }
An off-by-one in the results is almost always the Cognex accumulator counting at the wrong moment, or waypoint order not matching inspection order. Fix it before production, not after.

## Validate the vision separately

A useful technique: set the result source to **Manual** in **Settings** then **User preferences**, and run once. You score every feature by hand, which proves the motion, triggering, and sequencing are right without the vision job being involved.

Then switch back to Cognex and run again. If the motion run passed and the Cognex run fails, the problem is in the job or the cell addresses, not the routine.

## Review and rescan

If any feature is bad or unscored, the session offers a review pass: the arm returns to that feature and flashes it so you can inspect it directly, then returns home when you confirm.

The mechanism and the operator-facing procedure are described in [Reviewing and rescanning parts]({{ site.baseurl }}/operator-review.html).

## Scan history

Completed scans are listed on the run screen with good, bad, and pending counts. Opening one shows the per-feature breakdown. Use this during commissioning to compare runs after a change rather than relying on memory.

Scan history is stored on the PC — see [Projects, storage and backup]({{ site.baseurl }}/data.html).

## Sign-off before production

Recommended gate before enabling factory mode:

1. Three consecutive clean runs on known-good parts.
2. At least one run with a deliberately defective part, correctly reported bad on the right feature.
3. A stop and resume performed mid-run without the arm losing its place.
4. A `.ie` backup of the project exported and stored.

## Next

Continue to [Factory mode setup]({{ site.baseurl }}/factory-config.html).
