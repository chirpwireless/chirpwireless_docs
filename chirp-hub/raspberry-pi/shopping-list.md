---
description: "Shopping list for a Raspberry Pi smart home hub: the Pi, then only the extras you want, from cameras to LoRaWAN."
---

# What Parts Do I Need for a Raspberry Pi Hub?

Start with the Raspberry Pi and its basics, then buy only the extras for what you want your hub to do at home. Maybe that's just cameras, or just Zigbee; turning the Pi into a LoRaWAN gateway is another extra you can pick. Everything is a standard part you can buy online.

## What do I need for the Raspberry Pi itself?

| Part | What to buy | Why |
|---|---|---|
| Raspberry Pi | A Raspberry Pi 5 with 4 GB of memory or more, or a Raspberry Pi 4 Model B with 4 GB or 8 GB | Runs Chirp Hub; a Pi 5 handles more cameras than a Pi 4 |
| Power supply | The official Raspberry Pi USB-C power supply that matches your board: 27 W (5 V / 5 A) for a Pi 5, 15 W (5 V / 3 A) for a Pi 4 | An underpowered phone charger makes the Pi restart when it gets busy, and that looks like random problems |
| microSD card | 32 GB or more, A2 rated, from a well-known brand | Stores the operating system and the camera recordings; a card made for constant writing lasts longer |
| Case | One with some airflow, ideally with a fan. Building a LoRaWAN gateway? Then pick one tall enough to fit a Pi HAT, with a hole for the antenna connector | Regular Raspberry Pi cases are too short once a HAT is fitted |
| Network cable | Cat 5e or better | A cable to your router keeps the hub and the cameras online when Wi-Fi isn't |
| For setup | A microSD card reader on your computer; then, for the Pi, a screen and HDMI cable (the Pi itself has micro-HDMI ports), a USB keyboard and a mouse | For writing the operating system to the card and for using Chirp Hub on the Pi |

## What do I need to turn my Raspberry Pi into a LoRaWAN gateway?

Only buy these if you want your Pi to pick up LoRaWAN sensors, such as battery sensors in the basement or the garden. Using the hub just for cameras, Zigbee or Thread? Skip this part.

| Part | What to buy |
|---|---|
| Pi HAT | RAKwireless RAK2287/RAK5146 Pi HAT, the adapter board that holds the concentrator card on the Pi's 40-pin header |
| Concentrator card | RAKwireless RAK5146 in mPCIe format, **SPI** version, matching your region's band: 868 MHz for Europe, 915 MHz for North America and Australia. A version with GPS is available if you want it |
| Antenna | A LoRa antenna tuned to that same band, fitted with an SMA or RP-SMA connector |
| Antenna cable | An iPEX (MHF4)-to-SMA pigtail that brings the card's antenna connector out through the case |

Look out for the **RAK5146 Pi HAT kit**, which bundles the HAT and the card so you don't have to match them yourself. RAKwireless and electronics retailers carry all of these parts.

<figure><img src="../../.gitbook/assets/chirp-hub-rak-pi-hat.png" alt="RAKwireless RAK2287/RAK5146 Pi HAT, an adapter board with a 40-pin header and an mPCIe slot"><figcaption><p>The Pi HAT sits on top of the Raspberry Pi and carries the concentrator card.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/chirp-hub-rak5146-card.png" alt="RAKwireless RAK5146 SPI concentrator card in mPCIe format with one LoRa and one GPS antenna connector"><figcaption><p>The RAK5146 card. One connector takes the LoRa antenna, and the other, labeled GPS, takes the optional GPS antenna.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/chirp-hub-rak5146-pi-hat-kit.png" alt="RAK5146 Pi HAT kit with the concentrator card lying next to the HAT"><figcaption><p>The RAK5146 Pi HAT kit comes with the card and the HAT in one box.</p></figcaption></figure>

{% hint style="warning" %}
Match the card and the antenna to the radio band of the country your home is in. You can't change the band afterwards; the rest of the region settings are chosen in Chirp when you register the gateway.
{% endhint %}

## What do I need to connect Zigbee and Thread devices?

Get these if you want smart plugs, bulbs and door sensors on Zigbee, or Matter devices on Thread.

| Part | What to buy | Why |
|---|---|---|
| Zigbee coordinator | Any USB Zigbee dongle Chirp Hub recognizes. Popular picks are SONOFF ZBDongle-E/P or Zigbee Dongle Plus MG24, SMLIGHT SLZB-06/07, Home Assistant Connect ZBT-1 or SkyConnect, and dresden elektronik ConBee | Runs your Zigbee network. The full list is on the [Zigbee](../zigbee.md#which-zigbee-coordinators-does-chirp-hub-recognize) page |
| Thread radio | A second USB radio with OpenThread RCP firmware, such as a Nordic nRF52840 dongle | Thread needs a radio of its own, because one dongle can't run Zigbee and Thread together |
| USB extension cables | Two short ones | Keep each radio clear of the Pi and its USB 3 ports, whose noise disturbs 2.4 GHz signals |

## What do I need to record my IP cameras?

Get these if you want the hub to record your home cameras.

| Part | What to buy |
|---|---|
| IP cameras | Cameras with ONVIF and RTSP support, which most current IP cameras have. A Raspberry Pi 4 manages six or seven of them, and a computer running Chirp Hub manages more |
| Power for the cameras | A PoE switch, or one PoE injector per camera, for cameras that get their power through the network cable |

Electronics retailers stock both.

## How do I start small and add more later?

* Just starting out? Get the Pi basics plus the one thing you want first. Cameras, Zigbee, Thread or the LoRaWAN parts can follow whenever you like.
* Bought the LoRaWAN parts? Hang on to the antenna's box: it shows the band, and you'll need that when you register the gateway in Chirp.
* Next: [How Do I Assemble a Raspberry Pi Smart Home Hub?](hardware.md)
