---
description: Create an LNS connection for LoRaWAN sensors, a Tracker connection for your vehicle, or an Emulator connection to start with no hardware.
---

# Setting Up a Connection

Creating a connection takes just a few clicks. Here's how to set up an LNS connection (for LoRaWAN sensors), a Tracker connection (for vehicle trackers), and an Emulator connection (for trying Chirp before your sensors arrive).

## Adding an LNS connection

This is the most common connection for a smart home — it links Chirp's built-in LoRaWAN network to your sensor management.

1. Click **Connectors** in the sidebar.
2. Click **Add connector**.
3. In the dialog, select **LNS** from the **Connector type** dropdown.
4. Click **Add**.

That's it. The connection is created instantly. Chirp's built-in LoRaWAN network handles all the technical setup behind the scenes. To learn more about LoRaWAN, frequency bands, and the built-in network server, see the [LNS Connector](lns-connector/README.md) reference section.

### Inside the LNS connection

Click the LNS connection row in the table to open it. You'll see two tabs:

- **LoRaWAN Gateways** — Your gateway list. See [Setting Up Your Gateway](../gateways/lorawan-gateways/setting-up-a-lorawan-gateway.md).
- **Connected Devices** — Your sensor list. See [Adding Sensors](../devices/adding-sensors.md) and [Sensor Details](../devices/sensor-details.md).

## Adding a Tracker connection

If you want to track a vehicle, add a Tracker connection alongside your LNS connection. Chirp supports over 2,000 vehicle tracker models including OBD2 and CAN bus devices.

1. Click **Connectors** in the sidebar.
2. Click **Add connector**.
3. Select **Tracker** from the **Connector type** dropdown.
4. Click **Add**.

The Tracker connection is created instantly. Click its row to see the shared sensor list. For registration and management, see [Adding Sensors](../devices/adding-sensors.md) and [Sensor Details](../devices/sensor-details.md). For what this connector is (and isn't) for — cellular/GSM vehicle trackers, not LoRaWAN ones — see the [Tracker Connector](tracker-connector.md) page.

## Adding an Emulator connection

No sensors yet? Add an **Emulator** connection and Chirp will make up the readings for you, so you can build your dashboards and alerts before anything arrives in the post.

1. Click **Connectors** in the sidebar.
2. Click **Add connector**.
3. Select **Emulator** from the **Connector type** dropdown.
4. Click **Add**.

There is nothing to fill in — no account to link, no keys to copy. See [Emulator Connector](emulator-connector.md) for what it's for, and [Pretend Sensors](../devices/pretend-sensors.md) for making one.

## How many of each

Each home can have **one LNS connection**, **one Tracker connection** and **one Emulator connection**. MQTT is the exception: up to 10 External MQTT connections, and as many Cloud MQTT connections as you like.

Once you already have every kind you can add, the **Add connector** button stops offering new ones. If you need to start fresh, remove a connection by clicking the red trash icon on its row in the connection table (a confirmation dialog appears before anything is deleted).

## Next step

With a connection in place, you're ready to start adding sensors. Head to [Adding Sensors](../devices/adding-sensors.md) to register your first one.
