---
title: Running a scan
layout: default
parent: Operator manual
nav_order: 2
---

# Running a scan

The full procedure for inspecting one part.

{: .warning }
The cell must be clear before you press Play. Know where the hardwired emergency stop is. The red button on screen is a software stop only.

## 1. Load the part

Load and clamp the part in the fixture as you were trained. The robot follows a fixed taught path, so a part sitting differently than expected will be photographed in the wrong place, and in the worst case the robot can strike it.

## 2. Pick the routine

On the run screen, select the tile for the part you just loaded.

{: .screenshot }
The routine tiles on the factory mode run screen, with a red box around a selected tile.

{: .warning }
Match the routine to the part physically in the fixture. Do not assume the last operator left the right one selected.

## 3. Start the session

Select **Start**. The screen changes to the scan session: 3D view, camera view, parts list, and controls.

Nothing has moved yet.

## 4. Confirm the cell is clear

Look at the cell. No hands, no tools, no loose fixturing, nobody reaching in.

## 5. Play

Select **Play**.

The robot moves to each taught feature in turn and the camera fires at each one. As results come back, the parts list fills in.

{: .screenshot }
An active scan in progress with a red box around the parts list showing completed and pending features.

While it runs:

- Watch the cell, not just the screen.
- The parts list should keep advancing. If it stalls with the robot still moving, note it and tell your supervisor after the run.
- Do not reach into the cell for any reason.

## 6. Read the results

Each feature gets one of three states:

| State | Meaning |
|---|---|
| **Good** | Passed inspection |
| **Bad** | Failed inspection |
| **Pending** | No result yet, or the camera could not decide |

The session shows running totals of good, bad, and pending.

**If every feature is good**, the part passed. Go to step 7.

**If any feature is bad or pending**, you can send the robot back to that feature to look at it yourself. See [Reviewing and rescanning parts]({{ site.baseurl }}/operator-review.html).

## 7. Finish

| Choice | Use it when |
|---|---|
| **Save and exit** | Normal end of a run; keeps the record |
| **Exit scan** | Leaving without keeping the record |

Then unload the part and handle it according to your plant's process for a pass or a reject.

## Stopping a run

| Situation | Use |
|---|---|
| You need to pause in a controlled way | **Stop**, then **Resume** to continue |
| Something is going wrong on screen | **E-STOP** or `Space` |
| A person is at risk | **Hardwired emergency stop** |

{: .warning }
After any emergency stop, the robot stays locked until it is recovered. Do not enter the cell and do not attempt to restart it yourself. Call your supervisor.

## Running several parts

The station keeps the routine selected between runs, but confirm it each time anyway — especially if you are alternating between part types or taking over from another operator.

Completed scans are recorded on the station so a supervisor can review them later.
