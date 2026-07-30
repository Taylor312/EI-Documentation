---
title: Projects and routines
layout: default
parent: Setup and integration
nav_order: 8
---

# Projects and routines

**Prerequisites:** none, though teaching requires a connected or simulated robot.

## How work is organized

| Level | What it is |
|---|---|
| **Project** | A station or a family of parts. Holds one master schema and any number of routines. |
| **Routine** | One part program: its waypoints, no-go volumes, home points, and compiled output. |

A project is what factory mode locks onto. Operators pick a routine within that project; they cannot change the project. So group parts that run on the same station into one project.

{: .screenshot }
The Projects screen with a red box around the saved projects grid and the Create new project button.

## Create or open a project

From **Projects**:

- **Create new project** — starts an empty project.
- **Upload .ie file** — imports a project package exported from another station.
- Selecting a saved project card opens it.

With a project open you can rename it inline, **Switch project**, **Create new project**, or **Close project**.

## Routines inside a project

With a project open:

- **New routine** creates a part routine.
- Each routine card carries a **Part name** field and opens into the [Routine Editor]({{ site.baseurl }}/teach-routine.html).
- Routines can be deleted from their card.

{: .screenshot }
An open project with red boxes around the New routine button and the Part name field on a routine card.

{: .warning }
Routine order matters. Each routine gets a 1-based index that the robot selects through the Modbus **Routine** register. Reordering or deleting routines changes those indices, so recompile and redeploy the master schema afterwards, and re-verify that operators' routine choices still map to the right parts.

## The master schema

A project has one **master schema**: a single Standard Bots routine containing every taught part routine as a branch. At run time the robot reads the Modbus **Routine** register and executes the matching branch.

This is why the whole project deploys as one routine rather than one routine per part.

The **Master schema** section of the project screen provides:

- **Go to master schema upload page** — the deployment workflow
- **Load master as default** — makes this the routine the app plays

Full detail in [Compile and deploy the schema]({{ site.baseurl }}/deploy-schema.html).

## Portable `.ie` packages

**Download .ie package** exports the open project as a single file. It is a ZIP archive containing the project definition and, per routine, the waypoints, compiled schema, clearance volumes, and metadata.

Use it to:

- Back up a commissioned station before an upgrade or re-teach
- Move a project to another PC
- Hand a configuration to someone else for review

Importing assigns fresh internal identifiers, so importing a package twice creates two independent copies rather than overwriting.

{: .warning }
A `.ie` package does not contain the robot API token. That is encrypted per Windows user and machine and must be re-entered on the destination PC. See [Projects, storage and backup]({{ site.baseurl }}/data.html).

## Where this data lives

Projects are stored in the application data folder on the PC, not in the installation directory and not in any repository. Reinstalling or upgrading the app leaves them in place; wiping the data folder destroys them.

Details, file names, and backup guidance are in [Projects, storage and backup]({{ site.baseurl }}/data.html).

## Next

Continue to [Teaching a routine]({{ site.baseurl }}/teach-routine.html).
