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

1. A **Zigbee coordinator adapter** — the hardware bridge between Zigbee radio and your home network or computer.
2. **Zigbee2MQTT software** — runs on a Raspberry Pi, home server, or any always-on machine.
3. A **Chirp MQTT connector** — tells Chirp where to listen and how to read the messages.

### Recommended Zigbee coordinator adapters

Any adapter supported by Zigbee2MQTT will work. The most commonly used:

- **SONOFF Zigbee 3.0 USB Dongle Plus** — ZBDongle-P (CC2652P chip) or ZBDongle-E (EFR32MG21 chip). Plug directly into a USB port.
- **SMLIGHT SLZB-06 / SLZB-06M** — Network-attached. Connects over Ethernet or Wi-Fi. No need to run USB cables.
- **Home Assistant Connect ZBT-1 / SkyConnect** — Works when configured to use Zigbee2MQTT (instead of ZHA).
- **ConBee II / Phoscon** — USB adapter from Dresden Elektronik, used with deCONZ or Zigbee2MQTT.

For the current recommended options, see the [Zigbee2MQTT adapter guide](https://www.zigbee2mqtt.io/guide/adapters/).

---

## Two ways to connect: Chirp Cloud MQTT vs External MQTT

When you add the MQTT connector, you choose one of two broker options:

**Chirp Cloud MQTT** — Chirp provides the MQTT broker. You get connection credentials (endpoint, username, password) that you paste into Zigbee2MQTT or your device's settings. Nothing to host or maintain.

**External MQTT** — You use an existing MQTT broker you already run — on a Raspberry Pi, home server, or a cloud account. Chirp connects to it using the broker URL and credentials you supply.

For most home setups, **Chirp Cloud MQTT** is the simpler choice.

---

## Step 1: Add the MQTT connector

1. Tap **Connectors** in the sidebar.
2. Tap **Add connector**.
3. Select **MQTT** from the connector type list.
4. Tap **Add**.

The connector appears in your connections list. Tap its row to open the connector detail page.

---

## Step 2: Set up the broker connection

### Chirp Cloud MQTT

After the connector is created, Chirp generates connection details for you:

- **Broker endpoint** — the address your device or Zigbee2MQTT connects to.
- **Username** — assigned automatically.
- **Password** — shown once. **Copy it immediately** and keep it somewhere safe. If you lose it, you'll need to rotate the credentials.

Paste these into your Zigbee2MQTT configuration or device settings.

### External MQTT

Fill in these fields:

| Field | What to enter |
|-------|--------------|
| **Broker URL** | The full address including scheme and port. Examples: `mqtt://192.168.1.100:1883` (local), `mqtts://mqtt.yourdomain.com:8883` (remote with TLS). Accepted schemes: `mqtt://`, `mqtts://`, `tcp://`, `ssl://`. |
| **Authentication** | Choose from: **Anonymous** (no credentials), **Username / Password**, **TLS / Certificate** (paste PEM files), or **Token / JWT**. |
| **QoS** | Quality of Service level. Leave at the default for most home setups. |

Tap **Save** when done.

---

## Step 3: Register a device

Each sensor that sends data through this connector needs to be registered in Chirp. Registration maps MQTT topics to a sensor profile.

1. On the connector detail page, tap **Add device** — or go to **Devices** and start the registration flow there, selecting this connector.
2. Fill in the sensor name and pick a template if one fits.
3. In the **Connection** tab, set up topic routing:

### Zigbee2MQTT topic setup (the common case)

Zigbee2MQTT publishes each device's data to a topic named after the device:
```
zigbee2mqtt/0x00158d0001234567
```
or with a friendly name you've set in Zigbee2MQTT:
```
zigbee2mqtt/Living Room Sensor
```

For the **Device ID Topic**, enter:
```
zigbee2mqtt/{{deviceId}}
```

Leave **Telemetry topics** empty. Zigbee2MQTT publishes a flat JSON payload like:
```json
{"temperature": 21.4, "humidity": 58, "battery": 92, "linkquality": 115}
```

Chirp automatically reads all keys from this payload and maps them as separate metrics. You don't need to configure anything else — the sensor starts showing temperature, humidity, battery level, and link quality once data arrives.

### Topic routing fields explained

**Device ID Topic** — The MQTT topic pattern for this device. Use `{{deviceId}}` to mark the part of the topic that contains the device's identifier.

**Device ID Source** — Where Chirp finds the device ID:
- **Topic** (default) — extracted from the `{{deviceId}}` segment of the topic.
- **Payload** — taken from a field inside the JSON message body.

**Device ID Payload Path** — Required when source is set to **Payload**. A dot-notation path to the ID field. For example, `device.id` for a payload like `{"device": {"id": "sensor-01"}, "temp": 22.1}`.

**Telemetry topics** — Optional. Use these when you need to map specific metrics individually, or when values arrive on separate topics rather than a single JSON payload. If left empty, Chirp automatically parses the full payload as flat JSON.

### Placeholder reference

| Placeholder | What it does |
|-------------|-------------|
| `{{deviceId}}` | Marks the topic segment that contains the device's identifier. Chirp extracts this value to route the message to the right sensor. |
| `{{value}}` | Marks a topic segment that contains a measurement value directly (when the value is in the topic path rather than the payload). Requires a **Connector key** to name the metric. |

4. Tap **Save** to finish registration.

---

## What to expect after setup

Once a device is registered and data is flowing:

- The connector's **Last data received** timestamp updates each time a message arrives.
- The sensor's detail page shows incoming readings — temperature, humidity, battery level, or whatever your device reports.
- Readings appear on your dashboards and are available for automations and alerts.

For Zigbee2MQTT devices, data typically appears within a few seconds of the device sending its next report.

---

## More MQTT examples

**ESP32 DIY temperature sensor:**
You built a sensor that publishes to `home/sensors/esp-kitchen/data` with a JSON payload. Device ID Topic: `home/sensors/{{deviceId}}/data`. Leave telemetry topics empty — the payload is parsed automatically.

**Tasmota smart plug:**
Tasmota publishes to topics like `tele/plug-01/SENSOR`. Device ID Topic: `tele/{{deviceId}}/SENSOR`. The payload is flat JSON with energy readings (Power, Voltage, Current, Today). Chirp maps all of them automatically.

**Garden soil sensor:**
A custom sensor publishes soil moisture to `garden/{{deviceId}}/moisture` where the payload is a plain number. Add a telemetry topic row: topic `garden/{{deviceId}}/moisture`, connector key `soil_moisture`.

---

## Troubleshooting

**No data appears after setup:**
- For Zigbee2MQTT: confirm that Zigbee2MQTT is running and connected to the broker. Check the Zigbee2MQTT web interface to see whether devices are pairing and sending messages.
- Double-check the broker address and credentials. A small typo in the broker URL is the most common cause of connection failures.
- For Chirp Cloud MQTT: make sure you copied the password correctly at creation time. If unsure, rotate the credentials and reconfigure Zigbee2MQTT with the new password.

**Device appears but readings are wrong or missing:**
- Open the device detail page and check the **Logs** tab for incoming message content.
- Verify the Device ID Topic matches the exact topic path Zigbee2MQTT is publishing to. Topics are case-sensitive.
- If you added telemetry topic rows: check that the connector key spellings match the payload keys exactly.

**Zigbee device doesn't join:**
- This is a Zigbee2MQTT or coordinator issue, not a Chirp issue. Check the [Zigbee2MQTT documentation](https://www.zigbee2mqtt.io/guide/usage/pairing_devices.html) for device pairing steps.
- Make sure permit join is enabled in Zigbee2MQTT when pairing new devices.

**Password lost for Chirp Cloud MQTT:**
- Go to the MQTT connector settings and rotate the credentials. Update Zigbee2MQTT or your device with the new password.

---

## What's next

- [Adding Sensors](../devices/adding-sensors.md) — Complete your sensor setup and assign it to a room.
- [Choosing Widgets](../dashboards/choosing-widgets.md) — Display your new sensor readings on a dashboard.
- [Set Up a Home Alert](../alarm/set-up-a-home-alert.md) — Get notified when readings go outside normal ranges.
