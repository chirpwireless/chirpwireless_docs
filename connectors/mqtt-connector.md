# MQTT Connector

The MQTT connector is how you bring Zigbee sensors, DIY microcontroller sensors, and other smart home hardware directly into Chirp — without needing LoRaWAN.

The most popular use is Zigbee. Thousands of Zigbee-compatible devices are supported through [Zigbee2MQTT](https://www.zigbee2mqtt.io/supported-devices/) — temperature sensors, motion detectors, smart plugs, door and window sensors, leak detectors, and many more from brands including Aqara, IKEA, Sonoff, Philips Hue, and Tuya. Compatibility depends on Zigbee2MQTT's device support, your coordinator adapter, and the specific device model — check the [Zigbee2MQTT supported devices list](https://www.zigbee2mqtt.io/supported-devices/) to confirm your device before purchasing.

You can also connect non-Zigbee devices: an ESP32 you built yourself, a Tasmota-flashed smart plug, a soil moisture monitor with MQTT firmware, or any hardware that publishes data over MQTT.

> **What this section covers, and what it doesn't.** These pages cover MQTT telemetry — bringing data *from* your devices into Chirp — and how to map it to sensor metrics. MQTT command and control (sending commands *to* your devices through the Chirp API) is not covered here. If you want to control a Zigbee bulb during setup, use the Zigbee2MQTT web UI; commands you send there round-trip through your broker and update Chirp automatically.

## In this section

- [What MQTT is](mqtt/what-is-mqtt.md) — A short primer on brokers, topics, and JSON payloads.
- [Cloud MQTT](mqtt/cloud-mqtt.md) — Use Chirp's hosted broker. The simpler path for most homes.
- [External MQTT](mqtt/external-mqtt.md) — Use your own broker. Chirp connects out to it.
- [Topics and device routing](mqtt/topics-and-device-routing.md) — How Chirp matches incoming MQTT messages to the right device. Read this before registering devices.
- [Setting up Zigbee2MQTT](mqtt/zigbee2mqtt.md) — The generic Z2M install path that produces the telemetry you'll register here.
- [Troubleshooting](mqtt/troubleshooting.md) — When data isn't appearing, or the Logs tab stays empty.
- Tested hardware: [Sonoff ZBDongle-E coordinator](../gateways/zigbee2mqtt-hubs/sonoff-zbdongle-e-coordinator.md) and [Paulmann 50064 light bulb](../devices/tested-device-guides/zigbee/paulmann-50064-light-bulb.md). Other Zigbee2MQTT-supported coordinators and devices follow the same flow — these are tested examples.

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

> **Sensor name = device topic identifier, byte for byte.** Whatever you enter as the **Device ID** must match the device-level topic segment your hardware publishes — exactly. For Zigbee2MQTT, that's the friendly name. The Device ID input strips whitespace, so a Z2M friendly name like `Living Room Sensor` won't match a Device ID typed with spaces — use a whitespace-free name like `LivingRoomSensor` or `living_room_sensor` in **both** Z2M and Chirp. Capitalisation is preserved and significant.

3. The sensor opens with a **Mapping** tab. Inside Mapping there are two sub-tabs: **Topic** (where Chirp learns how to find the device in the topic stream) and **Mapping** (where you map payload keys to sensor metrics). Tapping **Mapping** opens the **Topic** sub-tab first — tap **Next** or the inner **Mapping** label to reach the per-key rows.

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
| **Data type** | Dropdown | Reported State, Telemetry, or Device Metadata |
| **Connector key** | Dropdown | Lists keys received from this device's payload. Empty until at least one publish has arrived |
| **Value** | Read-only | Current live value received from the broker |
| **Last update** | Read-only | Timestamp of the most recently received value |
| **Actions** | Icon | Trash icon removes the row |

**Add key** — adds a new empty mapping row.

#### Reported State vs Telemetry

The **Data type** dropdown distinguishes two kinds of values:

- **Reported State** — controllable device properties. The current state of something the device can also be told to change: a bulb's `state` (ON/OFF), `brightness`, `color_temp`, a smart plug's `power_state`. These are facts about what the device *is*.
- **Telemetry** — read-only measurements. Sensor readings that the device only reports: `temperature`, `humidity`, `linkquality`, `battery`, `pressure`. These are facts the device *observes*.

Pick the type that fits the value, not the metric template. Use Reported State when the field describes the device's controllable state; use Telemetry for everything else.

#### Connector Key dropdown is empty until your device publishes once

The **Connector key** column is a dropdown, not a text input. It lists the payload keys that have actually arrived from your device. Before the first publish, the dropdown shows nothing and the rows can't be filled.

The setup flow is two-pass:

1. Add a row per metric you want, pick the **Normalized key** from the templates dropdown (or use **+ Add new metric**), set the **Data type**, and leave the **Connector key** empty.
2. Tap **Save**. The device record is stored.
3. Make sure your hardware is publishing — for Zigbee2MQTT, the Z2M container is running and the device has reported at least once. (See [Discovering payload keys](mqtt/troubleshooting.md) if you're unsure how to force a publish.)
4. Reopen the device. The **Connector key** dropdown now lists the keys received from your device.
5. Match the right key to each row.
6. Tap **Save** again.

#### What the value column shows vs what the Logs tab shows

The Mapping tab's **Value** column updates from the most recent payload. It's a live snapshot — you'll see values as soon as the topic match works, even before you've finished filling in Connector keys.

The **Logs** tab is different: it's per-sensor history, and it only fills with publishes that arrive *after* you've saved Connector keys. If you fill in Connector keys, save, and then the lamp's wall switch is toggled but no MQTT publish is generated, the Logs tab will stay empty even though the Mapping tab shows the right value. To populate Logs, you need a fresh publish — drag a control in the Z2M web UI, send a `/get` poll, or wait for the device's next scheduled report. See [Troubleshooting](mqtt/troubleshooting.md) for the full list.

#### Z2M feature type → Chirp data type

When you're mapping a Zigbee2MQTT device, look up the device on [zigbee2mqtt.io/devices](https://www.zigbee2mqtt.io/supported-devices/). Each feature has a type — translate to Chirp's metric Type as follows:

| Z2M feature type | Chirp Type | Example |
|------------------|-----------|---------|
| `binary` | **String** | `state` — values are `"ON"`/`"OFF"` strings, not booleans |
| `numeric` | **Number** | `brightness`, `color_temp`, `linkquality` |
| `enum` | **String** | `color_mode`, `power_on_behavior` |
| `text` | **String** | Free-form text fields |

Selecting Boolean for a `state`-style binary field will leave the value empty — `"ON"` and `"OFF"` arrive as strings.

#### How to find what keys your device publishes

The Mapping tab doesn't auto-detect keys. Three ways to discover them:

1. **Z2M web UI** — open the Zigbee2MQTT frontend (default `http://localhost:8080`), click your device, look at the state panel. Every property name shown is a Connector Key candidate.
2. **The device's Z2M page** — `https://www.zigbee2mqtt.io/devices/{modelId}.html` lists the device's Exposes. Note that actual payloads can include keys that aren't on the Z2M page (`color_mode` is one example) — trust the live payload over the device page.
3. **Z2M logs** — after the first publish, `docker compose logs zigbee2mqtt | grep "MQTT publish"` shows the full JSON. Every top-level key is valid.

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

A short list — the [full troubleshooting page](mqtt/troubleshooting.md) covers Z2M startup logs, the empty-Logs-tab pattern, and how to force a publish for setup-time verification.

**No data appears after setup:**
- For Cloud MQTT: make sure you copied the password correctly at creation time. If unsure, rotate the credentials and update Zigbee2MQTT with the new password. Confirm the Topic prefix is being used correctly — all published topics must start with it.
- For External MQTT: double-check the broker URL and credentials. A small typo in the address is the most common cause of connection failures. For Zigbee2MQTT setups, confirm that Zigbee2MQTT is running and connected to the broker by checking the Zigbee2MQTT web interface.

**Sensor appears but readings are missing or wrong:**
- Open the sensor detail page and check the **Logs** tab for incoming message content.
- Verify the Device ID Topic matches the exact topic path the sensor is publishing to. Topics are case-sensitive.
- Verify the **Device ID** is byte-for-byte identical to the device-level segment (for Zigbee2MQTT, the friendly name) — no spaces, same case.
- If you added telemetry topic rows: check that the Connector Key spellings match the payload keys exactly.
- In the Mapping tab: confirm that the Connector Key column values match what the sensor is actually publishing.

**Mapping tab Value column populates but Logs tab is empty:**
This usually means Connector keys were saved after the most recent publish arrived. The Logs tab only fills with publishes that arrive *after* the keys are saved. Generate a fresh publish — drag a control in the Z2M web UI, or send a `/get` poll for setup-time verification — and the Logs tab will populate.

**"Toggle the device" doesn't produce data — what counts as a publish:**
Many Zigbee bulbs (including the Paulmann 50064) do not send an MQTT publish on a physical wall-switch toggle. Actions that *do* generate a publish during setup:
- Drag a control or click the toggle in the Z2M web UI for the device — Z2M sends a `/set` and re-publishes the new state.
- Send a `/get` poll (e.g. via `mosquitto_pub` to `{base_topic}/{friendlyName}/get`) — Z2M reads the device and publishes the current state. This is local Z2M-side verification, not a Chirp control path.
- Wait for the device's next scheduled report (battery sensors typically wake on a schedule).

**Zigbee device doesn't join:**
This is a Zigbee2MQTT or coordinator issue, not a Chirp issue. Check the [Zigbee2MQTT documentation](https://www.zigbee2mqtt.io/guide/usage/pairing_devices.html) for device pairing steps. Make sure permit join is enabled in Zigbee2MQTT when pairing new devices. For the Paulmann 50064 specifically, see the [tested device guide](../devices/tested-device-guides/zigbee/paulmann-50064-light-bulb.md).

**Cloud MQTT password lost:**
Go to the MQTT connector settings and rotate the credentials. Update Zigbee2MQTT or your device with the new password and topic prefix.

**Device fails to save on a Cloud MQTT connector:**
If saving a device on a Cloud MQTT connector fails, contact support for help completing the setup.

---

## What's next

- [Adding Sensors](../devices/adding-sensors.md) — Complete your sensor setup and assign it to a room.
- [Adding Widgets](../dashboards/adding-widgets/README.md) — Display your new sensor readings on a dashboard.
- [Set Up a Home Alert](../alarm/set-up-a-home-alert.md) — Get notified when readings go outside normal ranges.
