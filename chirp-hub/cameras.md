---
description: Find the IP cameras on your home network with Chirp Hub and start a recorder for each one, ready to pair with Lens.
---

# How Do I Connect Home IP Cameras to Chirp Hub?

Chirp Hub takes care of the home side of Chirp Lens. For every camera it starts a [Twin](../lens/installing-twin.md), the small recorder in your house that takes in the camera's video, records it and links the camera to Lens in the cloud. You never deal with Docker commands, image versions or port numbers.

## Why add cameras through Chirp Hub?

Set up by hand, each camera needs a Docker container with a unique name, storage volume, free port and image version. A doorbell camera, a garden camera and a garage camera already mean three containers to look after. Chirp Hub creates and keeps track of every one, installs Docker if the computer lacks it, and lists the state of each camera in one place.

## How do I find the cameras on my home network?

1. Open **Chirp Hub** and choose **Cameras** in the left menu.
2. Click **Scan for cameras**. The search of your home network takes around twenty seconds.
3. Any camera that announces itself shows up under **Found on your network**, together with its name and address.

<figure><img src="../.gitbook/assets/chirp-hub-cameras-scan.jpg" alt="Chirp Hub Cameras page with a camera found on the home network and a Set up button"><figcaption><p>After a scan, every camera that announced itself is listed with a Set up button.</p></figcaption></figure>

The scan finds a camera only when its discovery (ONVIF) is turned on and it is on the same network as the hub. If one of your cameras is missing from the list, use **Add camera** for it instead.

## How do I set up a camera the scan found?

1. Click **Set up** beside the camera. Chirp Hub works through three steps and shows each one as it goes: **Docker**, **Camera software** and **Your camera**. The camera software downloads once, with your first camera; after that, each new camera is ready within seconds.
2. When you see **Your camera is ready.**, write down the sign-in details that come with it.
3. Click **Open camera**, and that camera's Twin page opens in your browser.
4. Sign in using the username and password from Chirp Hub. On that first sign-in the Twin has you pick a password of your own, and the details Chirp Hub showed no longer work afterwards.
5. Carry on in the Twin: add the camera's stream and pair it with Lens, following [Connecting a Camera](../lens/connecting-a-camera.md).

## How do I add a camera the scan can't find?

1. Click **Add camera**. Chirp Hub sets a new camera up straight away and names it with a number, for example **Camera 2**.
2. You see **Open your new camera and choose which camera it records.** together with the sign-in details.
3. Click **Open camera**, sign in, and type the camera's stream address into the Twin. Until you do, the **Address** column shows **Set in camera setup**. Look up your camera brand in [RTSP Camera URLs](../lens/rtsp-camera-urls.md) to find its stream address.

## What happens if Docker isn't installed?

Docker is required for cameras. When it's missing or stopped, Chirp Hub explains its plan and shows one button: **Install Docker and add camera**, **Start Docker and add camera** or **Fix permissions and add camera**. Click it, and Chirp Hub finishes the camera without further help.

* **Windows** — Chirp Hub downloads Docker Desktop and installs it; approve the administrator prompt. Your PC may need to restart, and Chirp Hub opens again afterwards to finish adding the camera.
* **macOS** — Chirp Hub sets up a Docker engine of its own (around 400 MB), with no password and nothing new in Applications.
* **Linux and Raspberry Pi** — Chirp Hub installs Docker Engine and asks you for your password.

## How do I manage or remove a camera?

Each camera under **Your cameras** comes with three buttons:

* **Open camera** — opens that camera's Twin page in the browser.
* **Sign-in details** — brings back the first sign-in details.
* **Remove** — asks what should happen to the recordings. **Remove, keep recordings** stops the camera but leaves its video on the computer; **Remove and delete recordings** deletes the video too.

## How many cameras can Chirp Hub record?

That comes down to the computer running Chirp Hub. A [Raspberry Pi](raspberry-pi/README.md) 4 records about six or seven cameras while doing its other jobs. On a [computer](computer.md), the only limits are its processor, memory and network, so a home with lots of cameras is better off running Chirp Hub on a PC. The Dashboard's **Processor load** and **Memory used** show how much headroom is left.

## How do I get the most out of my home cameras?

* Turn on ONVIF discovery in each camera's own settings so the scan picks it up.
* Before adding cameras to a Raspberry Pi, check **Processor load** on the Dashboard; a Raspberry Pi 4 tops out at about six or seven. Need more? Run Chirp Hub on a [computer](computer.md).
* Save the password you pick at the first sign-in in a password manager the family shares. Chirp Hub doesn't keep a copy.
