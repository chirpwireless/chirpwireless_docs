---
description: "Find a home camera, change its name, restore its Twin connection, or remove it from Chirp Lens."
---

# Managing Cameras

**Cameras** keeps the household's connected camera views in one inventory. Names such as Garden Gate, Upstairs Landing, or Holiday Home Entrance help you find the right view even when the cameras come from different manufacturers. You can also check which Twins have stopped contacting Chirp.

## Find the view you need

Open **Cameras** from Chirp's main menu, then select **Cameras** in the Lens sidebar. Enter part of the camera's name in **Search cameras...** and choose **List view** or **Grid view** for the layout you prefer.

Look at **Status** and **Last Twin activity** before opening a view. A camera may be registered while its Twin is still disconnected. The activity time tells you when Twin contacted the platform; it does not tell you when someone last moved in front of the camera.

Each row shows the camera **Name**, **Status**, **Capabilities** (small badges for the features its Twin reports, such as audio or movement controls; a dash when none are reported), and **Last Twin activity** as a relative time. Every row has **Edit** and **Delete** buttons, and the top of the page has **Setup guide** (a checklist of the steps from installing Twin to seeing video) and **Add camera**. Longer lists are paged. Grid view shows the same information on cards.

Select a camera to open **Camera detail**. A breadcrumb leads back to **Cameras**, the pencil next to the title renames the camera, and tabs sit under the title. **Details** is always there. **Recording**, **Recording Area**, and **Storage** appear only when those features are switched on for your account; if you do not see them, the feature is not available to you yet.

The **Details** tab has two columns:

* **Left:** the camera's live picture with its controls (see [Watching Live Video](watching-live-video.md)), then **Media capabilities** with **Live audio** and **Talkback**. Each shows **Available**, **Not available**, **Not supported**, or **Needs setup**, with a reason such as "No audio track detected", "Audio codec not supported in the browser", "Camera cloud password required", "No two-way audio detected on this camera", "Not supported by this camera type", or "Audio transport failed". A camera that speaks ONVIF also gets an **ONVIF details** card with **PTZ support**, **Zoom**, **Pan/Tilt**, **Presets**, and **Default preset**.
* **Right:** **Lens connection** with **Device ID**, **Name**, **Twin key**, **Pairing** (Paired, Waiting for the Twin, or Pairing window expired, the last two in red) and the **Reconnect Twin** button; **Device details** with **Status** (Online or Offline), **Uptime**, **Last Twin activity**, **Stream type**, **SD available**, and **HD available**; **Device specs** with **Version**, **Hostname**, **Architecture**, **Memory**, **Camera type**, **IP addresses**, and **MAC addresses**; and, when Storage is on, a **Storage policy** card. Its chip reads **Local only** or **Local + Cloud**, and **Twin sync status** says whether the Twin follows the settings saved in Lens: **In sync**, **Local override** (the Twin uses a local configuration; save the Lens settings again to bring it back), or **Unknown** (the Twin has not reported yet).

If the camera is online but video does not play, check the stream in the local Twin and follow [Access and Troubleshooting](access-and-troubleshooting.md). Before the Twin has connected for the first time, the Details tab says it has not connected yet and there is nothing to show.

<figure><img src="../.gitbook/assets/chirp-lens-camera-management.jpg" alt="Chirp inventory retaining two home cameras while their Twins are offline"><figcaption><p>A disconnected camera stays in the list so you can check its details and recover its connection.</p></figcaption></figure>


<figure><img src="../.gitbook/assets/chirp-lens-cameras.jpg" alt="The Cameras list with two offline cameras, their last Twin activity, capability badges and Edit and Delete buttons, plus Setup guide and Add camera buttons"><figcaption><p>The Cameras list.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/chirp-lens-camera-detail.jpg" alt="A camera detail page with the Details, Recording, Recording Area and Storage tabs, a preview that says the camera is offline, and the Lens connection, Device details and Device specs cards"><figcaption><p>A camera detail page with its four tabs.</p></figcaption></figure>

## Give a camera a recognizable name

Choose **Edit camera**, update **Camera name**, and select **Save**. Use the place the camera watches rather than just its model number: for example, Back Door is easier to recognize than a manufacturer's product code. This changes its platform name without replacing or pairing the Twin again.

## Restore the connection to Twin

If the local Twin has lost its pairing, open the camera's **Details** and choose **Reconnect Twin** in **Lens connection**. Confirm that you want a new one-time connection token. Generating it invalidates any earlier token that has not been used.

Copy the **Lens API URL** and new token from the dialog into that camera's local **Lens Connector** settings. Use the values shown in the platform, then complete the steps in [Connecting a Camera](connecting-a-camera.md) before the token's displayed expiry time. An expired token must be replaced with a fresh one.

After saving, check that pairing succeeds and video returns. Preserve the Twin's existing configuration volume when recovering the connection or updating Docker: an empty replacement volume gives it a new identity. Connection tokens are private and should be hidden in any support screenshot.

## Retire a camera

Before removing a camera, review the home rules, dashboard references, and videowalls that depend on it. Choose **Delete**, then review the **Delete camera** confirmation, which asks "Delete {camera name}?". This removes its connection to the platform.

Removing a panel from a videowall is a smaller change: the camera remains available elsewhere. Deleting the platform camera also leaves its Docker container and any locally stored clips on the host computer. Remove those separately if you are retiring the installation altogether.
