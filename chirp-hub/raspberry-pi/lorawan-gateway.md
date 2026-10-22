---
description: Use a Raspberry Pi with a RAK5146 concentrator card as your home's LoRaWAN gateway, set up from Chirp Hub.
---

# How Do I Use a Raspberry Pi as a LoRaWAN Gateway?

Fit a LoRaWAN concentrator card on a Pi HAT and your Raspberry Pi becomes a complete LoRaWAN gateway. Chirp Hub reads the gateway ID from the card, points you to Chirp to register it, and installs the certificates Chirp hands you. The Pi then connects to Chirp's built-in LoRaWAN Network Server without you editing a single configuration file.

## Why build the gateway into the hub instead of buying one?

If your home already needs a box for cameras or Zigbee, the same Pi can cover your LoRaWAN sensors in the basement, the garage and the garden for the price of a concentrator card and an antenna. That's one device to plug in, place, connect and keep updated instead of two.

The gateway talks to Chirp over an encrypted **Basics Station** connection, the secure protocol Chirp expects from every LoRaWAN gateway. [LoRaWAN Gateways](../../gateways/lorawan-gateways/README.md) explains how Chirp works with gateways in general.

## What do I need before I start?

* A Raspberry Pi with the RAK5146 card and a LoRa antenna, bought from the [shopping list](shopping-list.md), [put together](hardware.md) and [set up with the script and Chirp Hub](setup.md).
* A Chirp account that can open **Gateways**.
* The LoRaWAN region your home is in, for example **EU868** in Europe or **US915** in North America.
* Internet access on the Pi.

## How do I set up the Raspberry Pi as a gateway?

1. On the Pi, open **Chirp Hub** and choose **LoRaWAN Gateway** in the left menu. You see the **Gateway ID**, read from the concentrator chip, and the radio Chirp Hub found. In Chirp, the same ID goes by the name Gateway EUI.
2. Click **Copy** beside the Gateway ID, then **Open Chirp**. Chirp opens in your browser at [app.chirpwireless.io](https://app.chirpwireless.io).
3. In Chirp, go to **Gateways**, click **Add gateway**, and choose **3rd Party Gateway**.
4. Type a name such as "Basement Gateway", pick the region your home is in, and paste the Gateway ID into **Gateway EUI**. Click **Next**.
5. Copy the **LNS Address** and download **certs.zip**. Inside the zip are three files: `tc.trust` (trust certificate), `tc.crt` (gateway certificate) and `tc.key` (private key).
6. Back in Chirp Hub, under **Add the files Chirp gave you**, use **Choose file** for **Trust certificate**, **Gateway certificate** and **Private key**, then paste the address into **LNS address**.
7. Click **Save** and approve the password prompt. Before touching anything, Chirp Hub checks that the three files belong together, then installs them and starts the gateway.
8. Once you see **This gateway is set up and running.**, click **Open Chirp** and watch the gateway come online under **Gateways**.

<figure><img src="../../.gitbook/assets/chirp-hub-lorawan-gateway-id.jpg" alt="Chirp Hub LoRaWAN Gateway page with the Gateway ID, the steps for registering it in Chirp and the certificate file fields"><figcaption><p>Copy the Gateway ID, follow the steps in Chirp, then add the files Chirp gives you.</p></figcaption></figure>

If the files don't match, for example certificates from two separate downloads or a private key protected by a password, Chirp Hub rejects them and tells you which one to pick again. If an install fails halfway through, it restores the earlier files, so the gateway never ends up with a mismatched set.

## How do I know the gateway is connected?

Chirp Hub tells you what it can check on the Pi: that the files are in place and that the gateway software is running. Whether the gateway has actually reached Chirp is shown in Chirp. To see that, open the gateway from **Gateways** in Chirp and check its status and traffic. [Checking LoRaWAN Gateway Health](../../gateways/lorawan-gateways/checking-lorawan-gateway-health.md) explains the details.

If the gateway software has stopped, the page reads **This gateway is set up but not running.** and offers a **Start gateway** button.

## Why does the page say there is no LoRaWAN radio?

This page only works on a Pi that has the concentrator card fitted and has been through the setup script. Anywhere else, such as a desktop computer or a Pi set up without the script, it names the hardware it's waiting for.

<figure><img src="../../.gitbook/assets/chirp-hub-lorawan-no-radio.jpg" alt="Chirp Hub LoRaWAN Gateway page explaining that it needs a concentrator such as a RAK5146 on a Raspberry Pi HAT"><figcaption><p>With no concentrator card, the page tells you which hardware to add.</p></figcaption></figure>

If the card is installed but not detected, see [Why Is My Raspberry Pi Hub Not Working?](troubleshooting.md#what-if-the-setup-script-says-the-concentrator-did-not-answer)

## How do I get the best range from my Pi gateway?

* Place the antenna as high as you can and never inside a metal cabinet. Its position affects range much more than the gateway hardware does.
* Keep `certs.zip` to yourself. Anyone holding it can pose as your gateway. If it leaks, create new certificates in Chirp and load the fresh files into Chirp Hub.
* Add your LoRaWAN sensors in Chirp the usual way, as described in [LoRaWAN Devices](../../devices/lorawan-devices.md). The Pi passes their readings on like any other gateway.
