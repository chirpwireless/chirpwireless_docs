---
description: Download Chirp Hub for Windows, macOS, Linux or a Raspberry Pi, install it, and get past the first-launch warning.
---

# How Do I Download and Install Chirp Hub?

Chirp Hub costs nothing. Each release lives on a single page with one installer per operating system:

**[Download Chirp Hub 0.1.1](https://github.com/chirpdepin/raspberry-pi-iot-hub/releases/tag/chirp-v0.1.1)**

Put it on the computer that stays in your home, not on a laptop that comes and goes with you. Your cameras, your Zigbee network and your gateway all run on whichever computer has Chirp Hub installed.

## Which Chirp Hub installer do I download?

On the release page, scroll down to **Assets** and choose the file that matches your computer. Each file name includes the version number.

| Your computer | File to download |
|---|---|
| Windows 10 or 11 (64-bit) | `Chirp-Hub-Setup-<version>.exe` |
| Mac with Apple silicon (M1 or newer) | `Chirp-Hub-<version>-arm64.dmg` |
| Mac with an Intel processor | `Chirp-Hub-<version>.dmg` |
| Ubuntu or Debian computer | `chirp-hub_<version>_amd64.deb` |
| Raspberry Pi (64-bit Ubuntu, prepared as in [How Do I Set Up a Raspberry Pi for Chirp Hub?](raspberry-pi/setup.md)) | `chirp-hub_<version>_arm64.deb` |
| Any other Linux | `Chirp-Hub-<version>.AppImage` for a regular 64-bit PC, `Chirp-Hub-<version>-arm64.AppImage` for an ARM board |

The `.yml` and `.blockmap` files on that page are not installers, so you can skip them.

## How do I install Chirp Hub on Windows?

1. Download `Chirp-Hub-Setup-<version>.exe` and run it.
2. If **Windows protected your PC** appears, choose **More info** and then **Run anyway**. SmartScreen asks this one time because the installer has no code signature yet.
3. Click through the installer. Chirp Hub starts when it's done and shows up in the Start menu.

Cameras need Docker Desktop. No Docker Desktop on your PC yet? When you add your first camera, Chirp Hub offers to fetch and set it up for you; just accept the administrator prompt.

## How do I install Chirp Hub on a Mac?

1. Download the `.dmg` for your Mac's processor and open it.
2. Drag **Chirp Hub** to **Applications**, and launch it from Applications rather than from the disk image.
3. macOS blocks that first launch, since Apple has not notarized this build yet. On macOS 15 or newer, go to **System Settings → Privacy & Security** and click **Open Anyway** beside Chirp Hub. On older versions, right-click Chirp Hub in Applications and pick **Open**.
4. When macOS asks if Chirp Hub may find devices on your local network, click **Allow**. If you don't, Chirp Hub can't see or reach your cameras.

From macOS 13 on, Chirp Hub brings a Docker engine of its own: roughly a 400 MB download, no password needed and nothing new in Applications. Any Docker you already use stays exactly as it was.

## How do I install Chirp Hub on Linux or a Raspberry Pi?

On Ubuntu or Debian, install the `.deb` package. It pulls in everything Chirp Hub needs:

```sh
sudo apt install ./chirp-hub_<version>_amd64.deb
```

A Raspberry Pi needs the [setup script](raspberry-pi/setup.md#how-do-i-get-the-pi-ready-for-the-lorawan-card-and-radios) before anything else. After that, install the `arm64` package and open **Chirp Hub** from the applications menu.

On any other distribution, use the AppImage:

```sh
chmod +x Chirp-Hub-<version>.AppImage
./Chirp-Hub-<version>.AppImage
```

If the AppImage won't start, add `libfuse2` with your package manager (on Ubuntu 24.04 the package is called `libfuse2t64`).

If Docker is missing when you add your first camera, Chirp Hub installs Docker Engine by itself and asks for your password in the system's password window.

## How do I update Chirp Hub?

Grab the newer Chirp Hub installer from the project's [releases page](https://github.com/chirpdepin/raspberry-pi-iot-hub/releases), where the Chirp Hub files start with `Chirp-Hub` or `chirp-hub`, and install it on top of the old one, just like the first time. Your cameras, Zigbee network and paired devices stay put, because they are saved in Chirp Hub's data folder rather than inside the program.

## How do I check which Chirp Hub version is running?

* Look at the version on the **Settings** page before and after updating, to be sure the new one is the one running.
* What's next: [Raspberry Pi](raspberry-pi/README.md) or [Windows, Mac and Linux](computer.md).
