---
description: "Check home cameras together in Chirp Lens and use supported sound or camera movement controls."
---

# How to Watch Live Video in Chirp Lens
Use Lens **Live view** for a quick look at what is happening at home. You can watch the front door and garden together, then enlarge one camera when you want a closer look.

<figure><img src="../.gitbook/assets/chirp-lens-live-view.jpg" alt="Two home cameras visible together in Chirp Lens Live view"><figcaption><p>Choose Preview for refreshed pictures or Live for continuous playback on each camera.</p></figcaption></figure>

## How do I open my cameras?
1. Choose **Cameras** in the Chirp sidebar.
2. Select **Live view** inside Lens.
3. Search for the cameras you need in **Search cameras...**, or use the status drop-down (**All statuses** by default) to filter by connection state.
4. Pick the layout with the toggle next to the search: **List view**, or a grid of 2, 3, or 4 columns (the buttons read "2 columns", "3 columns", and so on).
5. Start live video separately on each camera you want to watch.

The picture shown as a preview is not the same as an active live stream. Start live viewing when you want continuous video. Use fullscreen to focus on one camera and return to the grid to check the others.

More simultaneous streams use more bandwidth and browser resources. A smaller layout can make the pictures easier to read on a laptop.

## What do the sound and movement controls do?
If the camera supplies audio, you can listen or mute it. Two-way talkback is available only when the connected camera and its configuration support it.

A compatible motorized camera can offer pan, tilt, zoom, and preset positions. A fixed camera cannot be moved through software. The controls and capability states help show whether a function is available, needs setup, or is not supported.

## What do the tile controls and the dot in the corner show?

Each tile has a **Preview**/**Live** switch, a **Toggle fullscreen** control, and, when the camera supports them, the sound and talkback buttons. In **Live** mode the small status dot in the tile's corner shows connection details when you hover it: **Resolution**, **FPS**, **Codec**, **Bitrate**, and **Total Data**, and on a camera's own page also **Connection**, **RTT**, **Jitter**, **Packets Lost**, **Frames Dropped**, and **Key Frames**. They are handy when a picture stutters: a rising **Packets Lost** or **Jitter** points to the network between you and the home rather than to the camera.

## Why is my camera picture missing?
Once Lens reports a camera as offline, its preview shows **Camera is offline** instead of keeping the last snapshot on screen. **No preview available** means there is no preview to display; that message alone does not tell you whether the camera is offline. Check its connection state as well as the picture.

Check whether the camera is online. If it is offline, inspect its power and home network, then check that the computer running Twin is still on. If it is online but the live picture will not open, follow [Access and Troubleshooting](access-and-troubleshooting.md).

To hear about useful activity without watching continuously, [select a motion area](motion-zones.md) and connect it to [a home rule and alert](camera-rules-and-alerts.md).

Want to keep the front door and garden together in a layout you can reopen? Set up a [videowall](videowalls.md). Its [Return All to Home](videowalls.md#how-do-i-send-cameras-back-to-their-usual-view) action puts supported cameras back at their chosen presets after you look around.

## How do I listen and speak through a camera?
To listen to a supported camera, start its live stream and unmute the audio control; use the same control to mute it again. To speak through a camera with two-way audio, grant the browser microphone access, then hold the talkback control while speaking. Releasing it ends transmission. If this does not work, check the camera's displayed audio capability and setup as well as the browser permission.

## How do I move a camera and save positions?
**PTZ** means pan, tilt, and zoom. On a camera that supports it, open the controls and nudge the view with the arrows and zoom buttons. Save positions you will revisit:

1. Point the camera at a view you want to revisit, such as the garden gate.
2. Give that position a **Preset name** under **Presets**, then choose **Create preset**.
3. A **Preset update pending - refresh manually** message means you should refresh once the camera has finished the change.
4. Select **Go to** next to the saved position whenever you want to use it again.
5. For the view the camera should normally watch, choose the star action **Set as default**. The **Default** label identifies it; **Clear default** removes this choice.

The panel is titled **Camera controls**. Until you save a position it says **No presets saved**. **Return Home** sends the camera to its default position; it stays disabled with the hint **Set a default preset to enable Return Home** until you have chosen one. Remove an unwanted position with its **Delete** action and confirm (the dialog asks "Are you sure you want to delete ... preset?" and warns that it cannot be undone). When removing the default, select a replacement so return-home still has a destination. Check your motion zones whenever the camera starts watching a different area.

After you have followed some activity with one or several cameras, the [videowall return-home workflow](videowalls.md#how-do-i-send-cameras-back-to-their-usual-view) puts everything back to normal coverage.
