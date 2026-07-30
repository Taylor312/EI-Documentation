---
title: Teaching a routine
layout: default
parent: Setup and integration
nav_order: 9
---

# Teaching a routine

**Prerequisites:** a project open, the correct tooltip active ([End effector and tooltip]({{ site.baseurl }}/end-effector.html)), and either a connected robot or offline mode.

The **Routine Editor** walks one part through five phases. The phase tracker sits along the bottom of the screen and shows progress; phases that need motion take over the window with the 3D view from [Move]({{ site.baseurl }}/move.html) underneath.

| Phase | What you produce |
|---|---|
| 1. Train image | A trained Cognex job for this part |
| 2. No-go volumes | Keep-out regions the path planner must avoid |
| 3. Capture waypoints | The inspection poses |
| 4. Home points | Safe staging poses |
| 5. Master schema | The compiled robot routine |

{: .screenshot }
The Routine Editor with a red box around the five-phase tracker at the bottom of the screen.

---

## Phase 1: Train image

Train the Cognex job for this part and confirm the classification and accumulator cells behave. The app does not do this for you; the phase exists to keep the vision work in sequence and to record that it is done.

See [Cognex vision setup]({{ site.baseurl }}/cognex.html) for the requirements. Mark the phase complete when the job reliably distinguishes good from bad features and increments the count once per trigger.

---

## Phase 2: No-go volumes

Define the regions the arm must not pass through — the part, the fixture, clamps, anything else in the envelope. The app uses these when planning approach and retract moves between waypoints.

**At least one volume is required before you can capture waypoints.**

How to build one:

1. Jog the tooltip to a corner of the region.
2. Select **Capture point**.
3. Repeat around the region. **Undo** removes the last point.
4. **Close volume**, then **Save volume**.
5. **Add another volume** for additional obstacles.

| Control | Purpose |
|---|---|
| **Safety margin** | Inflates every saved volume by a fixed distance in millimetres |
| **Hull opacity** | Visibility of the volume in the 3D view |
| Volume list | Review and delete saved volumes |

{: .screenshot }
The No-go volumes phase with red boxes around the Capture point button, the Safety margin slider, and a saved volume shown in the 3D view.

{: .warning }
Volumes are captured as tooltip positions. If the tooltip is wrong, the keep-out regions land in the wrong place and the planned paths will be unsafe. Confirm the tooltip before this phase.

Set the safety margin to cover teaching error and part-to-part variation. It is cheaper to inflate the margin than to re-teach after a collision.

---

## Phase 3: Capture waypoints

Capture one waypoint per feature you want inspected, in the order you want them inspected.

{: .warning }
Waypoint order is inspection order, and it must match the order your Cognex accumulator counts. Feature 3 in the app is whatever the camera counted third.

For each feature:

1. Jog until the camera frames the feature. Use **Open camera** to check framing rather than guessing from the 3D view.
2. Optionally fire the **Shutter** to preview what the camera sees.
3. Select **Capture**, or press `Enter`.

| Control | Purpose |
|---|---|
| **Capture** | Save the current pose as a waypoint |
| **Shutter** | Fire the camera once |
| **Continuous 20 Hz** | Repeated triggering while framing |
| **Simulate** / **Stop** | Play the planned path offline |
| **Show path** / **Show arrows** | Path visualization |
| **Save** / **Clear** | Persist or discard the waypoint set |

The waypoint table lists everything captured. You can rename entries, delete them, and right-click to move the arm back to a stored point — useful for checking a pose you captured earlier.

{: .screenshot }
The Capture waypoints phase with red boxes around the Capture button, the waypoint table, and the camera panel.

Capturing a waypoint invalidates any previously compiled schema for the routine, because the compiled output no longer matches the taught data. Recompile in phase 5.

Use **Simulate** before moving on. It runs the planned path offline so you can see approach moves and clearance handling without commanding the arm.

---

## Phase 4: Home points

Home points are safe staging poses. The arm returns through them between features and at the end of a run, which is what keeps it out of the fixture when moving across the part.

1. **Capture main home** — the primary safe pose for the routine.
2. **Add side home** — additional staging poses for clusters of features that need a different approach.
3. Assign each waypoint to a home using the dropdown on its row, or select several waypoints in the 3D view and use **Group assign**.
4. **Re-validate** re-checks the assignments against the current geometry.

{: .screenshot }
The Home points phase with red boxes around the Capture main home button and the per-waypoint home assignment dropdowns.

Choose a main home that is clear of the part in every orientation, and give any awkward feature cluster its own side home rather than forcing a long traverse.

---

## Phase 5: Master schema

Compile the taught data into a robot routine. The button names the index this routine will occupy, for example *Compile to master schema as routine 2*, which is the value the Modbus **Routine** register must hold to select it.

Compiling produces one master schema for the whole project, containing every routine as a branch, plus the Modbus handshake, the camera trigger outputs, and the review loop.

{: .screenshot }
The Master schema phase with a red box around the compile button showing the routine index.

Compiling does not put anything on the robot. Deployment is a separate manual step — continue to [Compile and deploy the schema]({{ site.baseurl }}/deploy-schema.html).

---

## Re-teaching an existing routine

When a part or fixture changes:

1. Export a `.ie` backup first.
2. Re-capture only what changed; volumes, waypoints, and homes are edited independently.
3. Recompile the master schema.
4. Redeploy to the robot.
5. Re-run validation before releasing the station.

Skipping step 3 or 4 is the usual reason a re-taught routine behaves exactly as it did before: the robot is still running the previously deployed schema.
