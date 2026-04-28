# MQTT Connector

The MQTT connector is how you bring Zigbee sensors, DIY microcontroller sensors, and other smart home hardware directly into Chirp — without needing LoRaWAN.

The most popular use is Zigbee. Thousands of Zigbee-compatible devices are supported through [Zigbee2MQTT](https://www.zigbee2mqtt.io/supported-devices/) — temperature sensors, motion detectors, smart plugs, door and window sensors, leak detectors, and many more from brands including Aqara, IKEA, Sonoff, Philips Hue, and Tuya. Compatibility depends on Zigbee2MQTT's device support, your coordinator adapter, and the specific device model — check the [Zigbee2MQTT supported devices list](https://www.zigbee2mqtt.io/supported-devices/) to confirm your device before purchasing.

You can also connect non-Zigbee devices: an ESP32 you built yourself, a Tasmota-flashed smart plug, a soil moisture monitor with MQTT firmware, or any hardware that publishes data over MQTT.

---

## How Zigbee-over-MQTT works

Zigbee devices don't connect to Chirp directly. They connect through a coordinator — a small USB or network-attached adapter — and software called Zigbee2MQTT that translates Zigbee signals into MQTT messages. The MQTT connector then picks up those messages and routes the data into Chirp.

```
Zigbee sensor  →  Zigbee coordinator  →  Zigbee2MQTT  →  MQTT  →  Chirp
```

You need:

1. A **Zigbee coordinator adapter** — the hardware bridge between Zigbee radio and your home network.
2. **Zigbee2MQTT software** — runs on a Raspberry Pi, home server, or any always-on machine.
3. A **Chirp MQTT connector** — tells Chirp where to listen and how to read the messages.

### Recommended Zigbee coordinator adapters

Any adapter supported by Zigbee2MQTT will work. The most commonly used:

- **SONOFF Zigbee 3.0 USB Dongle Plus** — ZBDongle-P (CC2652P chip) or ZBDongle-E (EFR32MG21 chip). Plug directly into a USB port.
- **SMLIGHT SLZB-06 / SLZB-06M** — Network-attached. Connects over Ethernet or Wi-Fi.
- **Home Assistant Connect ZBT-1 / SkyConnect** — Works when configured to use Zigbee2MQTT (instead of ZHA).
- **ConBee II / Phoscon** — USB adapter from Dresden Elektronik, used with deCONZ or Zigbee2MQTT.

For the current recommended options, see the [Zigbee2MQTT adapter guide](https://www.zigbee2mqtt.io/guide/adapters/).

---

## Two ways to connect: Cloud MQTT vs External MQTT

When you add an MQTT connector, you choose one of two options:

**Chirp Cloud MQTT** — Chirp provides the MQTT broker. You get a ready-to-use endpoint, username, password, and topic prefix. Paste them into Zigbee2MQTT or your device settings and you're done. Nothing to install or maintain. This is the simpler choice for most home setups — especially if you don't already run a local broker.

**External MQTT** — You use an MQTT broker you already operate. Chirp connects to it using the broker URL and credentials you supply. Use External MQTT if your broker is reachable from the internet — for example, a broker you host on a VPS or in a cloud account. For local home setups where Zigbee2MQTT runs on a Raspberry Pi or home server, Cloud MQTT is usually the simpler choice: configure Zigbee2MQTT to publish outward to the Chirp-hosted endpoint rather than the other way around.

You can create multiple connectors of either type — External MQTT up to 10 per home, Cloud MQTT as many as you need.

---

## Step 1: Add a Chirp Cloud MQTT connector

1. Tap **Connectors** in the sidebar.
2. Tap **Add connector**.
3. Select **Cloud MQTT** from the connector type list.
4. Enter a **Name** for the connector.
5. Tap **Add**.

Chirp provisions a broker endpoint and displays the credentials:

| Credential | Details |
|-----------|---------|
| **Broker URL** | The hosted MQTT endpoint. Copy it using the copy button. |
| **Topic prefix** | All messages to this connector must be published under this prefix — it keeps your data organized. Copy it. |
| **Username** | Assigned automatically. Copy it. |
| **Password** | Shown once. **Copy it immediately** and save it somewhere safe. If you lose it, you'll need to rotate the credentials. |

#### Connecting Zigbee2MQTT or your device

Copy the credentials above into your Zigbee2MQTT configuration or device MQTT settings. A few things to know before you connect:

- **The Broker URL is the complete endpoint** — copy it exactly as shown. It uses TLS on port 1884 (not the standard 1883). In Zigbee2MQTT, set `server` to this value and enable TLS.
- **Every topic must start with the Topic prefix.** The full topic you publish to is: `{Topic prefix}/{device topic}`. For Zigbee2MQTT, set `base_topic` in its configuration to `{Topic prefix}/zigbee2mqtt` — for example `iot/abc123/xyz789/zigbee2mqtt`. Zigbee2MQTT then publishes each device under that path automatically.
- **Device routing templates don't include the prefix.** When you configure the Device ID Topic in the Topic tab (Step 2), enter only the device-level portion — for example `zigbee2mqtt/{{deviceId}}`. Chirp strips the prefix automatically before matching.

---

## Step 1 (alternative): Add an External MQTT connector

1. Tap **Connectors** in the sidebar.
2. Tap **Add connector**.
3. Select **External MQTT** from the connector type list.
4. Fill in the form:

   | Field | What to enter |
   |-------|--------------|
   | **Name** | A label for this connector (required) |
   | **Broker URL** | The full address including scheme and port. The broker must be reachable from the internet — a private home network address will not work. Examples: `mqtts://mqtt.yourdomain.com:8883` (TLS), `mqtt://mqtt.yourdomain.com:1883` (plain). Accepted schemes: `mqtt://`, `mqtts://`, `tcp://`, `ssl://` |

5. Choose an **authentication method**:
   - **Anonymous** — no credentials
   - **Basic** — Username and Password (password has a show/hide toggle)
   - **Certification** — three file upload buttons: **CA Certificate**, **Client Certificate**, **Private Key** (upload files — do not paste text)
   - **JWT Token** — Token field (show/hide + copy); a Certificate upload field also appears in the form as an optional attachment

6. Tap **Save**.

---

## Step 2: Register a sensor

Each sensor that sends data through this connector needs to be registered in Chirp. Registration maps MQTT topics and payload structure to a sensor profile.

1. On the connector detail page, tap **Add device** — or go to **Devices** and start registration from there, selecting this connector.
2. Fill in the sensor name and pick a template if one fits.
3. The sensor opens with two MQTT-specific tabs: **Topic** and **Mapping**.

---

### Topic tab — how Chirp finds the device

#### The common case: Zigbee2MQTT with a flat JSON payload

Zigbee2MQTT publishes each device's data to a topic named after the device:
```
zigbee2mqtt/0x00158d0001234567
```
or with a friendly name:
```
zigbee2mqtt/Living Room Sensor
```

For **Device ID Topic**, enter:
```
zigbee2mqtt/{{deviceId}}
```

Leave **Telemetry topics** empty. Zigbee2MQTT sends a flat JSON payload like:
```json
{"temperature": 21.4, "humidity": 58, "battery": 92, "linkquality": 115}
```

Chirp reads all keys from this payload automatically — no Telemetry topics configuration needed. However, the Mapping tab is still required: each key you want as a sensor metric needs a row in the Mapping tab with the Connector Key set to match the payload key name. Without a Mapping row for a key, that data is silently ignored.

This is the default path for most Zigbee sensors, ESP32 projects publishing flat JSON, and Tasmota devices.

#### Topic tab fields explained

**Device ID Topic** — The MQTT topic pattern for this device. Use `{{deviceId}}` to mark the part of the topic that contains the device identifier. Required.

**Where to get the device ID** — Dropdown:
- **Topic** (default) — extracted from the `{{deviceId}}` segment.
- **Payload** — taken from a field inside the JSON message body.

**Device ID Payload Path** — Required when source is **Payload**. A dot-notation path to the ID field. Example: `device.id` for a payload like `{"device": {"id": "sensor-01"}, "temp": 22.1}`.

**Telemetry topics** — Optional. Add rows here when you need per-topic control: for example, when a sensor publishes each measurement to a separate topic, or when the measurement value is in the topic segment rather than the payload body. Each row has:

- **MQTT Topic for telemetry** — topic pattern with `{{deviceId}}` placeholder
- **Connector Key** — names the source key arriving from MQTT. The Connector Key does not create a platform metric on its own — it must be linked to a normalized metric in the Mapping tab.

**Add new topic** — adds a telemetry topic row.

**Apply all** — uses the device ID topic pattern as a prefix to generate telemetry topic templates for rows that already have a Connector Key filled in. Useful when you have multiple per-topic rows that follow a predictable naming pattern.

#### Placeholder reference

| Placeholder | What it does |
|-------------|-------------|
| `{{deviceId}}` | Marks the topic segment that contains the device identifier |
| `{{value}}` | Marks a topic segment whose content is the measurement value itself — for example, `sensors/dev01/22.5` where `22.5` is the reading. Do not use `{{value}}` for topic segments that name the metric (like `temperature`) — if the segment is a label rather than a value, use the payload-style approach instead |

---

### Mapping tab — what the data means

The Mapping tab links incoming MQTT keys to normalized Chirp sensor metrics. This is where raw data becomes something Chirp can display in dashboards, trigger in alarms, and query in the AI assistant.

The Connector Key in the Mapping tab must match the key published in the MQTT payload (or the Connector Key defined in the Topic tab). If they don't match, data is ignored — the helper text above the table says: **"If the Connector key is not filled in, the data will be ignored."**

The table has 8 columns:

| Column | Type | Details |
|--------|------|---------|
| **Normalized key** | Dropdown | Select from sensor templates; includes a "+ Add new metric" option |
| **Unit** | Read-only | Derived from the selected template |
| **Type** | Read-only | Integer, Float, String, or Boolean — derived from template |
| **Data type** | Dropdown | Telemetry, Reported State, or Device Metadata |
| **Connector key** | Editable | Must match the key in the MQTT payload or the Connector Key from the Topic tab |
| **Value** | Read-only | Current live value received from the broker |
| **Last update** | Read-only | Timestamp of the most recently received value |
| **Actions** | Icon | Trash icon removes the row |

**Add key** — adds a new empty mapping row.

4. Tap **Save** to finish registration.

---

## What to expect after setup

Once a sensor is registered and data is flowing:

- The connector's **Last data received** timestamp updates each time a message arrives.
- The sensor's detail page shows incoming readings — temperature, humidity, battery, or whatever your sensor reports.
- Readings appear on your dashboards and are available for automations and alerts.

For Zigbee2MQTT sensors, data typically appears within a few seconds of the sensor's next report.

---

## More MQTT examples

**ESP32 DIY temperature sensor:**
Publishes to `home/sensors/esp-kitchen/data` with a flat JSON payload. Device ID Topic: `home/sensors/{{deviceId}}/data`. Leave telemetry topics empty — the payload is parsed automatically. Mapping tab maps `temperature` and `humidity` keys to the corresponding normalized metrics.

**Tasmota smart plug:**
Tasmota publishes to `tele/plug-01/SENSOR`. Device ID Topic: `tele/{{deviceId}}/SENSOR`. The payload is flat JSON with energy readings (Power, Voltage, Current, Today). Leave telemetry topics empty; then add Mapping tab rows for the Tasmota keys you want to track.

**Garden soil sensor — single metric on a dedicated topic:**
A custom sensor publishes soil moisture to `garden/{{deviceId}}/moisture` with a plain number payload. Add a telemetry topic row: topic `garden/{{deviceId}}/moisture`, Connector Key `soil_moisture`. Then in the Mapping tab, link `soil_moisture` to the normalized soil moisture metric.

---

## Troubleshooting

**No data appears after setup:**
- For Cloud MQTT: make sure you copied the password correctly at creation time. If unsure, rotate the credentials and update Zigbee2MQTT with the new password. Confirm the Topic prefix is being used correctly — all published topics must start with it.
- For External MQTT: double-check the broker URL and credentials. A small typo in the address is the most common cause of connection failures. For Zigbee2MQTT setups, confirm that Zigbee2MQTT is running and connected to the broker by checking the Zigbee2MQTT web interface.

**Sensor appears but readings are missing or wrong:**
- Open the sensor detail page and check the **Logs** tab for incoming message content.
- Verify the Device ID Topic matches the exact topic path the sensor is publishing to. Topics are case-sensitive.
- If you added telemetry topic rows: check that the Connector Key spellings match the payload keys exactly.
- In the Mapping tab: confirm that the Connector Key column values match what the sensor is actually publishing.

**Zigbee device doesn't join:**
This is a Zigbee2MQTT or coordinator issue, not a Chirp issue. Check the [Zigbee2MQTT documentation](https://www.zigbee2mqtt.io/guide/usage/pairing_devices.html) for device pairing steps. Make sure permit join is enabled in Zigbee2MQTT when pairing new devices.

**Cloud MQTT password lost:**
Go to the MQTT connector settings and rotate the credentials. Update Zigbee2MQTT or your device with the new password and topic prefix.

**Device fails to save on a Cloud MQTT connector:**
If saving a device on a Cloud MQTT connector fails, contact support for help completing the setup.

---

## What's next

- [Adding Sensors](../devices/adding-sensors.md) — Complete your sensor setup and assign it to a room.
- [Adding Widgets](../dashboards/adding-widgets/README.md) — Display your new sensor readings on a dashboard.
- [Set Up a Home Alert](../alarm/set-up-a-home-alert.md) — Get notified when readings go outside normal ranges.
