# How Sensors Connect to Chirp

A connection tells Chirp which protocol to listen on for a specific sensor type. It does not create sensor profiles — you register sensors separately through the sensor dialog. A connection establishes the protocol binding that makes data flow possible.

Most homes need just one connection: an **LNS connection** for LoRaWAN sensors. If you also want to track a vehicle, you can add a **Tracker connection** for vehicle trackers (OBD2, CAN bus, and standalone GPS vehicle tracking devices).

## Connection types

| Type | What it's for | Status |
|------|--------------|--------|
| **LNS** | LoRaWAN sensors — temperature, humidity, door/window, motion, soil moisture, and thousands more | Available |
| **Tracker** | Vehicle trackers — OBD2, CAN bus, and standalone GPS vehicle tracking devices (2,000+ preconfigured models) | Available |
| **MQTT** | Direct MQTT sensor connections — including Zigbee devices via Zigbee2MQTT, DIY sensors, and other MQTT-capable hardware. Two options: **External MQTT** (your own broker, up to 10 per home) and **Cloud MQTT** (Chirp-hosted broker, unlimited) | Available |

Your home can have **one LNS connection** and **one Tracker connection**. MQTT connections can be External (up to 10 per home) or Cloud MQTT (unlimited — each gets its own hosted broker credentials).

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

Want to learn more about LoRaWAN — the wireless technology behind your sensors? See the [LNS Connector](lns-connector/README.md) section for an introduction to the protocol, frequency bands by country, and how Chirp's built-in network server works.

Tracking a vehicle? See the [Tracker Connector](tracker-connector.md) for connecting a cellular GPS tracker — OBD2, CAN bus, or standalone GPS.

Want to connect Zigbee sensors, an ESP32 sensor, or any MQTT-capable device? See [MQTT Connector](mqtt-connector.md) for a complete setup guide.
