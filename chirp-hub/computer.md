---
description: Run Chirp Hub on a Windows, Mac or Linux computer at home to record many cameras and, on Linux, run Zigbee too.
---

# How Do I Run Chirp Hub on Windows, Mac or Linux?

You don't need a Raspberry Pi to use Chirp Hub. It also runs on a regular Windows, Mac or Linux computer, such as the desktop in the study or a mini PC next to the router. That computer then becomes the hub of your home, with a lot more power than a Pi.

## When is a computer better than a Raspberry Pi?

When you have more cameras than a Pi can handle. A Raspberry Pi 4 records about six or seven cameras. A computer can record many more, and the limit is its processor, memory and network. If your home already has a PC that's never switched off, putting Chirp Hub on it also means you don't have to buy anything new.

A computer can't be a LoRaWAN gateway, because there's nowhere to fit the LoRaWAN card. Got LoRaWAN sensors? Most people use a [ready-made LoRaWAN gateway](../gateways/lorawan-gateways/compatible-lorawan-gateways.md) for them. If you like building things, you can instead make a [Raspberry Pi gateway](raspberry-pi/lorawan-gateway.md) to sit alongside the computer.

## What can Chirp Hub do on each operating system?

| What | Windows | macOS | Linux |
|---|---|---|---|
| Cameras | Yes | Yes | Yes |
| Zigbee (USB stick) | No | No | Yes |
| Thread border router | No | No | No, Raspberry Pi only |
| LoRaWAN gateway | No | No | No, Raspberry Pi only |

On Windows and Mac, a USB Zigbee stick can't be used, so Zigbee needs a Pi or a Linux PC. On those systems the **Zigbee** page tells you so up front, instead of asking for a stick. Thread and the LoRaWAN gateway are part of the Raspberry Pi setup only.

## How do I set up a computer as my home hub?

1. [Download and install Chirp Hub](download-and-install.md) for your operating system.
2. Open Chirp Hub. The **Dashboard** shows the computer's operating system, memory, processors and Docker version.
3. Open **Cameras** and add your cameras, as described in [Cameras](cameras.md). If Docker isn't installed yet, Chirp Hub installs it when you add your first camera.
4. On Linux, plug in your Zigbee stick, open **Zigbee** and start your network, as described in [Zigbee](zigbee.md).
5. As you add more cameras, keep an eye on **Processor load** and **Memory used** on the Dashboard.

## How do I keep the computer recording all the time?

* Turn off sleep mode and any automatic shutdown. Cameras only record while the computer is on.
* Keep the computer in one place and connect it to the router with a network cable, since the cameras send it video nonstop.
* On Windows and macOS, keep Docker running. If Docker stops, Chirp Hub's cameras stop with it.

Next: [How Do I Connect Home IP Cameras to Chirp Hub?](cameras.md)
