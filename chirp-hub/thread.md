---
description: Add a Thread radio to Chirp Hub for Matter devices at home, and see why Thread needs a USB radio beside Zigbee.
---

# How Do I Add Thread to Chirp Hub?

Thread is the low-power mesh network that Matter smart home devices rely on: sensors, door locks, blinds and bulbs from lots of brands. Just like Zigbee, it needs a radio in your home, and on a Raspberry Pi, Chirp Hub runs the Thread border router that this radio works with.

## Why does Thread need its own radio?

Zigbee and Thread run on the same 2.4 GHz radio chips but need different firmware, and a dongle can only run one of them at a time. If your home uses both, you need two USB radios: one with Zigbee coordinator firmware for your [Zigbee](zigbee.md) network and one with Thread firmware. Chirp Hub keeps them separate, so your Thread radio never gets confused with the Zigbee coordinator, and the other way round.

## What radio does Thread need?

Pick a USB radio running OpenThread radio co-processor (RCP) firmware, such as a second Silicon Labs MG24 or a Nordic nRF52840 dongle. Lots of dongles sold for Zigbee can be reflashed for Thread; their maker provides the firmware and instructions for flashing it.

## How do I set up Thread on a Raspberry Pi?

If you prepared your Raspberry Pi with the [setup script](raspberry-pi/setup.md#how-do-i-get-the-pi-ready-for-the-lorawan-card-and-radios), the Thread border router (OpenThread) is installed already. It starts automatically as soon as a radio has been given the Thread role.

1. Plug the Thread radio into a USB port, beside the Zigbee coordinator if you have one.
2. Look up its USB serial number: run `ls /dev/serial/by-id` and take the long code at the end of the radio's name.
3. Give it the Thread role, just once:

   ```sh
   sudo iot-hub-radio-assign <usb-serial> thread
   ```

   The command makes sure the radio is plugged in and isn't already your Zigbee radio, sets it up as the Thread radio, and the border router starts. Because the role follows the serial number, it sticks through restarts and port changes.
4. Open **Chirp Hub** and choose **Thread** in the left menu. You see **Thread radio found.**

Without a Thread radio, both the Thread page and the Thread card on the Dashboard tell you that **Thread needs its own radio**, since a single dongle can't run Zigbee and Thread together.

<figure><img src="../.gitbook/assets/chirp-hub-thread-no-radio.jpg" alt="Chirp Hub Thread page saying that Thread needs its own radio"><figcaption><p>With no Thread radio plugged in, the page reminds you that Zigbee and Thread each need their own.</p></figcaption></figure>

Chirp Hub can't use USB radios on Windows or macOS, so Thread needs a Raspberry Pi.

## How do I avoid mixing up my Zigbee and Thread radios?

* Put a label on each dongle. They often look exactly alike, and plugging in the Zigbee one where the Thread one should be is the usual reason the Thread page can't find a radio.
* Use short USB extension cables for both, and keep them a little apart from each other and from the computer's Wi-Fi antenna.
