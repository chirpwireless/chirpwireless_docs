---
description: Register a LoRaWAN, tracker, MQTT or pretend sensor in Chirp and map its readings, step by step.
---

# Adding Sensors

Adding a device creates its **digital twin**—the record Chirp uses to keep its name, settings, and readings together. Give it a name for what you want to follow, such as **Family Car** or **Living Room Temperature**, then connect the tracker or sensor that supplies its data.

You can save this record before the hardware is connected. The [Emulator](pretend-sensors.md) can supply generated readings while you prepare your dashboard and automations.

Replacing a broken tracker or sensor is a different task: open its existing digital device so you keep its recorded measurements. See [Sensor Details](sensor-details.md#replace-your-cars-tracker).

## Before you start

You'll need:
- **A connection** set up — an LNS connection for LoRaWAN sensors, a Tracker connection for vehicle trackers, an MQTT connector (Cloud or External) for Zigbee2MQTT and other MQTT-publishing hardware, or an Emulator connection if your sensor hasn't arrived yet. See [Setting Up a Connection](../connectors/setting-up-a-connection.md) and the [MQTT Connector](../connectors/mqtt-connector.md) docs.
- **Your sensor's identifiers** — for LoRaWAN sensors: the **Device EUI** and **AppKey**, usually printed on the sensor or its packaging. For trackers: the **Unique ID** from the manufacturer. For MQTT sensors: the **device-level topic identifier** that the device publishes under — for Zigbee2MQTT this is the friendly name. The Device ID field in Chirp must match it exactly, including case and spaces. A [pretend sensor](pretend-sensors.md) needs none of this — you choose its Device ID yourself, within the naming rules on that page.
- **For MQTT sensors only — the device must be publishing before you can finish mapping.** The Device data key dropdown in the Mapping tab is populated from payload keys actually received from the device. See the [MQTT-specific note](#a-note-for-mqtt-sensors) further down for the two-pass save flow.

## Where to add a sensor

There are several ways to start — they all open the same registration page:

- **Devices in the sidebar** — Click **Devices**, then click **Add device** in the top-right corner.
- **From a connection** — Open your LNS or Tracker connection, then click the **+** (Add device) button on the connection row, or open the connection and click **Add device** in the Connected Devices tab.

## Step 1 — Create the sensor profile

The page opens in Add mode, showing only the basic sensor info. No tabs or navigation are visible yet.

- **Device photos** — Snap a picture of the sensor so you can easily identify it later. Helpful when you have several similar-looking sensors.
- **Device name** — Give it a name that tells you what it is and where it is. "Kitchen Temperature" is much more useful than "Sensor 4."

Enter a name for your sensor and click **Save**. The profile is created and the page transitions to edit mode.

For a car, use **Family Car** as the name and enter the tracker's hardware identifier in **Connection**. That way you can recognize the same car in Chirp after fitting another tracker.

## Step 2 — Configure the connection and details

After the first save, the page shows with **Device info**, **Connection**, **Mapping** and **Logs** tabs, and a **Next** button for navigating between them. Two more appear when they apply: **Commands & States** on a device you can switch on and off, and **Emulator** on a pretend sensor.

### Connection

Click the **Connection** tab to link your sensor to the thing that feeds it.

**For LoRaWAN sensors (LNS connection):** Follow [LoRaWAN Devices](lorawan-devices.md) for identifiers, profile templates and manual fields, codecs, reporting interval and network joining.

#### Keep the identifiers somewhere safe

Use **Add to Vault** to store the sensor's EUI/key pair in [Key Vault](../reports/key-vault.md). See [identity and credentials](lorawan-devices.md#identity-and-credentials).

#### Code functions (codec)

The LoRaWAN codec turns binary uplinks into named readings. See [Templates and manual profiles](lorawan-devices.md#templates-and-manual-profiles) for selecting or supplying it.

#### Data sending interval

Enter the physical sensor's reporting schedule: a positive whole number and minute/hour/day/week/month. The initial value is 1 hour. This describes the expected cadence; it does not change hardware settings. For a [pretend sensor](pretend-sensors.md), it controls generation instead.


**For vehicle trackers (Tracker connection):**

1. Select your **Tracker** connection from the **Connector type** dropdown.
2. Enter the **Unique ID** for your tracker.
3. Select a **Device model** by searching the tracker library.
4. A **Url for GPS tracker** panel appears — copy this URL and configure your tracker to send data to it.

**For MQTT sensors (Cloud or External MQTT):** Follow [MQTT Devices](mqtt-devices.md) to save the connection and topic routing, receive a message, then map its readings. Device ID must match the publisher's identifier, including case and spaces.


**For pretend sensors (Emulator connection):**

1. Select your **Emulator** connection from the **Connector type** dropdown.
2. Choose a **Device ID** — up to 64 characters (letters, numbers, spaces, dots, underscores, dashes), unique across all of Chirp. See [Pretend Sensors](pretend-sensors.md).
3. Say **how often it reports**, and either tick **Use device preset** to borrow a real model's readings or add them yourself.

Chirp then invents the readings for you, and an extra **Emulator** tab appears so you can push a value whenever you want to test something. This is how you get your dashboards and alerts working before the hardware arrives — and you can switch the same sensor over to the real one when it does. See [Pretend Sensors](pretend-sensors.md).

### Mapping {#metrics}

See [mapping controls](sensor-details.md#metrics) for every column, inline metric creation, and immediate template-change/removal behavior.

Click the **Mapping** tab to map your sensor's raw data to measurement definitions. A profile supplies the network configuration and codec. Assign measurement templates and connector keys here after the source has reported, or return later to finish mapping.

#### See what your sensor is sending

Once your sensor is connected and transmitting, the Mapping tab shows a live view of the raw data — a table listing every field your sensor sends, its current value, and when it last updated. You see exactly what's coming in, with the actual field names the sensor uses (like `t`, `hum`, `battery_mv`, or whatever the manufacturer chose).

Come back to this table any time you need to know what a device reports and how it words it — writing an automation condition, or setting up a check on a command. See [What Your Device Is Sending](what-your-device-is-sending.md).

#### Map raw fields to your data templates

This is where cryptic sensor output becomes something you can actually read. When you map a raw field like `t` to a data template called "Temperature" with the unit °C, Chirp starts displaying that reading as "Temperature (°C)" everywhere — in dashboards, automations, alerts, and history charts. You're giving each raw field a proper name, unit, and format.

To set up a mapping:

1. **Add a metric** — Click **Add key** and pick a data template from the dropdown (e.g., "Temperature", °C, Float). The Unit, Type, and Data type columns fill in automatically from the template. If you need a template that doesn't exist yet, create one in [Data Templates](data-templates.md).
2. **Choose the matching field** — In the **Device data key** dropdown, pick the raw field name that carries this measurement (e.g., pick `t` if your sensor sends temperature as `t`).
3. **Save** — The next matching transmission supplies the measurement to dashboards, automations, alerts, and history.

If the Device data key is not filled in, the data for that metric will be ignored.

Add as many metrics as your sensor reports — you can map them all in one go.

#### Works with any sensor — even prototypes

A device does not need a library preset to supply measurements. It does need a compatible connector and decoding path: a LoRaWAN codec, a supported MQTT message shape, or the appropriate adapter. Once named fields arrive, map the readings you need. See [LoRaWAN Devices](lorawan-devices.md) and [MQTT Devices](mqtt-devices.md).

#### A note for MQTT sensors

The **Device data key** dropdown fills after messages arrive. Save the connection first, let the sensor publish, then select the received keys for your measurements and save. Wait for another message to see stored history. See [MQTT Devices](mqtt-devices.md#map-messages-to-retained-measurements).

### Logs

The Logs tab is empty until your sensor starts sending data. After you save mappings and a fresh message arrives, stored measurement values appear here grouped by minute.

Click **Save** again to persist the connection and metrics configuration.

A disabled **Save** can mean a missing name, no permission to edit devices, or a subscription restriction. Adding another device also needs an available device slot.

## After saving

Your sensor's profile appears in the sensor lists throughout Chirp.

For LoRaWAN sensors, data starts flowing once the sensor powers on and connects to your gateway. For trackers, data flows once the physical device starts reporting to the URL you configured.

Worth knowing about that LoRaWAN connection: registering the sensor here sets Chirp up to recognize it, but the sensor still has to *join* the network itself before it sends anything. A sensor straight out of the box does that on its own the moment you power it up. A sensor with a past life — second-hand, inherited with the house, or previously set up on something else — is still joined to that old network and needs a reset before it will join yours. See [First things first: joining the network](connection-diagnostics.md#first-things-first-joining-the-network).

**Saved everything and still seeing no readings?** Don't start pulling batteries out. Open the sensor's **Connection** tab — Chirp will tell you exactly where the data has stopped and what to do about it. See [Connection Diagnostics](connection-diagnostics.md).

The device page adapts to a phone screen, so you can enter its details while installing it.

## What's next

- **Customize data templates** if Chirp doesn't automatically recognize what your sensor measures. See [Data Templates](data-templates.md).
- **View and edit your sensor** anytime. See [Sensor Details](sensor-details.md).
- **Nothing showing up?** See [Connection Diagnostics](connection-diagnostics.md).

## Check a key without leaving it exposed

While entering an **AppKey**, you can see what you type. Click outside the field or press Enter to hide it again. The eye button lets you reveal it when needed; a key filled from a QR code stays hidden. Close the visible-key state before sharing a screenshot.
