---
title: Projects & routines
layout: default
nav_order: 5
---

# Projects & routines

Use **Projects** to organize inspection work, and **Routine Editor** to author the motion / inspection sequence.

## Typical flow

1. Create or open a project in **Projects**.
2. Edit the routine in **Routine Editor** (waypoints, schema steps, clearance, homes).
3. Save the schema to the routine when the teach is ready.
4. Validate with **Test Run** (live or offline) before production use.
5. Optionally export a portable **`.ie`** package for backup or another PC — see [Data & backup](data.md).

## Where data is stored

Day-to-day editing writes to local AppData (`projects.json`), **not** to Git. Reinstalling the app usually keeps projects; wiping AppData does not.

## Offline vs live

| Mode | What it is for |
|------|----------------|
| Offline teach / Move | Capture waypoints and homes without REST motion |
| Offline schema play | Simulate the compiled routine path on the PC |
| Live | Real controller telemetry and motion |

Teach jog and schema play are separate paths — do not assume one offline mode covers both.

## Notes

- Compiled routines include Standard Bots routine metadata (for example `"motionPlanner": "ROS2"`). That field is vendor routine metadata and is unrelated to any parked Electron ROS2 sidecar used in some development builds.
- Schema / compile issues are separate from controller auth failures (`401` on motion APIs). Fix the token first if Play fails with unauthorized.
