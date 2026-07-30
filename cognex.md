---
title: Cognex vision setup
layout: default
parent: Setup and integration
nav_order: 6
---

# Cognex vision setup

**Prerequisites:** a Cognex In-Sight camera mounted on the end effector, reachable from the PC over the network.

{: .warning }
**Easy Inspection does not ship a vision program.** You train your own Cognex job for your parts. The app only reads two cells out of whatever job you build. Everything about how a part is judged good or bad is your job design, not the app.

## The contract between your job and the app

This is the whole integration. Your Cognex spreadsheet must expose two cells:

| Cell role | Default address | Value | Meaning |
|---|---|---|---|
| **Classification** | `K15` | `1` = pass, `0` = fail | The verdict for the feature just inspected |
| **Accumulator** | `L15` | Integer that increments | How many features have been inspected so far this run |

Anything else in the job is free. Use whatever tools, fixturing, lighting, and logic identify your parts consistently. Pattern match, blob, edge, calibrated measurement, a chain of conditions — the app neither knows nor cares, as long as those two cells end up holding the right values.

Cognex returns numeric cells as floats, so `1.000` and `1` are both read as a pass. The list of values treated as a pass is configurable.

### How the accumulator maps to your waypoints

At the start of a run the app records the accumulator's current value as a baseline. From then on:

```
feature index = current accumulator - baseline
```

That index selects which taught waypoint the verdict belongs to. So the accumulator must increment **exactly once per inspected feature**, in the same order the robot visits them.

{: .warning }
If the accumulator does not increment, the app never records a result and the run appears to stall with zero parts scored. If it increments more than once per feature, results land on the wrong waypoints. Get this right before teaching a long routine.

If the count jumps by more than one, the app fills in the skipped features with the current classification value rather than losing them.

## Triggering

**The robot triggers the camera, not the PC.** The compiled routine pulses a discrete output at each taught waypoint, which fires the camera in hardware. A second output drives a tower light.

| Robot output | Purpose |
|---|---|
| Output 1 | Camera trigger |
| Output 10 | Tower light / flash indicator |

This keeps trigger timing tied to the arm's actual position instead of to network round-trips.

{: .warning }
If the trigger is not wired, the run looks healthy — the robot moves through the whole path — but no new results ever arrive, because the camera is never fired. Verify the trigger before blaming the app.

The app can also fire a soft trigger during teaching so you can preview framing at a candidate waypoint.

## Connecting the app to the camera

Open **Settings**, then the **API** category.

| Setting | Default | Purpose |
|---|---|---|
| Camera IP | `192.168.1.20` | Camera address |
| Native Mode port | `23` | TCP port used to read cells |

Use **Run Protocol Probe** to confirm the PC can reach the camera and read cells. The same page has a Native Mode console for sending commands manually, plus an FTP browser for job files.

{: .screenshot }
The Settings API page with red boxes around the Camera IP field and the Run Protocol Probe button.

The app communicates over Cognex **Native Mode** and reads values with the Get Value command. During a run it polls both cells together, by default every 200 ms.

### Web HMI

The camera's own web interface can be embedded in the app and detached to its own window, which is how operators see the live image during a run. Note that Cognex limits how many clients can view the HMI at once; the app's result polling is a separate connection from the embedded view.

## Run-time result settings

**Settings** then **User preferences** has a **Pass / fail source** section:

| Setting | Default | Purpose |
|---|---|---|
| Result source | Cognex | Choose Cognex polling or manual operator scoring |
| Result cell | `K15` | Classification cell address |
| Screw count cell | `L15` | Accumulator cell address |
| Pass values | `1` | Comma-separated values treated as a pass |
| Poll interval | 200 ms | How often cells are read during a run |
| Count reset event | `1` | Soft event fired before a run to zero the accumulator |

Setting the result source to **Manual** makes the operator score every feature by hand. That is useful for commissioning a cell before the vision job is finished, and for validating that the motion is correct independently of the vision.

### Resetting the count

Before each run the app can fire a Cognex soft event to reset the accumulator. For this to work your job must wire that event to the logic that clears the count. If you would rather manage the count entirely inside the job, disable the reset event and rely on the run baseline instead.

## Commissioning checklist

1. Camera reachable from the PC; protocol probe succeeds.
2. Job trained on real parts, under production lighting.
3. Classification cell outputs `1` for a known-good feature and `0` for a known-bad one.
4. Accumulator increments once per trigger.
5. Trigger output from the robot fires the camera.
6. Cell addresses in the app match the addresses in your job.

{: .screenshot }
The Cognex spreadsheet view with red boxes around the classification cell and the accumulator cell.

## Next

Continue to [Modbus setup]({{ site.baseurl }}/modbus.html).
