# Setting Up a Connection

Creating a connection takes just a few clicks. Here's how to set up an LNS connection (for LoRaWAN sensors) and a Tracker connection (for vehicle trackers).

## Adding an LNS connection

This is the most common connection for a smart home — it links Chirp's built-in LoRaWAN network to your sensor management.

1. Click **Connectors** in the sidebar.
2. Click **Add connector**.
3. In the dialog, select **LNS** from the **Connector type** dropdown.
4. Click **Add**.

That's it. The connection is created instantly. Chirp's built-in LoRaWAN network handles all the technical setup behind the scenes. To learn more about LoRaWAN, frequency bands, and the built-in network server, see the [LNS Connector](lns-connector/README.md) reference section.

### Inside the LNS connection

Click the LNS connection row in the table to open it. You'll see two tabs:

- **LoRaWAN Gateways** — Your gateway list. See [Setting Up Your Gateway](../gateways/setting-up-your-gateway.md).
- **Connected Devices** — Your sensor list. See [Adding Sensors](../devices/adding-sensors.md) and [Sensor Details](../devices/sensor-details.md).

## Adding a Tracker connection

If you want to track a vehicle, add a Tracker connection alongside your LNS connection. Chirp supports over 2,000 vehicle tracker models including OBD2 and CAN bus devices.

1. Click **Connectors** in the sidebar.
2. Click **Add connector**.
3. Select **Tracker** from the **Connector type** dropdown.
4. Click **Add**.

The Tracker connection is created instantly. Click its row to see the shared sensor list. For registration and management, see [Adding Sensors](../devices/adding-sensors.md) and [Sensor Details](../devices/sensor-details.md).

## One of each

Each home can have one LNS connection and one Tracker connection. Once both exist, the **Add connector** button becomes unavailable. If you need to start fresh, you can remove a connection by clicking the red trash icon on its row in the connection table (a confirmation dialog will appear before anything is deleted).

## Next step

With a connection in place, you're ready to start adding sensors. Head to [Adding Sensors](../devices/adding-sensors.md) to register your first one.
