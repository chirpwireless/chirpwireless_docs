---
description: Start a Zigbee network with Chirp Hub, pair sensors, plugs and bulbs around the house, and open Zigbee2MQTT.
---

# How Do I Pair Zigbee Devices with Chirp Hub?

Chirp Hub makes a USB Zigbee coordinator into a working Zigbee network for your home. It identifies the dongle, chooses the matching radio driver, gives your network a security key of its own, runs Zigbee2MQTT and a small local message broker, and opens a pairing window whenever you add a device. Zigbee works on a Raspberry Pi and on Linux computers.

## Why set up Zigbee with Chirp Hub?

Setting up Zigbee2MQTT yourself means finding the dongle's serial port and the driver for its chip, creating a network key, running a broker and writing a settings file. Pick the wrong driver and the error message gives you no useful clue. Chirp Hub reads all of that from the dongle itself, keeps it working after a restart or when you plug in other USB gadgets, and creates a fresh network key for every home rather than one shared default.

## Which Zigbee coordinators does Chirp Hub recognize?

Chirp Hub knows the popular USB coordinator families and picks the driver itself:

* **Silicon Labs EFR32 chips (EmberZNet):** ZBDongle-E and Zigbee Dongle Plus MG24 from SONOFF, ZBT-1 and SkyConnect from Home Assistant, SLZB-07 and SLZB-06MU from SMLIGHT
* **Texas Instruments CC2652 / CC1352 chips:** ZBDongle-P from SONOFF, SLZB-07P and SLZB-06P from SMLIGHT
* **dresden elektronik:** ConBee and RaspBee
* **Nordic nRF52840:** dongles running ZBOSS

Plug in the dongle before you open the **Zigbee** page. If it's the only coordinator, Chirp Hub uses it for Zigbee on its own. If two or more are plugged in, say a Zigbee dongle and a Thread radio, Chirp Hub won't guess, and they appear under **Radios needing a decision**. Click **Use for Zigbee** on the one meant for Zigbee. Chirp Hub remembers it by its serial number, so it keeps that job after restarts and in whichever USB port you use. If no coordinator turns up, the page shows **No Zigbee coordinator found. Plug in a supported USB dongle and it will appear here.**

## How do I start the Zigbee network?

1. Open **Chirp Hub** and choose **Zigbee** in the left menu. The **Coordinator** table lists the dongle, its **Connection** (USB) and its **Type** (driver).
2. Click **Start Zigbee**. Chirp Hub brings the network up and waits for it to report that it's online, which can take up to a minute the first time.
3. **Zigbee started.** means your network is up. Any devices you paired before show in the **Devices** table.

<figure><img src="../.gitbook/assets/chirp-hub-zigbee.jpg" alt="Chirp Hub Zigbee page with the coordinator and a paired lamp connected to the hub"><figcaption><p>Your coordinator and every paired device, with its signal and battery, on one page.</p></figcaption></figure>

If the network is already running, **Start Zigbee** gives it a clean restart. That's the first thing to try when devices stop answering.

## How do I pair a Zigbee device?

1. Click **Add device**. Your network starts accepting new devices, and a countdown shows how long it stays open.
2. While **Searching for new devices…** is on screen, put your device into pairing mode. Most sensors have a button you hold down for a few seconds; a smart bulb usually needs switching off and on five times in a row until it blinks. Your device's manual has the exact steps.
3. Once it joins, the device is listed in the **Devices** table, showing its name, **Type**, **Status**, **Signal** and **Battery**. A green **Connected to hub** tells you it has joined your Zigbee network.
4. Click **Stop searching** once everything is paired, or just let the countdown finish. Either way, the network stops accepting new devices.

<figure><img src="../.gitbook/assets/chirp-hub-zigbee-pairing.jpg" alt="Chirp Hub pairing window counting down while it searches for new Zigbee devices"><figcaption><p>Put your device into pairing mode while the countdown runs.</p></figcaption></figure>

If the network isn't running yet, **Add device** asks you to start Zigbee first.

## How do I open the Zigbee2MQTT dashboard?

Zigbee2MQTT comes with a dashboard of its own. There you can rename devices, see every value they send, switch lights and plugs on and off, update firmware and view a map of your network. Chirp Hub opens it for you.

1. Click **Open Zigbee2MQTT**, and the dashboard opens in a browser tab.
2. On your first visit the dashboard shows **Auth** and asks for a **Token**. Chirp Hub displays the token under **Zigbee2MQTT is open in your browser.** — click **Copy** and paste it in. Your browser remembers it from then on.

<figure><img src="../.gitbook/assets/chirp-hub-zigbee-dashboard-token.jpg" alt="Chirp Hub showing the Zigbee2MQTT address and its access token with a Copy button"><figcaption><p>Chirp Hub shows where the dashboard is and the token it wants on your first visit.</p></figcaption></figure>

Each home gets a token of its own, and only the computer running Chirp Hub can reach the dashboard.

## How does Zigbee work on a Raspberry Pi hub?

If your Pi went through the [setup script](raspberry-pi/setup.md), Zigbee runs as a background service on the Pi itself:

* The first time you click **Start Zigbee**, Chirp Hub asks for the Pi's password once, to give the dongle its Zigbee role and create the network settings.
* From then on, the network starts on its own every time the Pi boots, whether a screen is connected or not.
* The dongle's role is tied to its serial number, so you can move it to a different USB port.

## How do I get a strong Zigbee network at home?

* Pair each device in the spot where it will live. Zigbee builds its mesh through plugged-in devices such as smart plugs and bulbs, so set those up first and battery sensors afterwards.
* Connect the coordinator with a short USB extension cable, keeping it clear of USB 3 ports and the computer's Wi-Fi.
* In the Zigbee2MQTT dashboard, give devices names the whole family understands, like "Kitchen plug" or "Basement leak sensor". Chirp Hub shows those same names.
