---
description: Chirp Hub is free software for your home that sets up IP cameras, Zigbee, Thread and a LoRaWAN gateway for Chirp.
---

# What Is Chirp Hub?

Chirp Hub is the part of Chirp that lives in your house. You install it on a computer that stays at home, such as a Raspberry Pi on a shelf in the hallway closet or the desktop PC in the study. From there it sets up and looks after everything your home devices need locally. That means one recorder per IP camera, your Zigbee network and your Thread radio, plus a LoRaWAN gateway when the Raspberry Pi has a concentrator card fitted.

<figure><img src="../.gitbook/assets/chirp-hub-dashboard.jpg" alt="Chirp Hub Dashboard with this device's details and the status of cameras, LoRaWAN, Zigbee and Thread"><figcaption><p>One look at the Dashboard tells you how busy the computer is and where each capability stands.</p></figcaption></figure>

## Why does Chirp need software in my home?

Some of your devices can only be reached from inside your home network. The camera above the garage door streams video over your home Wi-Fi or cable, a Zigbee door sensor talks to a USB stick, and a LoRaWAN radio card is wired straight into the board it sits on. A program in the house has to keep those connections open: it passes the camera and gateway traffic on to Chirp and keeps your Zigbee and Thread networks running.

Without Chirp Hub you would install every piece by hand: Docker, a separate container for each camera, a Zigbee2MQTT settings file that names the right serial port and radio driver, a local MQTT broker, and certificates for the gateway. Chirp Hub turns all of that into buttons. It spots your hardware, chooses the settings, runs everything in Docker and shows how it's going in a single window, so you can finish the whole setup without typing a command.

## What can Chirp Hub set up?

| Capability | What Chirp Hub does | Where it runs |
|---|---|---|
| **Cameras** | Spots the cameras on your home network and starts a separate recorder ([Twin](../lens/installing-twin.md)) for each one, ready to pair with Chirp Lens | Raspberry Pi and computers |
| **Zigbee** | Detects your USB coordinator, creates a Zigbee network with a security key of its own and opens a window for pairing new devices | Raspberry Pi and Linux computers |
| **Thread** | Runs a Thread border router for Matter devices on a dedicated radio, beside the Zigbee one | Raspberry Pi |
| **LoRaWAN gateway** | Reads the gateway ID off the concentrator card, installs the certificates Chirp issues for it and connects the gateway to Chirp's built-in LoRaWAN Network Server | Raspberry Pi with a concentrator HAT |

Every capability gets its own page in the left menu. When the hardware for one is missing, its page stays in the menu and tells you what to plug in, so an absent radio never looks like something broken.

## Should I run Chirp Hub on a Raspberry Pi or a computer?

Both work. What decides it is which radios you want and how many cameras you have.

* **Raspberry Pi** — a single small box for cameras, Zigbee and Thread, which can also be your LoRaWAN gateway if you fit the card. A Raspberry Pi 4 can record about six or seven cameras. See [Raspberry Pi](raspberry-pi/README.md).
* **Windows, macOS or Linux computer** — more horsepower and therefore many more cameras, which suits a big house with a camera on every side or a holiday rental you keep watch over from afar. A computer has nowhere to plug in a LoRaWAN concentrator card. See [Windows, Mac and Linux](computer.md).

## How do I get started with Chirp Hub?

1. [Download and install Chirp Hub](download-and-install.md) on the computer that will stay at home.
2. Open Chirp Hub. Its **Dashboard** shows the computer (system, memory, processors, Docker version) and where each capability stands.
3. Choose what you want to set up in the left menu, then follow the matching guide: [Cameras](cameras.md), [Zigbee](zigbee.md), [Thread](thread.md) or the [LoRaWAN gateway on a Raspberry Pi](raspberry-pi/lorawan-gateway.md).

Before adding one more camera, glance at the **Processor load** and **Memory used** bars on the Dashboard. They turn orange when the computer is getting full.

## Where do I find Chirp Hub logs?

**Settings**, at the bottom of the left menu, shows which Chirp Hub version you have, the operating system and the kind of device it runs on.

<figure><img src="../.gitbook/assets/chirp-hub-settings.jpg" alt="Chirp Hub Settings page showing the app version, the system and two diagnostics buttons"><figcaption><p>Settings has the version number and the two diagnostics buttons our support team will ask about.</p></figcaption></figure>

* **Open log folder** opens the folder where Chirp Hub keeps its log files.
* **Copy system details** puts the version, the operating system and the hardware details on your clipboard, so you can paste them straight into a message to support.

## How do I keep Chirp Hub running well at home?

* Choose a computer that never gets switched off. Cameras only record, and Zigbee devices only report to the hub, while it is running.
* Connect it to your router with a network cable if you can. Cameras send video around the clock, and a cable keeps the recordings free of gaps.
* Use the language selector at the bottom of the menu to switch between English, German, French, Spanish and Portuguese, and the **Dark** switch to change the theme.
