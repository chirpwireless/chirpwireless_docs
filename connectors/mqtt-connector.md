---
description: Bring Zigbee sensors, smart plugs, and DIY hardware into your home with the MQTT connector.
---

# How do I connect Zigbee devices to Chirp over MQTT?
Chirp's MQTT connector lets MQTT devices and bridged Zigbee sensors join the same dashboards and automations as the rest of your home. It is a way to bring a smart plug, temperature sensor, or DIY device into a shared setup instead of leaving its readings in a separate application.

**MQTT** is a messaging protocol: devices send messages to a server called a **broker**, and Chirp receives the messages it subscribes to.

Zigbee sensors do not speak MQTT themselves. A bridge such as [Zigbee2MQTT](mqtt/zigbee2mqtt.md), running with a compatible Zigbee coordinator, translates their radio messages into MQTT. Devices with MQTT firmware can send messages to the broker directly.

The most popular use is Zigbee. Thousands of Zigbee-compatible devices are supported through [Zigbee2MQTT](https://www.zigbee2mqtt.io/supported-devices/) — temperature sensors, motion detectors, smart plugs, door and window sensors, leak detectors, and many more from brands including Aqara, IKEA, Sonoff, Philips Hue, and Tuya. Compatibility depends on Zigbee2MQTT's device support, your coordinator adapter, and the specific device model — check the [Zigbee2MQTT supported devices list](https://www.zigbee2mqtt.io/supported-devices/) to confirm your device before purchasing.

You can also connect non-Zigbee devices: an ESP32 you built yourself, a Tasmota-flashed smart plug, a soil moisture monitor with MQTT firmware, or any hardware that publishes data over MQTT.

> **What this section covers.** These pages cover MQTT telemetry — bringing data *from* your devices into Chirp — and how to map it to sensor metrics. Once a device is connected, you can also send commands *to* it from Chirp: turn a plug on or off, dim a bulb, change its color temperature, and more. That two-way control is set up on each device under [Device Commands](../devices/commands/).

## In this section

- [What MQTT is](mqtt/what-is-mqtt.md) — A short primer on brokers, topics, and JSON payloads.
- [Cloud MQTT](mqtt/cloud-mqtt.md) — Use Chirp's hosted broker. The simpler path for most homes.
- [Topics and device routing](mqtt/topics-and-device-routing.md) — How Chirp matches incoming MQTT messages to the right device. Read this before registering devices.
- [Setting up Zigbee2MQTT](mqtt/zigbee2mqtt.md) — The generic Z2M install path that produces the telemetry you'll register here.
- [Troubleshooting](mqtt/troubleshooting.md) — When data isn't appearing, or the Logs tab stays empty.
- Tested hardware: [Sonoff ZBDongle-E coordinator](../gateways/zigbee2mqtt-hubs/sonoff-zbdongle-e-coordinator.md) and [Paulmann 50064 light bulb](../devices/tested-device-guides/zigbee/paulmann-50064-light-bulb.md). Other Zigbee2MQTT-supported coordinators and devices follow the same flow — these are tested examples.

---

## How does Zigbee over MQTT work?
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

## How do I connect MQTT devices to Chirp?

Chirp supplies the broker. When you add an MQTT connector, Chirp hosts a broker for you and gives you an endpoint, a username, a password and a topic prefix. Paste those into Zigbee2MQTT or your device settings and the connection is ready. There is nothing to install or keep running, and you can add as many Cloud MQTT connectors as you need.

---

## How do I add a Chirp Cloud MQTT connector?
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

- **Copy the Broker URL exactly as shown** — it is the whole endpoint, nothing needs to be added to it. It uses TLS on port 1884 (not the standard 1883). In Zigbee2MQTT, set `server` to this value and enable TLS.
- **Every topic must start with the Topic prefix.** The full topic you publish to is: `{Topic prefix}/{device topic}`. For Zigbee2MQTT, set `base_topic` in its configuration to `{Topic prefix}/zigbee2mqtt` — for example `iot/abc123/xyz789/zigbee2mqtt`. Zigbee2MQTT then publishes each device under that path automatically.
- **Device routing templates don't include the prefix.** When you build the **MQTT Topic for device ID** on the **Connection** tab (Step 2), enter only the device-level portion — for example `zigbee2mqtt/{{deviceId}}`. Chirp strips the prefix automatically before matching.

---

## How do I register a Zigbee sensor in Chirp?
Every sensor that sends data through this connector gets its own device in Chirp. Registering it tells Chirp which topic carries the device's messages and which payload fields are readings.

1. Open **Devices** and select **Add device**, or open **Connectors** and use **Add device** on this connector's row.
2. Type a **Device name** and, if you use applications, pick one under **Application**. Select **Save**.
3. The device opens on its **Connection** tab. Under **Connector type**, choose this MQTT connector. The topic settings appear below it.
4. Build the topic on the **Connection** tab, as described next, and select **Save**.
5. Open the **Mapping** tab to link the payload fields to readings.

> **The Device ID must match the topic segment your hardware publishes, character for character.** For Zigbee2MQTT that segment is the friendly name. A Device ID can be 1 to 64 characters of ASCII letters, digits, spaces, periods, underscores and hyphens, and Chirp keeps capitals and spaces exactly as typed. Because Zigbee2MQTT topics are easiest without spaces, a name like `LivingRoomSensor` is the safer choice in both Zigbee2MQTT and Chirp.

---

### How does Chirp find the device in the MQTT topic stream?

#### The common case: Zigbee2MQTT with a flat JSON payload

Zigbee2MQTT publishes each device's data to a topic named after the device:
```
zigbee2mqtt/0x00158d0001234567
```
or with a friendly name:
```
zigbee2mqtt/LivingRoomSensor
```

In **MQTT Topic for device ID**, add the text segment `zigbee2mqtt`, then a **Device ID** segment, so the resolved preview reads:
```
zigbee2mqtt/{{deviceId}}
```

Leave **Topic Telemetry** empty. Zigbee2MQTT sends a flat JSON payload like:
```json
{"temperature": 21.4, "humidity": 58, "battery": 92, "linkquality": 115}
```

Chirp reads every key in that payload by itself, so no telemetry topic rows are needed. The **Mapping** tab is still required: each key you want as a reading needs a row there with its **Device data key** set to the payload key name. A key without a row is ignored.

This is the default path for most Zigbee sensors, ESP32 projects that publish flat JSON, and Tasmota devices.

#### What the topic settings on the Connection tab do

- **Topic for defining Device ID, MQTT Topic for device ID** is the topic pattern for this device, built from text segments and one **Device ID** segment. A Cloud MQTT prefix appears first and is locked.
- **Where to get the device ID** chooses **Topic** (the default, taken from the Device ID segment) or **Payload** (taken from a field inside the JSON message). With **Payload**, **Payload template** holds a dot path such as `device.id`, and **Payload preview** shows the JSON around it.
- **Topic Telemetry** is optional. Add rows with **Add new topic** when each measurement arrives on its own topic or when the value sits inside the topic itself. A row has **MQTT Topic for telemetry** and a **Device data key**, which must be filled in. The key does not create a reading on its own; link it to a metric on the **Mapping** tab.
- **Apply all** builds the telemetry topics from the device ID topic, and only for rows whose **Device data key** is already filled in. It saves time when several rows follow one naming pattern.

For the segment builder, the placeholders and the payload mode in full, see [Topics and device routing](mqtt/topics-and-device-routing.md).

#### Placeholder reference

| Placeholder | What it does |
|-------------|-------------|
| `{{deviceId}}` | Marks the topic segment that contains the device identifier |
| `{{value}}` | Marks a topic segment whose content is the measurement value itself, such as `22.5` in `sensors/dev01/22.5`. Leave it out when the segment names the metric (for example `temperature`). A telemetry topic without `{{value}}` tells Chirp to find the number inside the message and store it under the row's Device data key. |

---

### How do I map MQTT payload fields to readings?

The **Mapping** tab links incoming MQTT keys to Chirp metrics. This is where incoming fields become readings you can put on dashboards and use in automations. The AI Assistant can help map them and build the response around them.

A row only receives data when its **Device data key** matches a key the device actually sends. The helper text above the table says: **"If the Device data key is not filled in, the data will be ignored."**

The table has these columns, from left to right:

| Column | Type | Details |
|--------|------|---------|
| **Device data key** | Dropdown | Lists the keys this device has actually sent. Empty until at least one message has arrived. |
| **Value** | Read-only | Current live value received from the broker |
| **Last update** | Read-only | Timestamp of the most recently received value |
| **Normalized key** | Dropdown | Lists your metric templates, with **+ Add new metric** at the bottom for creating one |
| **Unit** | Read-only | Taken from the selected template |
| **Type** | Read-only | Integer, Float, String or Boolean, taken from the template |
| **Data type** | Dropdown | **Telemetry** |
| (remove) | Icon | Removes the row |

**Add key** adds a new empty mapping row.

#### Why is the Device data key dropdown empty?

The **Device data key** column is a dropdown, not a text input. It lists the payload keys that have actually arrived from your device. Before the first publish, the dropdown shows nothing and the rows can't be filled.

The setup flow is two-pass:

1. Add a row per metric you want, pick the **Normalized key** from the templates dropdown (or use **+ Add new metric**), set the **Data type**, and leave the **Device data key** empty.
2. Tap **Save**. The device record is stored.
3. Make sure your hardware is publishing — for Zigbee2MQTT, the Z2M container is running and the device has reported at least once. (See [Discovering payload keys](mqtt/troubleshooting.md) if you're unsure how to force a publish.)
4. Reopen the device. The **Device data key** dropdown now lists the keys received from your device.
5. Match the right key to each row.
6. Tap **Save** again.

#### What the value column shows vs what the Logs tab shows

The Mapping tab's **Value** column updates from the most recent payload. It's a live snapshot — you'll see values as soon as the topic match works, even before you've finished filling in Device data keys.

The **Logs** tab is different: it's per-sensor history, and it only fills with publishes that arrive *after* you've saved Device data keys. If you fill in Device data keys, save, and then the lamp's wall switch is toggled but no MQTT publish is generated, the Logs tab will stay empty even though the Mapping tab shows the right value. To populate Logs, you need a fresh publish — drag a control in the Z2M web UI, send a `/get` poll, or wait for the device's next scheduled report. See [Troubleshooting](mqtt/troubleshooting.md) for the full list.

#### Mapping is iterative

MQTT mapping is rarely a one-shot operation. The first publish often reveals payload keys you didn't know to map during initial registration. After data starts arriving, return to the device's Mapping tab, look at the **Device data key** dropdown and **Value** column to see what the device is actually publishing, add rows for any useful fields you missed, set the right Data type for each, and save again. Generate another publish afterwards if you want the Logs tab to populate the new mappings.

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

1. **Z2M web UI** — open the Zigbee2MQTT frontend (default `http://localhost:8080`), click your device, look at the state panel. Every property name shown is a Device data key candidate.
2. **The device's Z2M page** — `https://www.zigbee2mqtt.io/devices/{modelId}.html` lists the device's Exposes. Note that actual payloads can include keys that aren't on the Z2M page (`color_mode` is one example) — trust the live payload over the device page.
3. **Z2M logs** — after the first publish, `docker compose logs zigbee2mqtt | grep "MQTT publish"` shows the full JSON. Every top-level key is valid.

4. Tap **Save** to finish registration.

---

## What should I see after setting up MQTT?
Once a sensor is registered and data is flowing:

- The connector's **Last data received** timestamp updates each time a message arrives.
- The sensor's detail page shows incoming readings — temperature, humidity, battery, or whatever your sensor reports.
- Readings appear on your dashboards and are available for automations and alerts.

For Zigbee2MQTT sensors, data typically appears within a few seconds of the sensor's next report.

---

## Where can I find more MQTT examples?
**ESP32 DIY temperature sensor:**
Publishes to `home/sensors/esp-kitchen/data` with a flat JSON payload. MQTT Topic for device ID: `home/sensors/{{deviceId}}/data`. Leave Topic Telemetry empty — the payload is parsed automatically. Mapping tab maps `temperature` and `humidity` keys to the corresponding normalized metrics.

**Tasmota smart plug:**
Tasmota publishes to `tele/plug-01/SENSOR`. MQTT Topic for device ID: `tele/{{deviceId}}/SENSOR`. The payload is flat JSON with energy readings (Power, Voltage, Current, Today). Leave Topic Telemetry empty; then add Mapping tab rows for the Tasmota keys you want to track.

**Garden soil sensor — single metric on a dedicated topic:**
A custom sensor publishes soil moisture to `garden/{{deviceId}}/moisture` with a plain number payload. Add a telemetry topic row: topic `garden/{{deviceId}}/moisture`, Device data key `soil_moisture`. Then in the Mapping tab, link `soil_moisture` to the normalized soil moisture metric.

---

## How do I troubleshoot the MQTT connector?
A short list — the [full troubleshooting page](mqtt/troubleshooting.md) covers Z2M startup logs, the empty-Logs-tab pattern, and how to force a publish for setup-time verification.

**No data appears after setup:**
- For Cloud MQTT: make sure you copied the password correctly at creation time. If unsure, rotate the credentials and update Zigbee2MQTT with the new password. Confirm the Topic prefix is being used correctly — all published topics must start with it.

**Sensor appears but readings are missing or wrong:**
- Open the sensor detail page and check the **Logs** tab for incoming message content.
- Verify the MQTT Topic for device ID matches the exact topic path the sensor is publishing to. Topics are case-sensitive.
- Verify the **Device ID** is byte-for-byte identical to the device-level segment (for Zigbee2MQTT, the friendly name) — no spaces, same case.
- If you added telemetry topic rows: check that the Device data key spellings match the payload keys exactly.
- In the Mapping tab: confirm that the Device data key column values match what the sensor is actually publishing.

**Mapping tab Value column populates but Logs tab is empty:**
This usually means Device data keys were saved after the most recent publish arrived. The Logs tab only fills with publishes that arrive *after* the keys are saved. Generate a fresh publish — drag a control in the Z2M web UI, or send a `/get` poll for setup-time verification — and the Logs tab will populate.

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

Each device is configured separately. [MQTT Devices](../devices/mqtt-devices.md) shows how: pick its identifier, complete the connection fields, map the incoming readings to measurements, and then verify the retained history.
