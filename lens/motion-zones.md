---
description: "Focus home-camera motion detection on a doorway or gate instead of everything in the picture."
---

# How to Set Motion Zones for a Home Camera
A **motion zone** marks the part of a camera picture where movement should count. It helps when you care about someone approaching your door but do not want ordinary movement on the pavement to trigger the same response.

You draw the area in the camera's local Twin. The camera itself does not need a built-in AI detector.

<figure><img src="../.gitbook/assets/chirp-lens-motion-zone.jpg" alt="A selected area in the Chirp Twin motion-zone editor"><figcaption><p>This demonstration selects part of the room. Choose the area that matters in your own camera view.</p></figcaption></figure>

## How do I mark a motion zone?
1. Sign in to Twin and open **Settings → Recording**.
2. Set **When to record** to **Motion** so the motion-detection path is active.
3. Begin with time schedules and external conditions disabled while you test.
4. Open **Recording Area**.
5. Use a rectangle for a simple doorway, or a polygon to follow an irregular boundary.
6. Save your changes.

The editor's shortcuts are **R** for rectangle, **O** for polygon, and **M** for moving or deleting an area. Keep the pavement outside the selected shape if you only want to detect activity at the door.

## Can I draw the area in Chirp instead?

Yes. Open **Cameras**, select the camera, and choose the **Recording Area** tab. The card says: "Select the area where movement should start a recording. Movement outside the selected areas is ignored. Saved clips still show the full camera view." The camera's current snapshot appears with the same drawing tools: **Rectangular box (R)**, **Polygon-selection (O)**, and **Regions Manipulation (M)** to move, resize, or delete a shape. Select **Save**; the message "Zones saved." and then "Saved — pending sync to camera." means Lens has the areas and Twin will pick them up. If the camera is offline you see "No snapshot available. Camera must be online to edit zones." and cannot draw; if saving fails the card says "Failed to save zones. Please try again." Some places open the same editor as a **Region Of Interest** dialog with the hint "By defining one or more regions, motion will be tracked only in the regions you have defined." and **Save** and **Cancel** buttons.

## How do I test a motion zone?
Walk inside the area and check the motion reading. Then walk outside it and check again. Adjust the global pixel-change threshold if necessary: a lower threshold makes detection more sensitive.

Sensitivity applies to the detector rather than to each individual shape. If no areas are drawn, the whole picture is used. If several areas are drawn, movement in any of them can count as motion.

Changes in light, shadows, or weather can affect detection too. Revisit the setup after dark and after moving the camera. Motion detection tells you that part of the picture changed; it does not tell you who caused it.

## What should motion do?
You can use motion readings in Chirp without saving clips, as long as motion processing remains enabled. If you do want clips, enable [local recording](local-recordings.md) separately. Timetables and external conditions can restrict processing, so add those settings after the basic test works.

Your selected area does not crop live video or saved recordings. Continue with [Camera Rules and Alerts](camera-rules-and-alerts.md) to turn the motion reading into a useful notification.
