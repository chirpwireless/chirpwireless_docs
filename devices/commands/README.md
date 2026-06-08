---
description: Control your smart home devices from Chirp — turn things on and off, dim lights, change color temperature, and send settings to any device that can receive commands.
---

# Controlling Your Devices

Up to now, Chirp has mostly listened — gathering readings from your sensors and showing them on your dashboards. **Commands** flip that around. They let Chirp *talk back* to your devices, so the same app that tells you the living room is chilly can also turn the heater on.

If a device can be told to do something, Chirp can do it for you: flick a smart plug on or off, dim the bedroom lights to 30%, warm a bulb's color temperature for movie night, nudge a thermostat to a new target, or send a setting to almost anything in your home. It works whether your device connects over Zigbee/MQTT or LoRaWAN — you don't have to think about the plumbing.

## Why you'll love it

Before, controlling a smart device usually meant juggling apps — one for the lights, another for the plugs, a third for the thermostat. Chirp brings the controls into the same place you already watch your home:

* **One home, one place to control it.** Define what a device can do once, then operate it with a tap — no fiddling with technical settings every time.
* **Tap-friendly controls.** You see a simple, friendly action ("Turn on", "Set brightness") — Chirp handles the messy details behind the scenes.
* **Know it actually happened.** Chirp can check that the device really responded, not just that the message was sent (see [Making sure it worked](verification.md)).
* **A tidy history.** Every action you send is logged, so you can always see what changed and when.

## Where to find it

Open a device, and look for the **Commands & States** tab. It has two parts:

* **Commands** — where you set up the actions a device can do. See [Setting up a command](creating-commands.md).
* **States** — where you actually press the buttons and see what happened. See [Sending a command](executing-commands.md).

You'll see the **Commands & States** tab on devices that can be controlled:

* **Smart home devices connected over MQTT** — most Zigbee devices (through Zigbee2MQTT), DIY ESP32 builds, Tasmota plugs, and similar.
* **Class C LoRaWAN devices** — these listen all the time, so they're always ready to receive a command. (Battery-saving Class A LoRaWAN sensors only wake briefly, so they can't be controlled on demand.)

Once a device has at least one command set up, it becomes *controllable* — and you can also drop it onto a dashboard as a [Control widget](../../dashboards/adding-widgets/control-widget.md).

## Before you start

To control a device, you'll want:

1. **A device that can receive commands** — connected over MQTT, or a Class C LoRaWAN device.
2. **At least one command set up** — a brand-new device has no actions yet. Start with [Setting up a command](creating-commands.md).
3. **Permission to control it** — managing and sending commands follows your home's sharing settings.
4. **Sensible values** — if a command takes an input (like a brightness level), it has to be within the allowed range before Chirp will send it.

## Three ways to control a device

Commands are the foundation. They show up in a few places:

* **On the device** — open it, go to **States**, and press a command.
* **On a dashboard** — add a [Control widget](../../dashboards/adding-widgets/control-widget.md) so a light switch or button sits right next to your readings.
* **Through automations** — let the [Rules engine](../../rules-engine/) react to what's happening and send the right alert at the right time.

Ready? Head to [Setting up a command](creating-commands.md).
