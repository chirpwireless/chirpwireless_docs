---
description: "Check household camera access, reconnect Twin, and fix common Lens setup or viewing problems."
---

# Access and Troubleshooting

Chirp keeps cameras within the selected organization. When someone no longer needs access, update their organization access rather than sharing or changing one common Chirp login. This does not require setting up each camera again.

Twin has its own local administrator login, separate from your Chirp account. Keep both kinds of credentials private.

## Check the right home and permissions

The current Lens workspace requires camera-management permission. Rules, alarm definitions, and other resources have their own access requirements. If a camera or action is missing, first check the selected organization and your permissions there.

Adding cameras also depends on available organization device capacity. Every camera must have its own Twin key.

## Pair an existing camera again

Open the camera in Lens and choose **Reconnect Twin**. Copy the new token, then open **Settings → Lens Connector** in that camera's Twin. Select **Enter a new token to re-pair**, check the **Lens API URL**, paste the new **Connection token**, and select **Save** in the connection section. Return to Chirp to confirm the camera is online and its video works.

Keep the same Twin configuration volume so the installation retains its identity. Do not create a duplicate camera to fix a lost connection.

## Common problems

| What you see | Where to start |
|---|---|
| Twin does not start | Check the required first-use login variables and the container's logs and folder access. |
| No picture in Twin | Check camera power, network address, RTSP path, credentials, and video settings. |
| The Twin key is already in use | Find the camera already paired with it and use Reconnect Twin. |
| Chirp refuses to add the camera | Check your camera permissions and organization device limit. |
| An online camera will not play | Check stream settings and the connection between your browser, Lens, and Twin. |
| Movement does not reach the rule | Check Motion mode, the drawn areas, sensitivity, and any timetable or external condition. |
| Older clips are missing | Review both the size limit and age limit under Storage. |

If the platform reports a service connection error while adding a camera, check whether the camera was created before retrying. For help, provide the error message and connection state without including passwords, camera URLs containing passwords, or pairing tokens.
