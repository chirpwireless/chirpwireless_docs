---
description: Run Chirp Hub on a Windows, macOS or Linux computer at home to record lots of cameras and, on Linux, run Zigbee too.
---

# How Do I Run Chirp Hub on Windows, Mac or Linux?

Chirp Hub works on a regular Windows, macOS or Linux computer, not only on a Raspberry Pi. Installed on a computer, it becomes the hub of your home: a desktop in the study or a mini PC beside the router that records every camera in the house and runs your local radios, with far more power than a tiny single-board computer.

## When is a computer better than a Raspberry Pi for my home?

Go with a computer when you have more cameras than a Raspberry Pi can keep up with. A Raspberry Pi 4 manages about six or seven cameras; on a computer, the only limits are its processor, memory and network. Plenty of homes already have a PC that is never turned off, and putting Chirp Hub on it means there's no extra box to buy.

A computer can't act as a LoRaWAN gateway, because there's nowhere to fit a concentrator card. If your home uses LoRaWAN sensors, run a [Raspberry Pi LoRaWAN gateway](raspberry-pi/lorawan-gateway.md) or a [compatible LoRaWAN gateway](../gateways/lorawan-gateways/compatible-lorawan-gateways.md) alongside the computer.

## What does Chirp Hub run on each operating system?

| Capability | Windows | macOS | Linux |
|---|---|---|---|
| Cameras | Yes | Yes | Yes |
| Zigbee (USB coordinator) | No | No | Yes |
| Thread border router | No | No | No — Raspberry Pi only |
| LoRaWAN gateway | No | No | No — Raspberry Pi only |

Windows and macOS run Docker inside a virtual machine that USB radios can't get through to, which is why Zigbee works only on Linux. The Thread border router is part of the Raspberry Pi setup. On Windows and macOS, the Zigbee page tells you this up front rather than asking for a dongle that would never work there.

## How do I set up a computer as my home hub?

1. [Download and install Chirp Hub](download-and-install.md) for your computer's operating system.
2. Open Chirp Hub. The **Dashboard** lists the computer's operating system, memory, processors and Docker version.
3. Add your cameras from **Cameras** ([Cameras](cameras.md)). No Docker yet? Chirp Hub installs it when you add your first camera.
4. On Linux, plug in your Zigbee coordinator and create the network from **Zigbee** ([Zigbee](zigbee.md)).
5. Watch **Processor load** and **Memory used** on the Dashboard as more cameras join.

## How do I keep the computer recording all the time?

* Switch off sleep mode and any automatic shutdown. Cameras record only while the computer is on.
* Keep the computer in one spot and connect it to the router with a cable, since the cameras send video to it nonstop.
* On Windows and macOS, leave Docker open. When Docker stops, Chirp Hub's cameras stop with it.
