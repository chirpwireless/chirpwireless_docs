---
description: Make a pretend sensor in Chirp that invents its own readings, so your dashboards and alerts are ready before the real one arrives.
---

# Pretend Sensors

You have ordered a leak sensor. It arrives on Thursday. A pretend sensor lets you get everything ready in the meantime — lay out your dashboard, write your alerts, and watch them actually go off — days before anything turns up in the post.

A pretend sensor behaves like a real one in every way that matters. It appears in your sensor list, it reports on a schedule, its readings land on your dashboards, and your alerts fire off them. The only difference is where the numbers come from: Chirp makes them up instead of a device sending them.

<figure><img src="../.gitbook/assets/emulator-device-metrics.jpg" alt="A pretend sensor set up from a real model, listing its readings and their value types"><figcaption></figcaption></figure>

## Before you start

You need an **Emulator** connection. It takes two clicks and there is nothing to fill in — no account to link, no keys to copy. See [Emulator Connector](../connectors/emulator-connector.md).

That's the whole list. No sensor, no gateway, no identifiers off the back of a box.

## Making one

Add a sensor as usual, then on its **Connection** tab choose **Emulator**. You will be asked for:

* **Device ID** — a name of your own, so you can tell your pretend sensors apart. Up to 64 characters, using letters, numbers, spaces, dots, underscores and dashes. It has to be unique across all of Chirp — not just your home — so something like `garage-temp-01` will be accepted where `sensor1` may already be taken.
* **How often it reports** — a number and a unit, like every 10 minutes. Match roughly what the real sensor will do, so your alerts behave realistically. Unlike a real sensor, this genuinely is the schedule — Chirp sends on it.
* **Support commands** — switch this on if you want to practise turning the thing on and off, not just reading from it. See [Controlling Your Devices](commands/README.md).
* **Use device preset** — the quick way. Pick a real sensor model and Chirp fills in the readings that model actually sends.

### Starting from a real sensor model

Tick **Use device preset** and pick from the list of real sensor models, and you get that model's genuine set of readings — a multi-sensor gives you temperature, humidity, CO2 and air quality, each with the right kind of value. It saves typing, and it means the names on your dashboard are the ones the real sensor will use when it arrives.

Worth knowing: picking a preset **replaces** anything you typed in by hand, including how often it reports. Choose the preset first, then adjust.

### Or type the readings yourself

Use **Add device data key** and give each reading a name — `temperature`, `humidity`, whatever you like — and say what kind of value it is. Pick **Float** for anything with a decimal point. A whole-number reading will quietly drop the decimals: type 1.5 and you get 1. See [Data Templates](data-templates.md) for how value types work.

## Making it send something

Open the sensor's **Emulator** tab and you will see each reading with a box next to it:

* **Save** parks a value there. The sensor keeps reporting it, which is how you hold the basement at 85% humidity while you check your damp alert behaves.
* **Send once** fires a single reading and goes back to normal. This is the one for "does my alert actually work?"

<figure><img src="../.gitbook/assets/emulator-manual-value.jpg" alt="The Emulator tab with a temperature value typed in, ready to send"><figcaption></figcaption></figure>

Sending a value counts as changing something, so a household member with view-only access can watch a pretend sensor but cannot push readings into it.

## When the real sensor arrives

Open the sensor, go to its **Connection** tab, and change it from **Emulator** to the real connection — then enter the details that came with it.

Everything else stays exactly as you left it: the dashboard, the widgets, the alerts, who gets told. You are swapping out where the numbers come from, nothing else. Your Thursday delivery becomes a five-minute job instead of an evening.

You can go the other way too, putting a real sensor back on the emulator for a moment if you want to test something without waiting for the house to cooperate.

## Copying one

Copying a sensor gets you part of the way, but not all of it — worth knowing before you set one up carefully and expect five free copies.

The copy arrives with the original's name, its reading rows, its connection and its photos. What it does **not** bring is the pretend setup itself: the readings it invents, how often it reports, and whether it accepts commands all go back to their defaults. Until you set those up again, the copy sits there quietly and sends nothing.

The mapping between raw fields and your data templates does not survive the save either, so redo that on the copy too.

See [Sensor Details](sensor-details.md).

## Just ask the helper

You do not have to do any of this by hand. Ask your [AI helper](../ai-assistant/README.md) to set up a pretend sensor and it will — choosing a model, creating the sensor, sending a reading to test an alert, and later taking it live onto your LoRaWAN connection. Asking the helper to switch a pretend sensor to a tracker or an MQTT sensor is the one part it cannot do for you; do that yourself on the Connection tab.

> *"Make a pretend temperature sensor for the garage and send a reading of 2 degrees."*

## What's next

* [Tracking What Matters](../dashboards/tracking-what-matters.md) — build the dashboard you have been waiting to build
* [Alarms](../alarm/README.md) — and the alerts you can finally test properly
* [Adding Sensors](adding-sensors.md) — the normal way, once your hardware is here
