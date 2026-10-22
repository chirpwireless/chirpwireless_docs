---
description: Turn a Raspberry Pi into an affordable smart home hub for cameras, Zigbee and Thread, plus LoRaWAN if you like.
---

# How Do I Turn a Raspberry Pi into a Smart Home Hub?

Put Chirp Hub on a Raspberry Pi and you get a small, low-cost hub that lives in your home and covers jobs that normally take three or four boxes. Plug in a Zigbee dongle and let it find your IP cameras, and one Pi becomes your camera recorder and smart home radio. Want it to be your LoRaWAN gateway too? Fit a LoRaWAN card and an antenna. You set all of it up from one app, with no terminal session for each device.

## What problem does a Raspberry Pi hub solve at home?

A smart home tends to pile up boxes:

* a **LoRaWAN gateway** on a shelf for the battery sensors in the basement and the garden,
* a **video recorder (NVR)** in a closet for the cameras,
* a **Zigbee bridge** for smart plugs, bulbs and door sensors,

and each one is bought, plugged in, connected and updated on its own. In a house or a holiday rental with a few sensors and a couple of cameras, those boxes end up eating most of what you spend.

A Raspberry Pi hub swaps them for one device that uses a few watts, fits on a bookshelf or in a closet and is run from a single window. The parts cost far less than a store-bought gateway plus an NVR, and each part is a standard component you can swap out by itself.

## What does a Raspberry Pi hub do?

| Capability | What it does | Hardware it needs |
|---|---|---|
| **LoRaWAN gateway** | Receives your LoRaWAN sensors' readings and passes them, over an encrypted Basics Station connection, to the LoRaWAN Network Server built into Chirp | Only if you want it: RAKwireless Pi HAT, RAK5146 concentrator card, LoRa antenna |
| **Cameras** | Finds the IP cameras in your home and runs a recorder for each, so video is saved in the house and ready to link with Chirp Lens | IP cameras on your home network |
| **Zigbee** | Runs a Zigbee network for sensors, plugs and bulbs, which you pair from the app | USB Zigbee coordinator |
| **Thread** | Runs a Thread border router for Matter devices | A second USB radio flashed with Thread firmware |

A Raspberry Pi 4 records about **six or seven cameras**, even with Zigbee and a gateway running too, and a Raspberry Pi 5 copes with more. As you add cameras, Chirp Hub shows how much room is left.

Choose just what your home needs: only cameras, only Zigbee, a LoRaWAN gateway, or a mix. Anything else can come later.

## When is a computer the better choice?

Got more cameras than one Pi can record? Let a computer running Chirp Hub take care of them, as described in [Windows, Mac and Linux](../computer.md). There, the number of cameras depends only on the computer's processor, memory and network. Want a LoRaWAN gateway as well? That job stays with the Pi, since computers don't take a LoRaWAN card.

## How do I build a Raspberry Pi hub, step by step?

1. **Shop for the parts** — [What Parts Do I Need for a Raspberry Pi Hub?](shopping-list.md)
2. **Put it together** — [How Do I Assemble a Raspberry Pi Smart Home Hub?](hardware.md)
3. **Prepare the Pi and install Chirp Hub** — [How Do I Set Up a Raspberry Pi for Chirp Hub?](setup.md)
4. **Turn on each capability:**
   * the LoRaWAN gateway, if you fitted the card — [How Do I Use a Raspberry Pi as a LoRaWAN Gateway?](lorawan-gateway.md)
   * cameras — [How Do I Connect Home IP Cameras to Chirp Hub?](../cameras.md)
   * Zigbee — [How Do I Pair Zigbee Devices with Chirp Hub?](../zigbee.md)
   * Thread — [How Do I Add Thread to Chirp Hub?](../thread.md)
5. **If something won't start** — [Why Is My Raspberry Pi Hub Not Working?](troubleshooting.md)

Allow about an hour for your first hub. Most of that time goes on waiting while the operating system downloads and the setup script runs.

## How do I keep my Raspberry Pi hub happy?

* Put the hub together and test it on your desk or the kitchen table before moving it to its final spot.
* Connect it to your router with a network cable. Cameras send video all the time, and a gateway on Wi-Fi goes offline whenever your Wi-Fi does.
* Give the Pi some air. Shut inside a cupboard, it slows down once the cameras get busy, and you'll see a high **Processor load** on the Dashboard.
