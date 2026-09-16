---
description: See how connections link your home sensors to Chirp over LoRaWAN, MQTT or a vehicle tracker — or use pretend sensors before any hardware arrives.
---

# How Sensors Connect to Chirp

A Chirp connection is the software link that brings messages from your sensors into your home's workspace. In **Connectors**, you choose how those messages arrive, then register the devices and the readings you want to see.

The connection is separate from a gateway or hub, which is a physical device. LoRaWAN sensors send radio messages through a compatible gateway to Chirp's built-in network server. Zigbee sensors use a bridge such as [Zigbee2MQTT](mqtt/zigbee2mqtt.md), which converts their messages to MQTT before Chirp receives them. Hardware that already sends MQTT can use an [MQTT connection](mqtt-connector.md).

Choose the route that matches your equipment. You can also use the Emulator to try Chirp with simulated readings before buying hardware; see [Setting Up a Connection](setting-up-a-connection.md).

## Connection types

| Type | What it's for | Status |
|------|--------------|--------|
| **LNS** | LoRaWAN sensors — temperature, humidity, door/window, motion, soil moisture, and thousands more | Available |
| **Tracker** | Vehicle trackers — OBD2, CAN bus, and standalone GPS vehicle tracking devices (2,000+ preconfigured models) | Available |
| **MQTT** | Direct MQTT sensor connections — including Zigbee devices via Zigbee2MQTT, DIY sensors, and other MQTT-capable hardware. Two options: **External MQTT** (your own broker, up to 10 per home) and **Cloud MQTT** (Chirp-hosted broker, unlimited) | Available |
| **Emulator** | Pretend sensors that make up their own readings, so you can set up and try your whole home before the real ones arrive — then switch the device over to the real sensor when it does | Available |

Your home can have **one LNS connection**, **one Tracker connection** and **one Emulator connection**. MQTT connections can be External (up to 10 per home) or Cloud MQTT (unlimited — each gets its own hosted broker credentials).

## Where to find connections

Click **Connectors** in the sidebar to see your connections. If you haven't set any up yet, you'll see an empty page inviting you to create your first one.

Once you have connections, the page shows a table with:

| Column | What it shows |
|--------|--------------|
| **Name** | The connection name (assigned automatically) |
| **Last data received** | When a sensor last sent data through this connection |
| **Connected devices** | How many sensors are using this connection |
| **Creation date** | When you created the connection |

## What's next

Ready to set up your first connection? Head to [Setting Up a Connection](setting-up-a-connection.md) for a step-by-step walkthrough.

Nothing arrived yet? The [Emulator Connector](emulator-connector.md) gives you pretend sensors that invent their own readings, so you can build and test your whole home before the real ones turn up.

Want to learn more about LoRaWAN — the wireless technology behind your sensors? See the [LNS Connector](lns-connector/README.md) section for an introduction to the protocol, frequency bands by country, and how Chirp's built-in network server works.

Tracking a vehicle? See the [Tracker Connector](tracker-connector.md) for connecting a cellular GPS tracker — OBD2, CAN bus, or standalone GPS.

Want to connect Zigbee sensors, an ESP32 sensor, or any MQTT-capable device? See [MQTT Connector](mqtt-connector.md) for a complete setup guide.
