---
description: Fix a Raspberry Pi hub that won't work, from a LoRaWAN card it can't find to Zigbee that refuses to start.
---

# Why Is My Raspberry Pi Hub Not Working?

When a Raspberry Pi hub misbehaves, the cause is usually a part that isn't seated properly, a step that got skipped, or a power supply that can't keep up. Find the section that matches what you're seeing and follow it.

## What if the setup script says the concentrator did not answer?

When the setup script can't reach the RAK5146 card, it stops with **FAILED: the concentrator did not answer**. The problem is in the hardware, not the software.

1. Run `sudo poweroff`, wait until the green light goes out, then unplug the power.
2. Make sure the card is pushed all the way into the HAT's mPCIe slot and held down by its screw.
3. Make sure the HAT is fully seated on the Pi's 40-pin header, with no row of pins sticking out of the socket.
4. Make sure the antenna is attached to the card's LoRa connector.
5. Power the Pi back on and run `sudo ./scripts/install-ubuntu.sh --with-desktop` once more.

To test the card on its own, run the commands below on the Pi. If the card responds, the second command prints its gateway ID:

```sh
sudo concentrator-reset start
cd /opt/iot-hub/src/sx1302_hal && sudo util_chip_id -d /dev/spidev0.0
```

## Why does Chirp Hub say there is no LoRaWAN radio?

The LoRaWAN Gateway page shows **No LoRaWAN radio on this computer** when the setup script never ran on this Pi, or quit before it reached the card. Run [the script](setup.md#how-do-i-get-the-pi-ready-for-the-lorawan-card-and-radios) again and let it finish; once it prints the gateway ID, restart the Pi.

## Why won't my gateway connect to Chirp?

Chirp Hub reports what it sees on the Pi; Chirp tells you whether the gateway is connected.

* Chirp Hub shows **This gateway is set up and running.**, yet Chirp lists the gateway as offline: compare the LNS address in Chirp Hub with the one Chirp lists for this gateway, and check that the gateway's registered region matches the band of your card and antenna. Also confirm the Pi can reach the internet.
* **This gateway is set up but not running.**: click **Start gateway**.
* **This gateway is only part-way set up.**: pick all three files again and click **Save**.
* **This device's gateway folder is not safe to write to, so nothing was changed.**: the folder holding the gateway's settings wasn't made by the setup script. Run the script again.

## Why won't Zigbee start?

* **No Zigbee coordinator found.**: plug in the dongle, ideally with a USB extension cable, and give it a few seconds.
* **Radios needing a decision**: Chirp Hub sees more than one radio. Click **Use for Zigbee** on your Zigbee dongle.
* **Zigbee didn't come up.**: unplug the dongle, plug it in again and click **Start Zigbee** once more. Still stuck? Restart the Pi.
* **Zigbee on this device was set up with a different kind of dongle.**: the network belongs to a different dongle. Plug the original one back in and your paired devices stay.

## Why does Chirp Hub ask for a password?

Chirp Hub asks for the Pi's password, the one you chose in Raspberry Pi Imager, each time it changes something on the system: installing the gateway certificates, starting or restarting the gateway, starting Zigbee for the first time, or assigning a radio its role. Clicking **Cancel** leaves everything as it was. The password isn't saved, so the next change asks for it again.

## Why is my Pi slow or my cameras stopping?

* Check the Dashboard's **Processor load** and **Memory used**. Six or seven cameras is about the most a Raspberry Pi 4 can record, so put any extras on [Chirp Hub running on a computer](../computer.md).
* A Pi that runs hot slows itself down. Choose a case with a fan or open vents, and don't shut it away inside a metal cabinet.
* If the Pi keeps restarting at random, the power supply is usually too weak. Use the official one for your Pi model.

## Where do I find the logs for support?

In Chirp Hub, open **Settings** and click **Open log folder** or **Copy system details** to share them with support.
