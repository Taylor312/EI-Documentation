---
title: Factory mode setup
layout: default
parent: Setup and integration
nav_order: 12
---

# Factory mode setup

**Prerequisites:** a validated routine — see [Test run and validation]({{ site.baseurl }}/test-run.html).

Factory mode turns the station into an operator HMI. The sidebar disappears, navigation is pinned to the run screen, and the app is locked to one project. Operators choose which routine to run and nothing else.

The run procedure itself does not change. Factory mode only removes everything an operator should not touch.

## Configure it

Open **Factory config**.

{: .screenshot }
The Factory config screen with red boxes around the factory project selector, the Classification and Accumulator cell fields, the unlock password field, and the Turn on factory mode button.

| Setting | What it does |
|---|---|
| **Factory project** | The project the station is locked to |
| **Classification cell** | Cognex cell holding pass/fail, default `K15` |
| **Accumulator cell** | Cognex cell holding the feature count, default `L15` |
| **Unlock password** | Required to leave factory mode; default `admin` |
| **Configure end effector** | Shortcut to the tooltip setup |

Select **Save config**, then **Turn on factory mode**.

{: .warning }
Change the unlock password from the default before deploying a station. The default is public knowledge and is the only thing preventing an operator from leaving the locked screen.

The cell addresses here are the same ones on the run preferences page. Saving factory config copies them into the run settings so the HMI polls the right addresses.

## Why the button may be disabled

Factory mode will not enable until all of these are true:

| Requirement | Fix |
|---|---|
| A project is selected | Choose one in the dropdown |
| Classification cell is set | Enter the address from your Cognex job |
| Accumulator cell is set | Enter the address from your Cognex job |
| Final Cognex tooltip is active | [End effector and tooltip]({{ site.baseurl }}/end-effector.html) |

These are checked because each one silently produces wrong results rather than an obvious failure. A locked station with the wrong cell address will run all shift and score nothing.

Two further things are not checked here but are required at run time:

- The master schema must be on the robot — [Compile and deploy the schema]({{ site.baseurl }}/deploy-schema.html)
- The Modbus server must be reachable from the robot — [Modbus setup]({{ site.baseurl }}/modbus.html)

## What operators see

- No sidebar; the run screen only.
- A **Factory mode** chip and an **Exit factory mode** control in the title bar.
- The project name shown as locked; only the routine can be chosen.
- Attempting to navigate elsewhere returns to the run screen.

{: .screenshot }
The application in factory mode with a red box around the Factory mode chip and Exit factory mode control in the title bar.

Give operators the [Operator manual]({{ site.baseurl }}/operator/). They do not need the rest of this site.

## Leaving factory mode

Select **Exit factory mode** in the title bar and enter the unlock password. The full application returns, with the project still open.

Do this for re-teaching, upgrades, or diagnosis, and turn factory mode back on before releasing the station.

## Routine indices and operator choices

Operators pick routines by name, but the selection is sent to the robot as the Modbus **Routine** register value, which is the routine's 1-based position in the project.

{: .warning }
If you add, delete, or reorder routines, those indices shift. Recompile and redeploy the master schema, then confirm that each routine tile still starts the part it names. Getting this wrong means an operator selects one part and the robot inspects another.

## Handover checklist

Before signing the station over:

1. Unlock password changed from the default and recorded somewhere retrievable.
2. Correct project locked, and every routine tile verified against the part it runs.
3. Cognex cell addresses match the deployed job.
4. Modbus server set to start on launch, and the firewall rule in place.
5. Telemetry set to connect automatically, so a restart does not require an integrator.
6. `.ie` backup of the project exported and stored off the station.
7. Operators shown the run, review, and stop procedures on real parts.

## Next

For plant-level integration beyond this PC, continue to [External control and PLC integration]({{ site.baseurl }}/external-control.html).
