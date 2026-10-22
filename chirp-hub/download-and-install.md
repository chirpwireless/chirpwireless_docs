---
description: Download Chirp Hub for Windows, Mac, Linux or a Raspberry Pi, install it, and get past the warning on first launch.
---

# How Do I Download and Install Chirp Hub?

**Setting up a Raspberry Pi?** Skip this page and go to the [Raspberry Pi guide](raspberry-pi/README.md). The Pi needs some preparation first, and the guide includes the download.

On a Windows, Mac or Linux computer, start here. Chirp Hub is free. Every release has one download page with an installer for each operating system:

**[Download Chirp Hub 0.1.1](https://github.com/chirpdepin/raspberry-pi-iot-hub/releases/tag/chirp-v0.1.1)**

Install it on the Raspberry Pi or PC that stays at home, not on a laptop you carry around. Your cameras record, your Zigbee network runs and your gateway listens only on the computer where Chirp Hub is installed, and only while that computer is on.

## Which Chirp Hub installer do I download?

On the release page, scroll down to **Assets** and pick the file for your computer. The version number is part of each file name.

| Your computer | File to download |
|---|---|
| Windows 10 or 11 (64-bit) | `Chirp-Hub-Setup-<version>.exe` |
| Mac with Apple silicon (M1 or newer) | `Chirp-Hub-<version>-arm64.dmg` |
| Mac with an Intel processor | `Chirp-Hub-<version>.dmg` |
| Ubuntu or Debian computer | `chirp-hub_<version>_amd64.deb` |
| Raspberry Pi with 64-bit Ubuntu (see the [Raspberry Pi setup](raspberry-pi/setup.md)) | `chirp-hub_<version>_arm64.deb` |
| Any other Linux | `Chirp-Hub-<version>.AppImage` for a regular 64-bit PC, `Chirp-Hub-<version>-arm64.AppImage` for an ARM board |

You can ignore the `.yml` and `.blockmap` files on that page. They aren't installers.

## What is Docker, and do I need it?

Docker is a free program that runs other programs in their own sealed-off boxes, called containers. Chirp Hub uses it to run the recorder for each of your cameras. You only need Docker for cameras, and you don't have to install it in advance: when you add your first camera, Chirp Hub offers to install or start it for you.

## How do I install Chirp Hub on Windows?

1. Download `Chirp-Hub-Setup-<version>.exe` and run it.
2. If Windows shows **Windows protected your PC**, choose **More info** and then **Run anyway**. That's because Windows doesn't know who publishes Chirp Hub yet and wants your OK. You only see it once.
3. Go through the installer. When it finishes, Chirp Hub opens, and you'll find it in the Start menu from then on.

When you add your first camera and Docker Desktop isn't on your PC yet, Chirp Hub downloads and installs it for you. You only need to approve the administrator prompt.

## How do I install Chirp Hub on a Mac?

1. Download the `.dmg` that matches your Mac's processor and open it.
2. Drag **Chirp Hub** into **Applications**. Always start it from Applications, not from the disk image.
3. The first time you open it, macOS stops it, because it doesn't know who publishes Chirp Hub yet and wants your OK. On macOS 15 or newer, open **System Settings → Privacy & Security** and choose **Open Anyway** next to Chirp Hub. On an older macOS, find Chirp Hub in Applications, right-click it and pick **Open**.
4. macOS then asks whether Chirp Hub may find devices on your local network. Choose **Allow**. If you don't, Chirp Hub can't see your cameras.

On macOS 13 and newer, Chirp Hub sets up a Docker of its own when you add your first camera. It's about a 400 MB download, it doesn't ask for a password, and nothing new shows up in Applications. If you already use Docker for something else, it's left alone.

## How do I install Chirp Hub on Linux or a Raspberry Pi?

On Ubuntu or Debian, install the `.deb` package. It brings everything Chirp Hub needs along with it:

```sh
sudo apt install ./chirp-hub_<version>_amd64.deb
```

On a Raspberry Pi, follow the [setup page](raspberry-pi/setup.md) instead. It runs the [setup script](raspberry-pi/setup.md#how-do-i-get-the-pi-ready-for-the-lorawan-card-and-radios) first and then installs the `arm64` package, and after a restart the Pi opens Chirp Hub by itself.

On any other Linux, use the AppImage:

```sh
chmod +x Chirp-Hub-<version>.AppImage
./Chirp-Hub-<version>.AppImage
```

If the AppImage doesn't start, install `libfuse2` with your package manager. On Ubuntu 24.04 the package is called `libfuse2t64`.

If Docker isn't installed when you add your first camera, Chirp Hub installs Docker Engine for you and asks for your password in the system's password window.

## How do I update Chirp Hub?

Download the newer installer from the project's [releases page](https://github.com/chirpdepin/raspberry-pi-iot-hub/releases). The Chirp Hub files are the ones whose names start with `Chirp-Hub` or `chirp-hub`. Install it over the old version, the same way you did the first time.

Updating doesn't touch your cameras, your Zigbee network or your paired devices. They're saved in Chirp Hub's data folder, not inside the program itself.

To be sure the update worked, check the version on the **Settings** page before and after.

Next: building on a Raspberry Pi? Read [How Do I Turn a Raspberry Pi into a Smart Home Hub?](raspberry-pi/README.md) Using a PC or Mac? Read [How Do I Run Chirp Hub on Windows, Mac or Linux?](computer.md)
