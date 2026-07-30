---
title: End effector and tooltip
layout: default
parent: Setup and integration
nav_order: 5
---

# End effector and tooltip

**Prerequisites:** robot connected — see [Connect the robot]({{ site.baseurl }}/connect-robot.html).

Every taught waypoint is stored as a tooltip pose. If the robot's active tooltip is the bare wrist flange rather than the camera tip, every pose you capture is offset by the length of the end effector, and the routine will point the camera at the wrong place.

This is why the app refuses to capture waypoints or start a run until the correct tooltip is active.

## What "correct" means

The app compares the tooltip pose reported by the robot against where it computes the camera tip should be. It classifies the result as either the stock wrist tooltip or the **Final Cognex** tip. Only the latter is accepted.

| Indicator | Meaning |
|---|---|
| End effector widget is red on **Home** | Tooltip is not configured; capture and running are blocked |
| **Wrist TCP** chip in the title bar | The robot is reporting the bare flange |
| Widget reports the final tip active | You are good to proceed |

{: .screenshot }
The Home dashboard with a red box around the Configure end effector widget in its unconfigured red state.

## Setting the tooltip

The tooltip is selected on the robot, not in Easy Inspection. The app embeds the robot interface so you do not have to walk to the tablet.

1. Open **SB Controller** from the sidebar, or select **Configure end effector** on Home, which takes you there.
2. In the Standard Bots interface, select the **Final Cognex** / final tooltip definition for the camera end effector.
3. Return to Easy Inspection. The widget turns green once live telemetry reflects the change.

{: .screenshot }
The SB Controller tab with a red box around the tooltip selection control in the Standard Bots interface.

If the widget does not update, reconnect telemetry so the app picks up the new tooltip pose.

## Camera tooltip offset

**Settings** then **User preferences** contains a **Camera tooltip offset** section with X, Y, Z in millimetres and roll, pitch, yaw in degrees.

This offset describes where the camera tip sits relative to the wrist. It is used to classify the active tooltip and to drive the simulated arm in offline mode.

{: .warning }
Change this only if your end effector geometry differs from the configured default. An incorrect offset makes the app misjudge which tooltip is active, which either blocks capture on a correctly configured cell or allows capture on a misconfigured one.

## Why this gate exists

Two failure modes it prevents:

- **Silent teaching errors.** Waypoints captured with the wrong tooltip look fine in the 3D view but put the camera in the wrong place at run time, usually discovered only when parts start failing inspection for no visible reason.
- **Collisions.** No-go volumes are captured as tooltip positions too. A tooltip offset by the length of the end effector produces keep-out volumes in the wrong place.

If you are working in offline mode without hardware, the simulated arm uses the configured camera tooltip offset, so capture is allowed.

## Next

Continue to [Cognex vision setup]({{ site.baseurl }}/cognex.html).
