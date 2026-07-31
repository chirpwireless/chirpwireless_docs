---
description: Try Chirp before your sensors arrive — pretend sensors that make up their own readings, so your dashboards and alerts are ready on day one.
---

# Emulator Connector

You have ordered a leak sensor. It arrives on Thursday. Until now there was nothing to do until then — no dashboard to arrange, no alert to set up, nothing to look at.

The Emulator fixes that. It gives you **pretend sensors that invent their own readings**, so you can lay out your dashboard, write your alerts, and watch them actually go off — days before anything turns up in the post. And when the real sensor does arrive, you point that same device at it and keep everything you set up.

<figure><img src="../.gitbook/assets/emulator-connector-list.jpg" alt="The Connectors page in Chirp showing an Emulator connection alongside Tracker and LoRaWAN"><figcaption></figcaption></figure>

## Why you would use it

* **To try Chirp properly before buying anything.** Set up the home you are thinking about and see whether it works the way you want.
* **To get everything ready while you wait for delivery.** The fiddly part of a new sensor is not sticking it to the wall — it is deciding what should happen when it reads something. Do that first.
* **To test an alert without ruining a Sunday.** Want to know your leak alert really reaches your phone? You do not have to pour water on the floor. Type the number and watch it fire.

## Setting it up

Go to **Connectors → Add connector** and pick **Emulator**. That's it — there is nothing to fill in, no account to link, no code to copy.

## Creating a pretend sensor

Add a device as usual, then on its **Connection** tab choose **Emulator**. You will be asked for:

* **Device ID** — any name you like, so you can tell your pretend sensors apart.
* **How often it reports** — a number and a unit, like every 10 minutes. Match roughly what the real sensor will do, so your alerts behave realistically.
* **Support commands** — switch this on if you want to practise turning the thing on and off, not just reading from it.
* **Use device preset** — the quick way. Pick a real sensor model and Chirp fills in the readings that model actually sends.

### Starting from a real sensor model

Tick **Use device preset** and choose a model, and you get its genuine set of readings — a multi-sensor gives you temperature, humidity, CO2 and air quality, each with the right kind of value. It saves typing, and it means the names on your dashboard are the ones the real sensor will use when it arrives.

Worth knowing: picking a preset **replaces** anything you typed in by hand, including how often it reports. Choose the preset first, then adjust.

<figure><img src="../.gitbook/assets/emulator-device-metrics.jpg" alt="A pretend sensor set up from a real model, listing its readings and their value types"><figcaption></figcaption></figure>

### Or type the readings yourself

Use **Add device data key** and give each reading a name — `temperature`, `humidity`, whatever you like — and say what kind of value it is. Pick **Float** for anything with a decimal point. A whole-number reading will quietly drop the decimals: type 1.5 and you get 1.

## Making it send something

Open the device's **Emulator** tab and you will see each reading with a box next to it:

* **Save** parks a value there. The sensor keeps reporting it, which is how you hold the basement at 85% humidity while you check your damp alert behaves.
* **Send once** fires a single reading and goes back to normal. This is the one for "does my alert actually work?"

<figure><img src="../.gitbook/assets/emulator-manual-value.jpg" alt="The Emulator tab with a temperature value typed in, ready to send"><figcaption></figcaption></figure>

## When the real sensor arrives

Open the device, go to its **Connection** tab, and change it from **Emulator** to the real connection — then enter the details that came with the sensor.

Everything else stays exactly as you left it: the dashboard, the widgets, the alerts, who gets told. You are swapping out where the numbers come from, nothing else. Your Thursday delivery becomes a five-minute job instead of an evening.

You can go the other way too, putting a real sensor back on the emulator for a moment if you want to test something without waiting for the house to cooperate.

## Copying a pretend sensor

Duplicating a device brings its emulator settings along. Set one room up nicely, copy it for the other five, and rename them.

## Just ask the helper

You do not have to do any of this by hand. Ask your [AI helper](../ai-assistant/) to set up a pretend sensor and it will — choosing a model, creating the device, sending a reading to test an alert, and later switching it over to the real sensor.

> *"Make a pretend temperature sensor for the garage and send a reading of 2 degrees."*

## See also

* [Adding Sensors](../devices/adding-sensors.md) — the normal way, once your hardware is here
* [Rules Engine](../rules-engine/) — the automations you can now build early
* [Alarms](../alarm/) — and the alerts you can finally test properly
