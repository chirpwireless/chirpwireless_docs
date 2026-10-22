---
description: Fix a Raspberry Pi hub that isn't working, from a LoRaWAN card the setup script can't find to Zigbee that won't start.
---

# Why Is My Raspberry Pi Hub Not Working?

When a Raspberry Pi hub misbehaves, it's usually one of three things: a part that isn't pushed in all the way, a step that got skipped, or a power supply that's too weak. Find the message or problem you're seeing below and follow the steps.

## Why does the setup script say no LoRaWAN card was found? {#what-if-the-setup-script-says-the-concentrator-did-not-answer}

You fitted a LoRaWAN card, but at the end the setup script says **No LoRaWAN card found, so this Pi is not set up as a LoRaWAN gateway.** Everything else was installed. Only the gateway part was skipped.

1. **Restart first if the script asked you to.** If the script also said **A reboot is required to finish**, the card's connection may not be switched on yet. Run `sudo reboot`, sign in again and run `sudo ./scripts/install-ubuntu.sh --with-desktop` once more.
2. **Still not found? Check the hardware.** Run `sudo poweroff`, wait until the green light goes out, and unplug the power. Then:
   * make sure the card is pushed all the way into the mPCIe slot on the Pi HAT and held down by its screw;
   * make sure the HAT sits fully on the Pi's 40-pin header, with no row of pins showing outside the socket;
   * make sure the antenna is connected to the card's LoRa connector.
3. Plug the power back in and run `sudo ./scripts/install-ubuntu.sh --with-desktop` again.

To check the card on its own, run these commands on the Pi. If the card answers, the second command prints its gateway ID:

```sh
sudo concentrator-reset start
cd /opt/iot-hub/src/sx1302_hal && sudo util_chip_id -d /dev/spidev0.0
```

If you don't have a LoRaWAN card, that message is expected and nothing is wrong. Your Pi works for cameras, Zigbee and Thread.

## Why does Chirp Hub say there is no LoRaWAN radio?

On a Pi without a LoRaWAN card, that's expected: the LoRaWAN Gateway page says **No LoRaWAN radio on this computer. LoRaWAN needs a concentrator such as a RAK5146 on a Raspberry Pi HAT.** You can ignore it.

If your Pi does have a card, the setup script either never ran on this Pi or didn't find the card. Run [the script](setup.md#how-do-i-get-the-pi-ready-for-the-lorawan-card-and-radios) again and let it finish. When it prints the gateway ID, restart the Pi. If it says no LoRaWAN card was found, follow the [steps above](#what-if-the-setup-script-says-the-concentrator-did-not-answer).

## Why won't my gateway connect to Chirp?

Chirp Hub tells you what it sees on the Pi. Chirp tells you whether the gateway has actually connected.

* Chirp Hub says **This gateway is set up and running.**, but Chirp shows the gateway as offline: check that the LNS address in Chirp Hub matches the one Chirp shows for this gateway, and that the region you registered matches the band of your card and antenna. Also check that the Pi is connected to the internet.
* **This gateway is set up but not running.**: select **Start gateway**.
* **This gateway is only part-way set up.**: choose all three files again and select **Save**.
* **This device's gateway folder is not safe to write to, so nothing was changed.**: the folder that holds the gateway's settings wasn't created by the setup script. Run the script again.

## Why won't Zigbee start?

* **No Zigbee coordinator found.**: plug in the Zigbee stick, ideally on a USB extension cable, and wait a few seconds.
* **Radios needing a decision**: Chirp Hub sees more than one radio stick. Select **Use for Zigbee** on your Zigbee stick.
* **Zigbee didn't come up.**: unplug the stick, plug it back in and select **Start Zigbee** again. If that doesn't help, restart the Pi.
* **Zigbee on this device was set up with a different kind of dongle.**: your network was created with another stick. Plug the original stick back in, and your paired devices stay paired.

## Why does Chirp Hub keep asking for a password?

Chirp Hub asks for the Pi's password, the one you chose in Raspberry Pi Imager, every time it changes something on the system: installing the gateway certificates, starting or restarting the gateway, starting Zigbee for the first time, or giving a radio stick its job. If you select **Cancel**, nothing changes. Chirp Hub doesn't save the password, so the next change asks again.

## Why is my Pi slow, or why do my cameras keep stopping?

* Look at **Processor load** and **Memory used** on the Dashboard. A Raspberry Pi 4 can record about six or seven cameras at most. Put any extra cameras on [Chirp Hub running on a computer](../computer.md).
* A Pi that gets too hot slows itself down. Use a case with a fan or open vents, and don't shut it inside a metal cabinet.
* If the Pi restarts at random, the power supply is usually too weak. Use the official power supply for your Pi model.

## Where do I find the logs for support?

In Chirp Hub, open **Settings** and select **Open log folder** or **Copy system details**, and send what you find to support.

Next: once your hub is running, carry on in Chirp. Connect your cameras to Lens in [Connecting a Camera](../../lens/connecting-a-camera.md), and if you set up a gateway, add your sensors in [LoRaWAN Devices](../../devices/lorawan-devices.md).
