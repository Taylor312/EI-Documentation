---
title: Connect the robot
layout: default
parent: Setup and integration
nav_order: 3
---

# Connect the robot

**Prerequisites:** the app installed, and network access to the Standard Bots controller.

Connecting happens in two distinct stages, and the difference matters: **telemetry** is read-only, **API control** is what lets the app move the arm.

## 1. Enter the connection settings

Open **Settings** and select the **Network** category.

| Field | What to enter |
|---|---|
| **Robot URL** | The controller address, for example `http://192.168.1.22:3000` |
| **Authorization token** | The Developer API token from the robot |
| **Control-box LAN address** | The controller's LAN IPv4 address |
| **ROS 2 Ethernet adapter IPv4** | Only if adapter selection is ambiguous on a multi-NIC PC |
| **ROS 2 bot ID** | Optional; auto-detected when blank |
| **Connect telemetry automatically** | Reconnect read-only telemetry on launch |

Select **Encrypt & save settings**.

{: .screenshot }
The Settings Network page with red boxes around the Robot URL field, the Authorization token field, and the Encrypt and save settings button.

### Getting the token from the robot

On the robot's web interface, open **Settings** then **Configure Developer API**, and enable both **ROS2 API** and **ROS2 bridge**. Generate or copy the API token there.

{: .warning }
Confirm that **Play** works from the robot's own tablet interface before debugging the desktop app. If the tablet cannot play a routine, the token or the controller is the problem, not Easy Inspection.

### How the token is stored

The token is encrypted with Windows DPAPI under the current user account and written to the application data folder. It is never shown again after saving and is not written to logs.

This has a practical consequence: **the token is bound to that Windows user on that PC.** Copying the data folder to another machine will not carry a working token. See [Projects, storage and backup]({{ site.baseurl }}/data.html).

### Windows firewall

If the PC has multiple network adapters, select **Configure Windows ROS2 firewall** and approve the administrator prompt. The rule created is scoped to the application, UDP only, local subnet only, and limited to private and domain profiles.

## 2. Connect and take control

Go to **Robot settings** (or use the Robot settings tile on Home). Work down the panel in order:

| Step | Button | Result |
|---|---|---|
| 1 | **Connect telemetry** | Read-only pose polling starts; the 3D view tracks the real arm |
| 2 | **Recover / clear robot error** | Only if the controller reports a fault |
| 3 | **Unbrake robot** | Releases the brakes |
| 4 | **Assert API control** | Takes command authority so the app can move the arm |

{: .screenshot }
The Robot settings connection panel with red boxes around Connect telemetry, Unbrake robot, and Assert API control.

There is also **Autoconnect robot + camera** on the Home dashboard, which performs the connect-and-assert sequence in one action.

{: .warning }
Asserting API control means the app can command motion. Make sure the cell is clear and someone is at the hardwired emergency stop before this step.

### Reading the status panel

The panel reports three things separately, because they fail independently:

- **Control mode** — whether the app holds command authority
- **Brake state** — whether the arm is free to move
- **Recovery** — whether the controller needs operator intervention

Telemetry can be healthy while control is unavailable. That is normal and is why the two are separate buttons.

## 3. Confirm it works

- The 3D view follows the real arm when you move it by hand or from the tablet.
- The telemetry panel shows plausible tooltip coordinates.
- Status shows API control active after step 4.

Compare the reported tooltip position against the robot's own pendant readout once. If they disagree, the active tooltip is probably wrong — see [End effector and tooltip]({{ site.baseurl }}/end-effector.html).

---

## Common failures

| Symptom | Cause | Fix |
|---|---|---|
| "Save the robot authorization token first" | No token stored | Enter the token in Settings and select **Encrypt & save settings** |
| HTTP 401 on connect, jog, or play | Token invalid or regenerated on the robot | Re-copy the token; confirm the tablet can play; reboot the control box if the tablet also reports invalid token |
| HTTP 500 when asserting control | Known controller-side behaviour on some firmware | Check the robot's recovery panel; telemetry still works independently |
| "Waiting for live robot pose" | Telemetry dropped | Reconnect; check cabling and that the controller is reachable |
| "Assert API control before jogging" | Telemetry connected but control not taken | Select **Assert API control** |
| "Saved robot credentials could not be decrypted" | Data folder copied from another PC or user | Use **Reset robot connection settings**, then re-enter the token |

The full table is in [Troubleshooting]({{ site.baseurl }}/troubleshooting.html).

## Next

Continue to [Move and jogging]({{ site.baseurl }}/move.html).
