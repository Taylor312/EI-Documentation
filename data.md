---
title: Projects, storage and backup
layout: default
parent: Reference
nav_order: 2
---

# Projects, storage and backup

Where Easy Inspection keeps things, what survives an upgrade, and what to back up.

## Location

Everything lives in the per-user application data folder:

```
%APPDATA%\Easy Inspection\
```

Nothing of value is stored in the installation directory, so upgrading or reinstalling the app leaves your work intact. Conversely, wiping this folder destroys projects, routines, and scan history with no recovery other than a `.ie` backup.

Because it is per-user, a different Windows account on the same PC sees a different set of projects.

## What is in there

| File | Contents |
|---|---|
| `projects.json` | All projects, their routines, waypoints, volumes, home points, and compiled schemas |
| `app-preferences.json` | User preferences: jog defaults, shortcuts, Modbus settings, camera settings, result cells |
| `robot-settings.json` | Robot URL and the encrypted API token |
| `scans.json` | Scan history and per-feature results |
| `saved-paths.json` | Remembered file locations |
| `downloads/` | Exported `.ie` packages |

A small amount of UI state — the factory-mode lock and floating panel positions — is kept in the app's own browser storage rather than these files. Clearing it resets window layout, and can drop the factory lock, so treat factory mode as configuration to re-verify after a data reset.

{: .warning }
The API token is encrypted with Windows DPAPI, bound to the current Windows user on the current machine. Copying `robot-settings.json` to another PC produces a token that cannot be decrypted. Keep the token available separately when re-imaging or replacing a station.

## `.ie` packages

A `.ie` file is the portable form of a project. Export with **File** then **Download .ie package**, or from the Projects screen.

{: .screenshot }
The File menu open with a red box around Download .ie package and Import .ie package.

It is a ZIP archive containing a manifest, the project definition, and per routine the waypoints, compiled schema, clearance volumes, and metadata, plus any assets.

| Travels in a `.ie` | Does not travel |
|---|---|
| Projects and routines | The robot API token |
| Waypoints, no-go volumes, home points | Machine-specific network settings |
| Compiled master schema | Scan history |
| Routine metadata and assets | The routine deployed on the robot |

Importing assigns new internal identifiers, so importing the same package twice gives you two independent copies rather than overwriting the first.

{: .warning }
Restoring a `.ie` on a new PC does not restore the robot. The compiled schema still has to be pasted onto the controller, and the Modbus host embedded in it points at the old PC's address — recompile after import if the address changed. See [Compile and deploy the schema]({{ site.baseurl }}/deploy-schema.html).

## Backup routine

For a commissioned station:

- Export a `.ie` package after any teaching change, and keep it off the station.
- Record the robot URL and keep the API token somewhere retrievable.
- Record the factory-mode unlock password.
- Note the app version in use.

For a full snapshot, copy the whole `%APPDATA%\Easy Inspection\` folder while the app is closed. That captures preferences and scan history as well, but remember the token will not decrypt elsewhere.

## Restoring onto a replacement PC

1. Install the same app version — [Downloads and versions]({{ site.baseurl }}/downloads.html)
2. Enter the robot URL and API token, and save — [Connect the robot]({{ site.baseurl }}/connect-robot.html)
3. Import the `.ie` package
4. Recompile the master schema and redeploy it to the robot if the PC's IP address changed
5. Reconfigure the Modbus server and firewall — [Modbus setup]({{ site.baseurl }}/modbus.html)
6. Reconfigure factory mode, including the unlock password
7. Run a validation scan before releasing the station

## Repair actions

**Settings** then **Network** includes two recovery actions:

| Action | Effect |
|---|---|
| **Reset robot connection settings** | Clears the stored URL and token. Use when saved credentials cannot be decrypted. |
| **Repair local data** | Rewrites application data files that have become unreadable. |

{: .warning }
Use these deliberately. Resetting connection settings requires re-entering the token, which you need to have kept a copy of.

## Scan history

Completed scans are recorded per project with good, bad, and pending counts, and a per-feature breakdown. History is local to the PC and is not included in a `.ie` export. If results need to be retained for quality records, copy them off the station on your own schedule.
