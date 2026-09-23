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
| The terminal cannot find `docker` | Check that Docker is installed and available to your terminal, then reopen the terminal if needed. Start with [Installing Twin](installing-twin.md#check-docker-is-ready). |
| Docker says it cannot connect to the engine | Open Docker Desktop or start Docker Engine on Linux. Check that Docker is connecting to the intended host, then retry `docker info`. A result from `docker --version` alone does not mean the engine is running. See [Docker's connection checks](https://docs.docker.com/engine/daemon/troubleshoot/). |
| Docker reports permission denied | Follow Docker's [Linux access instructions](https://docs.docker.com/engine/install/linux-postinstall/) if applicable, or the access guidance for your installation. Retry `docker info` from the terminal you will use for Twin. |
| Cameras disconnect after the computer sleeps or shuts down | Wake or start the computer, restore Docker, and check that the Twin container is running. Keep the computer awake and Docker running while you need the cameras. |
| First setup asks for **Current password** | Enter the temporary password supplied when Twin was started, then set your permanent password. Follow [Which password do I use?](installing-twin.md#which-password-do-i-use); do not enter your Chirp or camera password. |
| Twin does not start | Check the required first-use login variables and the container's logs and folder access. |
| No picture in Twin | Check camera power, network address, RTSP path, credentials, and video settings. |
| The Twin key is already in use | Find the camera already paired with it and use Reconnect Twin. |
| Chirp refuses to add the camera | Check your camera permissions and organization device limit. |
| An online camera will not play | Check stream settings and the connection between your browser, Lens, and Twin. |
| Movement does not reach the rule | Check Motion mode, the drawn areas, sensitivity, and any timetable or external condition. |
| Older clips are missing | Review both the size limit and age limit under Storage. |

If video cannot start through WebRTC in **Twin's local viewer**, Twin tries SD viewing when that camera source provides it. Without an SD option, it marks the stream unavailable. This describes the local Twin viewer, not the cloud Lens viewing controls. A change of viewing mode cannot reconnect a powered-off camera or guarantee a picture; check the camera and network if video is still missing.

If the platform reports a service connection error while adding a camera, check whether the camera was created before retrying. For help, provide the error message and connection state without including passwords, camera URLs containing passwords, or pairing tokens.
