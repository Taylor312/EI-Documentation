---
title: Troubleshooting
layout: default
parent: Reference
nav_order: 4
---

# Troubleshooting

Symptoms grouped by subsystem. Work top to bottom within a section; the earlier checks isolate the later ones.

## First, isolate the layer

A run touches five subsystems. Identify which one before changing anything.

| Question | If no |
|---|---|
| Does telemetry show a live pose? | Connection problem |
| Is the tooltip gate satisfied? | Tooling problem |
| Does the Modbus panel show a connected client? | Modbus problem |
| Does the arm move when you play the routine? | Deployment or Modbus problem |
| Does the parts list advance during a run? | Camera or Cognex job problem |

---

## Connection

| Symptom | Cause | Fix |
|---|---|---|
| "Save the robot authorization token first" | No token stored | Enter the token in **Settings** then **Network** and save |
| HTTP 401 on connect, jog, or play | Token invalid or regenerated | Re-copy the token from the robot; confirm the tablet can play a routine; reboot the control box if the tablet also reports an invalid token |
| HTTP 500 asserting control mode | Known controller-side behaviour on some firmware | Check the robot's recovery panel; telemetry is unaffected |
| "Waiting for live robot pose" | Telemetry dropped | Reconnect telemetry; check cabling and controller power |
| "Assert API control before jogging" | Telemetry up, control not taken | Select **Assert API control** |
| "Saved robot credentials could not be decrypted" | Data folder from another PC or Windows user | **Reset robot connection settings**, re-enter the token |
| Telemetry drops on a multi-NIC PC | Adapter ambiguity or firewall | Set the ROS 2 adapter IPv4 explicitly; run **Configure Windows ROS2 firewall** |

{: .warning }
Before debugging the app, confirm the robot's own tablet can play a routine. If it cannot, the problem is on the controller.

## Tooling

| Symptom | Cause | Fix |
|---|---|---|
| End effector widget red on Home | Tooltip not configured | Select the Final Cognex tooltip in **SB Controller** |
| **Wrist TCP** chip in the title bar | Robot reporting the bare flange | Same as above |
| Capture disabled in the Routine Editor | Tooltip gate not satisfied | Same as above |
| Widget stays red after selecting the tooltip | Telemetry has stale data | Reconnect telemetry |
| Reported position disagrees with the pendant | Wrong tooltip, or wrong camera offset | Verify the tooltip first, then the camera tooltip offset in **User preferences** |

## Modbus

| Symptom | Cause | Fix |
|---|---|---|
| Self-test fails | Server not running, or port in use | **Start / restart server**; try another port and update the robot |
| Self-test passes, zero clients | Robot pointed at the wrong address, firewall, or client disabled | Use the PC address the panel reports for the robot-facing NIC; run **Open firewall for Modbus** |
| Last client shows `127.0.0.1` only | Only the self-test has connected | The robot has never reached the PC |
| Client connects, values never change | Wrong register offsets or data format on the robot | Registers are 16-bit unsigned, big-endian, at offsets 0, 1, 2 |
| Intermittent disconnects | Timeout too low or congested link | Raise the client timeout; put the link on a stable segment |

{: .warning }
A station with the camera on one NIC and the robot on another can have both on similar `192.168.1.x` subnets while being physically separate networks. The robot must be given the address the *controller* can reach.

## Running a routine

| Symptom | Cause | Fix |
|---|---|---|
| "No robot routine named ..." | Routine missing on the robot, or names differ | Create it on the tablet with the expected name, or change the expected name in the schema options |
| Routine plays, arm never moves | Blocked waiting on the **Routine** register | Check Modbus connectivity; confirm a routine was selected before Play |
| Wrong part inspected | Routine indices shifted after add, delete, or reorder | Recompile, redeploy, re-verify each routine tile |
| Changes appear to do nothing | Recompiled but not re-pasted onto the robot | Redeploy the schema — [Compile and deploy the schema]({{ site.baseurl }}/deploy-schema.html) |
| Arm collides or moves through the fixture | Missing or misplaced no-go volumes | Re-capture volumes; increase the safety margin; verify the tooltip |
| Cannot start a scan | A prerequisite is unmet | The run screen names it; see the checklist in [Test run and validation]({{ site.baseurl }}/test-run.html) |

## Camera and results

| Symptom | Cause | Fix |
|---|---|---|
| Arm runs the whole path, zero results | Camera trigger not wired, or the accumulator never increments | Verify the robot's trigger output fires the camera; verify the count cell in the job |
| Protocol probe fails | Camera unreachable, wrong IP or port | Check the camera IP and Native Mode port in **Settings** then **API** |
| Results shifted by one feature | Accumulator counts at the wrong moment, or waypoint order does not match inspection order | Fix the job so it increments exactly once per feature; re-check waypoint order |
| Everything reported fail | Classification cell is the wrong address, or the pass value list does not match the job | Verify the cell address; Cognex returns floats, so `1.000` and `1` are both matched by a pass value of `1` |
| Counts never reset between runs | Soft event not wired to the reset logic in the job | Wire the event in the job, or disable the reset and rely on the run baseline |
| Live view unavailable | Cognex client limit reached | Close other viewers of the camera web HMI |

{: .warning }
"The arm moves but nothing is scored" is nearly always the hardware trigger or the accumulator, not the app. Confirm the camera is actually firing before changing anything in Easy Inspection.

## Factory mode

| Symptom | Cause | Fix |
|---|---|---|
| **Turn on factory mode** disabled | Missing project, cell address, or tooltip | The screen lists which; see [Factory mode setup]({{ site.baseurl }}/factory-config.html) |
| Locked out, password unknown | Password changed and not recorded | The default is `admin` if it was never changed; otherwise recover from your records |
| Sidebar missing on a station you expected unlocked | Factory mode is on | **Exit factory mode** in the title bar |
| Factory mode off after a data reset | The lock is stored in local UI state | Re-enable it in **Factory config** |

## Data

| Symptom | Cause | Fix |
|---|---|---|
| Projects missing after an upgrade | Different Windows user account | Sign in as the original user; project data is per-user |
| Imported `.ie` produced a duplicate | Import always creates a new copy | Delete the copy you do not want |
| Imported project will not run | Schema not deployed, or embedded Modbus host points at the old PC | Recompile and redeploy — [Compile and deploy the schema]({{ site.baseurl }}/deploy-schema.html) |
| Corrupt or unreadable settings | Interrupted write | **Repair local data** in **Settings** then **Network** |

---

## When you are stuck

Narrow the problem by removing variables:

1. **Offline mode** — if teaching and simulation work offline, the app is fine and the issue is in the cell.
2. **Manual result source** — if a manual run is correct, motion and sequencing are fine and the issue is the vision job.
3. **Robot tablet** — if the tablet cannot play the routine, the issue is on the controller.
4. **Modbus self-test** — if it passes but the robot cannot connect, the issue is the network or firewall.

Each of those cleanly separates one half of the system from the other.
