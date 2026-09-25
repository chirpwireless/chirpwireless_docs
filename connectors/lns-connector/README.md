---
description: The LNS connector links your LoRaWAN sensors to Chirp's built-in network server — nothing to install.
---

# LNS Connector

The LNS connector lets you use LoRaWAN sensors in Chirp without running a separate network server at home. Chirp's built-in **LoRaWAN Network Server** handles the messages arriving from your radio gateway and makes the readings available to dashboards, alerts, and automations.

LoRaWAN is the wireless protocol used by your sensors and gateway. Add the connector, connect a gateway that supports **Basics Station**, and register the sensors. You supply the radio equipment; Chirp supplies the network-server software.

## What You'll Find Here

- [What is LoRaWAN?](what-is-lorawan.md) — A quick guide to the wireless technology your sensors use
- [LoRaWAN Frequencies](lorawan-frequencies.md) — Which frequency band applies in your country
- [Built-in Network Server](built-in-lns.md) — How Chirp handles all the network complexity for you

## Setting Up the LNS Connector

For step-by-step instructions on adding the LNS connector to your home, see [Setting Up a Connection](../setting-up-a-connection.md).

## Inside the LNS Connector

Once your LNS connector is set up, click it in the connectors list to see two tabs:

- **LoRaWAN Gateways** — Your gateway list. See [Gateways](../../gateways/) for setup.
- **Connected Devices** — Your sensors. See [Adding Sensors](../../devices/adding-sensors.md) for the full walkthrough.

For the device-level setup, follow [LoRaWAN Devices](../../devices/lorawan-devices.md). It covers the physical identifier, connection fields, measurement mapping and checking retained history.
