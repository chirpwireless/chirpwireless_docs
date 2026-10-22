---
description: Use a Raspberry Pi as a cheap, always-on home hub for cameras, Zigbee and Thread, and a LoRaWAN gateway if you like.
---

# How Do I Turn a Raspberry Pi into a Smart Home Hub?

Chirp Hub has to run on a computer that stays at home and never gets switched off. A Raspberry Pi is a good fit for that job. It's an inexpensive little computer, roughly as big as a deck of cards. It uses only a few watts, so it's fine to leave it on day and night, and it fits on a bookshelf.

Put Chirp Hub on a Pi and it becomes the hub for your home: it records your cameras, runs your Zigbee network and, if you want, runs Thread too. If you have LoRaWAN sensors and like to build things yourself, you can also add a radio card and make the same Pi your LoRaWAN gateway.

## Why use a Raspberry Pi as a home hub?

Without a hub, a smart home tends to collect boxes. There's a video recorder for the cameras, a Zigbee bridge for the plugs and bulbs, and maybe a LoRaWAN gateway on a shelf for the battery sensors in the basement and the garden. You buy, plug in, connect and update each one on its own.

A Raspberry Pi with Chirp Hub does all of those jobs from one small box, and you manage everything from one app.

## What can a Raspberry Pi hub do?

You don't need all of these. Pick the ones your home needs and add the rest later.

| What you want | What the Pi does | What you add to the Pi |
|---|---|---|
| **Cameras** | Finds the IP cameras in your home and runs a recorder for each one, so the video is saved at home and ready to link with Chirp Lens | Nothing. The cameras only have to be on your home network |
| **Zigbee** | Runs a Zigbee network for smart plugs, bulbs and sensors, which you pair from the app | A Zigbee USB stick |
| **Thread** | Runs a Thread border router for Matter devices | A second USB radio stick with Thread firmware on it |
| **LoRaWAN gateway** | Only if you build your own gateway instead of buying one: picks up the signals from your LoRaWAN sensors and sends them to Chirp | A Pi HAT (an add-on board that plugs onto the pins along the edge of the Pi), a LoRaWAN concentrator card (the radio itself) and an antenna |

A Raspberry Pi 4 can record about six or seven cameras while doing its other jobs. A Raspberry Pi 5 can record more. As you add cameras, Chirp Hub's Dashboard shows how much room is left.

## Should I make my Raspberry Pi a LoRaWAN gateway too?

Only if you have LoRaWAN sensors, or plan to get some. LoRaWAN is a long-range radio used by small battery sensors, such as a water leak sensor in the basement or a soil moisture sensor at the far end of the garden. Those sensors need a gateway nearby: a receiver that catches their signals and passes them on to Chirp over the internet.

You have two ways to get one:

* **Buy a ready-made LoRaWAN gateway.** This is what most people do. You plug it in, register it in Chirp, and it works without a Raspberry Pi or Chirp Hub. [Compatible Gateways](../../gateways/lorawan-gateways/compatible-lorawan-gateways.md) explains what to look for.
* **Build your own on the Pi.** You add three parts to the Raspberry Pi: a Pi HAT, a concentrator card and an antenna, all listed on the [shopping list](shopping-list.md). Chirp Hub then turns the Pi into a LoRaWAN gateway. This is for you if you enjoy a do-it-yourself project, or if you'd like one box at home that also records your cameras and runs Zigbee.

If you don't have LoRaWAN sensors, or you're buying a ready-made gateway, skip the LoRaWAN parts. Your Pi hub works fine without them, and you can still add them later.

## When is a computer better than a Raspberry Pi?

When you have more cameras than one Pi can record. On a Windows, Mac or Linux computer running Chirp Hub, the number of cameras depends on the computer's processor, memory and network. See [Windows, Mac and Linux](../computer.md).

A computer can't take a LoRaWAN card, so for LoRaWAN sensors you'd add a gateway next to it, as described [above](#should-i-make-my-raspberry-pi-a-lorawan-gateway-too).

## How do I build a Raspberry Pi hub, step by step?

1. **Buy the parts:** [What Parts Do I Need for a Raspberry Pi Hub?](shopping-list.md)
2. **Put it together:** [How Do I Assemble a Raspberry Pi Smart Home Hub?](hardware.md)
3. **Prepare the Pi and install the app:** [How Do I Set Up a Raspberry Pi for Chirp Hub?](setup.md)
4. **Set up what you want to use:**
   * the LoRaWAN gateway, if you added the card: [How Do I Use a Raspberry Pi as a LoRaWAN Gateway?](lorawan-gateway.md)
   * cameras: [How Do I Connect Home IP Cameras to Chirp Hub?](../cameras.md)
   * Zigbee: [How Do I Pair Zigbee Devices with Chirp Hub?](../zigbee.md)
   * Thread: [How Do I Add Thread to Chirp Hub?](../thread.md)
5. **If something doesn't work:** [Why Is My Raspberry Pi Hub Not Working?](troubleshooting.md)

Plan on about an hour for your first hub. Most of that is waiting while Ubuntu downloads and the setup script runs.

## How do I keep my Raspberry Pi hub running well?

* Put the hub together and try it out on your desk or the kitchen table first. Move it to its final spot once everything works.
* Connect it to your router with a network cable. Cameras send video all the time, and a gateway on Wi-Fi drops out whenever your Wi-Fi does.
* Give the Pi some air. Shut away in a cupboard, it slows down when the cameras are busy, and you'll see a high **Processor load** on the Dashboard.

Next: [What Parts Do I Need for a Raspberry Pi Hub?](shopping-list.md)
