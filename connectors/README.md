# How Sensors Connect to Chirp

A connection tells Chirp which protocol to listen on for a specific sensor type. It does not create sensor profiles — you register sensors separately through the sensor dialog. A connection establishes the protocol binding that makes data flow possible.

Most homes need just one connection: an **LNS connection** for LoRaWAN sensors. If you also want to track a vehicle, you can add a **Tracker connection** for vehicle trackers (OBD2, CAN bus, and standalone GPS vehicle tracking devices).

## Connection types

| Type | What it's for | Status |
|------|--------------|--------|
| **LNS** | LoRaWAN sensors — temperature, humidity, door/window, motion, soil moisture, and thousands more | Available |
| **Tracker** | Vehicle trackers — OBD2, CAN bus, and standalone GPS vehicle tracking devices (2,000+ preconfigured models) | Available |
| **MQTT** | Direct MQTT sensor connections | Preview — not yet available for setup |

Your home can have **one LNS connection** and **one Tracker connection**. Once both are set up, you're covered for the most common sensor types.

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
