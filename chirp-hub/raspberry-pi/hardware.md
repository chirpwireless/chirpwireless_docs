---
description: Put together a Raspberry Pi smart home hub. Fit the RAK5146 card to the Pi HAT, add the antenna, case and radios.
---

# How Do I Assemble a Raspberry Pi Smart Home Hub?

Putting the hub together takes around fifteen minutes and a small screwdriver. Keep the Pi unplugged the whole time, and attach the antenna before the Pi ever gets power with the card installed.

## How do I fit the concentrator card to the Pi HAT?

1. Tilt the RAK5146 card slightly and slide its gold edge all the way into the Pi HAT's mPCIe slot.
2. Push the card flat and secure it with the screw on the HAT's standoff.
3. Clip the antenna cable onto the card's **LoRa** antenna connector. It's one of the two small round connectors: use the one *without* the GPS label, and press straight down until it clicks.
4. If you bought a GPS antenna, attach it to the connector labeled **GPS**. GPS gives the gateway precise time and location, but the gateway runs fine without it.

<figure><img src="../../.gitbook/assets/chirp-hub-rak5146-pi-hat-kit.jpg" alt="RAK5146 concentrator card beside the Pi HAT, with the mPCIe slot the card slides into"><figcaption><p>The card slides into the HAT's mPCIe slot and is fixed with a single screw.</p></figcaption></figure>

{% hint style="warning" %}
Don't ever power the Pi while the concentrator card is fitted and the antenna is disconnected. A LoRa radio that transmits with no antenna attached can damage itself.
{% endhint %}

## How do I mount the HAT on the Raspberry Pi?

1. Screw the standoffs supplied with the HAT into the four mounting holes on the Pi.
2. Line up the HAT's 40-pin socket with the Pi's 40-pin GPIO header and press down evenly until it's fully seated. All the pins need to be inside the socket; a HAT shifted by one row won't work.
3. Fasten the HAT to the standoffs with the rest of the screws.

## How do I put the hub in its case?

1. Set the Pi, with its HAT, into the case.
2. Pass the SMA end of the antenna cable through the antenna hole in the case and tighten the nut.
3. Screw the LoRa antenna onto that SMA connector on the outside.
4. Close the case and keep the vents uncovered.

Stand the antenna upright, as high up as you can and away from metal. For range, where the antenna sits matters much more than the gateway itself: the top of a bookshelf beats the back of a metal cabinet every time.

## How do I connect the Zigbee and Thread radios?

1. Connect the Zigbee coordinator to a USB port **with a short USB extension cable**.
2. Using Thread? Plug the Thread radio into a different USB port, also on an extension cable, a little way from the Zigbee dongle.
3. Use the black USB 2 ports where you can. USB 3 ports and their cables disturb 2.4 GHz radios.

## How do I connect the cameras?

1. Connect every IP camera to the home network the Pi is on. A camera powered through its network cable plugs into a PoE switch or a PoE injector.
2. Write down each camera's username and password. You'll type them into the camera's recorder when you link it to its stream.

## How do I connect the Pi itself?

1. Insert the microSD card you prepare in the next step.
2. Plug in the network cable.
3. For the first setup, attach a screen, a keyboard and a mouse.
4. Plug in the power supply last. The Pi boots as soon as it has power.

Next: [How Do I Set Up a Raspberry Pi for Chirp Hub?](setup.md)
