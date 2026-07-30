---
title: Reviewing and rescanning parts
layout: default
parent: Operator manual
nav_order: 3
---

# Reviewing and rescanning parts

When the camera marks a feature bad, or cannot decide, you can send the robot back to that feature and look at it yourself before making the final call.

{: .warning }
The robot moves during a review. Stay out of the cell for the whole review, exactly as during a normal run.

## When to review

| Result | What it usually means |
|---|---|
| **Bad** | The camera judged the feature as failing |
| **Pending** | No result arrived for that feature |

A bad result is not always a bad part. Lighting, a smudge, or a slightly shifted part can produce a false reject, which is exactly what the review pass is for.

## How a review works

1. You pick the feature you want to look at.
2. The robot moves back to that feature and flashes the camera on it, so it is obvious which one you are looking at.
3. You decide **good** or **bad**.
4. The robot returns to its home position.

You can review as many features as you need, one at a time.

{: .screenshot }
The review overlay with red boxes around the list of features needing review and the Good and Bad buttons.

## Step by step

1. With the scan finished, open the review view for the features marked bad or pending.
2. Select the feature to inspect.
3. Wait for the robot to finish moving and flash the feature. **Do not enter the cell.**
4. Look at the feature — on the camera view, or visually from outside the cell if your plant's procedure allows it.
5. Select **Good** or **Bad**.
6. Wait for the robot to return home before selecting the next feature.

{: .warning }
Always wait for the robot to come to a complete stop before making your selection. Confirming while it is still moving makes it hard to tell which feature you are actually looking at.

## Marking results by hand

You can also change a verdict directly in the parts list, without sending the robot back — **Mark good** or **Mark bad**.

Use this only when you can already tell the answer, for example an obvious defect you can see from outside the cell, or a feature you have already reviewed.

{: .warning }
Your manual verdict replaces the camera's. Only override a result when you are certain. If you are not sure, send the robot back and look at the feature properly.

## After the review

Once every feature has a verdict, finish the run:

- **Save and exit** keeps the record, including your manual decisions.
- **Exit scan** leaves without keeping it.

Then handle the part according to your plant's process.

## When to escalate

Stop and call your supervisor if:

- The same feature fails on part after part. That usually means the setup or camera needs attention, not that every part is bad.
- Features come back **pending** repeatedly. The camera may not be producing results.
- The robot does not move when you request a review, or does not return home afterwards.
- Anything about the robot's movement looks different from normal.

You are not expected to fix any of these. Stop, keep people out of the cell, and escalate.
