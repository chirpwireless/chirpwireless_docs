---
description: Put your Raspberry Pi home hub together, plug in radios and cameras, and fit the LoRaWAN card only if you want one.
---

# How Do I Assemble a Raspberry Pi Smart Home Hub?

You'll need a small screwdriver and roughly a quarter of an hour. Keep the Pi unplugged until the very last step.

What you do depends on the parts you bought. The first two sections are only for a LoRaWAN gateway, where you fit the concentrator card and the Pi HAT. No gateway? Go straight to [putting the hub in its case](#how-do-i-put-the-hub-in-its-case).

## How do I fit the LoRaWAN card to the Pi HAT?

Only for a LoRaWAN gateway. Connect the antenna before the Pi ever gets power with the card fitted.

1. Tilt the RAK5146 card a little and push its gold contacts fully into the HAT's mPCIe slot.
2. Lay the card flat against the HAT and screw it to the standoff, the small metal post on the HAT that holds the card up.
3. Clip the antenna cable onto the card's **LoRa** antenna connector. The card has two small round connectors. Use the one that is *not* marked GPS, and press straight down until it clicks.
4. If you bought a GPS antenna, clip it onto the connector marked **GPS**. GPS gives the gateway exact time and location, but the gateway works fine without it.

<figure><img src="../../.gitbook/assets/chirp-hub-rak5146-pi-hat-kit.png" alt="RAK5146 concentrator card beside the Pi HAT, with the mPCIe slot the card slides into"><figcaption><p>The card slides into the mPCIe slot on the HAT and is held by one screw.</p></figcaption></figure>

{% hint style="warning" %}
Never power on the Pi with the concentrator card fitted and no antenna connected. A LoRa radio that sends without an antenna can damage itself.
{% endhint %}

## How do I mount the Pi HAT on the Raspberry Pi?

Only for a LoRaWAN gateway.

1. Screw the standoffs that came with the HAT into the four mounting holes on the Pi. These are small posts that keep the HAT at the right height above the Pi.
2. Place the HAT so its 40-pin socket sits over the Pi's 40 pins, then push down evenly until it won't go any further. Every pin has to be inside the socket. A HAT that's off by one row won't work.
3. Screw the HAT onto the standoffs with the remaining screws.

## How do I put the hub in its case?

1. Put the Pi into the case, with the HAT on top if you fitted one.
2. If you fitted the LoRaWAN card, push the SMA end of the antenna cable through the antenna hole in the case, tighten its nut, and screw the LoRa antenna onto it from the outside.
3. Close the case. Leave the air vents uncovered.

If you have a LoRaWAN antenna, stand it upright, as high as you can and away from metal. Range depends far more on the antenna's position than on the gateway hardware. The top of a bookshelf works much better than the back of a metal cabinet.

## How do I connect the Zigbee and Thread radio sticks?

1. Plug the Zigbee stick into a USB port **using a short USB extension cable**.
2. Got a Thread stick too? Give it its own USB port and its own extension cable, and keep it a little way from the Zigbee stick.
3. Use the black USB 2 ports if you can. The USB 3 ports and their cables interfere with 2.4 GHz radios.

## How do I connect my cameras?

1. Connect each IP camera to the same home network as the Pi. If a camera gets its power through the network cable, plug it into a PoE switch or a PoE injector.
2. Write down each camera's username and password. The camera's recorder asks for them later, when you point it at the camera's video.

## How do I connect the Raspberry Pi itself?

Stop here for now. The microSD card isn't ready yet: you prepare it on the next page, and that page tells you when to put it in and plug everything in.

When you get there, you'll plug in the network cable, a screen, a keyboard and a mouse for the first setup, and the power supply last. The Pi starts as soon as it gets power.

Next: [How Do I Set Up a Raspberry Pi for Chirp Hub?](setup.md)
