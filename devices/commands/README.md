---
description: Control your devices from Chirp — turn things on or off, dim lights, or just ask the AI helper to do it for you.
---

# Controlling Your Devices

Up to now, Chirp has mostly listened — gathering readings from your sensors and showing them on your dashboards. **Commands** flip that around. They let Chirp *talk back* to your devices, so the same app that tells you the living room is chilly can also turn the heater on.

If a device can be told to do something, Chirp can do it for you: flick a smart plug on or off, dim the bedroom lights to 30%, warm a bulb's color temperature for movie night, nudge a thermostat to a new target, or send a setting to almost anything in your home. It works whether your device connects over Zigbee/MQTT or LoRaWAN — you don't have to think about the plumbing.

<figure><img src="../../.gitbook/assets/device-command-states.jpg" alt="A device's Commands & States tab, with its commands and recent actions"><figcaption></figcaption></figure>

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
* **Pretend sensors with Support commands switched on** — a [pretend sensor](../pretend-sensors.md) behaves like the real thing, so you can practise the whole business before the hardware turns up.

Once a device has at least one command set up, it becomes *controllable* — and you can also drop it onto a dashboard as a [Control widget](../../dashboards/adding-widgets/control-widget.md).

## Before you start

To control a device, you'll want:

1. **A device that can receive commands** — connected over MQTT, a Class C LoRaWAN device, or a [pretend sensor](../pretend-sensors.md) with commands switched on.
2. **At least one command set up** — a brand-new device has no actions yet. Start with [Setting up a command](creating-commands.md).
3. **Permission to control it** — managing and sending commands follows your home's sharing settings.
4. **Sensible values** — if a command takes an input (like a brightness level), it has to be within the allowed range before Chirp will send it.

## Five ways to control a device

Commands are the foundation, and you can run them from five places:

* **On the device** — open it, go to **States**, and press a command.
* **On a dashboard** — add a [Control widget](../../dashboards/adding-widgets/control-widget.md) so a light switch or button sits right next to your readings.
* **From an automation** — the [Rules engine](../../rules-engine/) can now press a command for you, automatically, the moment something happens. The same command you'd tap yourself gets sent with nobody home — so a leak at 3 a.m. shuts the water off on its own. See [When an Automation Runs a Command](../../rules-engine/reference/automation-runs-a-command.md).
* **By asking the helper** — say *"turn on the lamp"* and your [AI helper](../../ai-assistant/README.md) does it, after showing you what it's about to send and checking afterwards that the device got it. See [Ask It to Turn Things On](../../ai-assistant/let-ai-set-it-up.md).
* **From your own AI app** — connect ChatGPT, Claude or anything else that speaks MCP and ask it the same thing from wherever you already work. See [Your Own AI App](../../api/mcp-server.md).

All five end up in the same place: the commands you set up here, sent the same way, logged the same way.

Alerts still have their place alongside all of them: an automation can act *and* tell you about it — shut the water off **and** send you a heads-up — so the problem's handled and you're never left in the dark.

Ready? Head to [Setting up a command](creating-commands.md).
