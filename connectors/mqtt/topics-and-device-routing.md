# Topics and device routing

This is the page to read once before you register your first MQTT device. It explains what the **Device ID Topic** field actually accepts, how Chirp matches incoming messages to the right device, why the **Connector key** dropdown is empty when you first open it, and the small handful of conventions that — once you know them — make every MQTT device registration feel routine.

## The shape of an incoming MQTT topic

When a device publishes through your MQTT connector, the topic Chirp sees has the device-level segment plus, for Cloud MQTT, your connector's prefix:

```
Cloud MQTT:    iot/{org}/{connection}/zigbee2mqtt/LivingRoomSensor
External MQTT: zigbee2mqtt/LivingRoomSensor
```

For Cloud MQTT, the `iot/{org}/{connection}/` part identifies which connector the message belongs to. Chirp strips it before matching, leaving the device-level topic — `zigbee2mqtt/LivingRoomSensor`. For External MQTT, the bridge adds and strips its own prefix internally, but the device-level topic ends up the same shape.

So when you fill in **Device ID Topic** in Chirp, you're describing the device-level shape only. Forget the prefix; Chirp handles it.

## The Device ID Topic field is a pattern, not a value

The label might suggest you should type a fixed identifier, but the field actually accepts a **topic pattern** with placeholders. The standard pattern for Zigbee2MQTT is:

```
zigbee2mqtt/{{deviceId}}
```

`{{deviceId}}` is a placeholder. When a topic arrives, Chirp matches it against the pattern and pulls the segment that aligns with `{{deviceId}}` out as the device's identifier. So an incoming topic of `zigbee2mqtt/LivingRoomSensor` resolves to `LivingRoomSensor` — and Chirp looks for a device record whose Device ID equals that string.

For non-Zigbee2MQTT setups, the pattern follows whatever shape your hardware publishes. A Tasmota smart plug publishing to `tele/PlugKitchen/SENSOR` would use:

```
tele/{{deviceId}}/SENSOR
```

A custom ESP32 publishing to `home/sensors/esp-kitchen/data` would use:

```
home/sensors/{{deviceId}}/data
```

The placeholder marks the segment where the device identifier lives. Everything else in the pattern is matched literally.

## Available placeholders

| Placeholder | What it does |
|-------------|-------------|
| `{{deviceId}}` | Marks the topic segment that contains the device identifier. Required in any Device ID Topic pattern. |
| `{{value}}` | Marks a topic segment whose content **is** the measurement reading itself — for example, `sensors/dev01/22.5` where `22.5` is the temperature. Useful for sensors that encode the reading in the topic. Do not use `{{value}}` for segments that name a metric (like `temperature`) — for that case, use the payload-side approach instead. |

## The Device ID field must match the device-level segment exactly

When you create the device record in Chirp, the **Device ID** field has to be byte-for-byte identical to whatever the publishing side puts in the `{{deviceId}}` segment. For Zigbee2MQTT, that means it has to equal the friendly name you chose in Z2M.

The biggest hidden trap here: **Chirp's Device ID input strips whitespace.** If your Z2M friendly name is `Living Room Sensor` (with spaces), and you paste that into Chirp's Device ID field, the platform stores it as `LivingRoomSensor` (or as `Living` — the exact normalization isn't guaranteed) — and the topic match fails. No error appears anywhere; you just see an empty Logs tab and wonder why.

The safe pattern: **pick a whitespace-free name on the Z2M side** and use it byte-for-byte in Chirp. Examples that work:

- `LivingRoomSensor` — CamelCase
- `living_room_sensor` — snake_case
- `lamp-01` — kebab-case

Capitalisation is preserved, so `LivingRoomSensor` and `livingroomsensor` are different devices. Pick one and be consistent on both ends.

## Telemetry topics: when to use them, when to skip them

The **Telemetry topics** section under the Topic sub-tab is for devices that publish **each metric to its own topic** — like a custom sensor that publishes soil moisture to `garden/{deviceId}/moisture` and temperature to `garden/{deviceId}/temperature`, each with just a number as the payload.

For Zigbee2MQTT and most other modern devices, you can leave Telemetry topics completely empty. Z2M publishes a flat JSON payload on a single topic with all the metrics inside:

```json
{"temperature": 21.4, "humidity": 58, "battery": 92, "linkquality": 115}
```

Chirp parses that JSON automatically — every top-level key becomes a candidate Connector Key in the Mapping tab. No per-topic configuration needed.

Add Telemetry topic rows only when you genuinely have one-metric-per-topic publishing. For everything else, the Mapping tab is enough.

## The Mapping tab has two sub-tabs (and they have the same name)

A small UI quirk worth flagging: the device's **Mapping** tab is itself divided into two sub-tabs, **Topic** and **Mapping**. When you tap the outer **Mapping** tab, you land on the **Topic** sub-tab — that's where the Device ID Topic field lives. To reach the connector-key rows, tap **Next** at the bottom or click the inner **Mapping** label directly.

Users who fill in the Topic sub-tab and then tap Save without visiting the inner Mapping sub-tab end up with a device that has no telemetry mappings. The outer "Mapping" name is the headline; the inner "Mapping" sub-tab is where the actual key matching happens.

## Connector Key dropdown is empty until your device publishes once

When you reach the inner Mapping sub-tab and start adding rows, the **Connector key** column is a dropdown — and the first time you open it on a brand-new device, it's empty.

That's intentional. The dropdown lists keys that have actually arrived from your device's payload. Before the first publish, Chirp doesn't know what keys your device sends, so the list is empty.

The setup flow is therefore two-pass:

**Pass 1 — set up the rows without Connector keys:**
1. Add a row for each metric you want to track.
2. Pick the **Normalized key** from the templates dropdown (this is the platform-side metric — Temperature, Humidity, Battery Level, etc.). If the metric you need doesn't exist yet, use **+ Add new metric** to create one. (One-time aside: the **+ Add new metric** modal handles two things behind the scenes — it ensures the normalized name exists *and* creates the sensor template that makes it appear in this dropdown. Pre-creating names elsewhere isn't necessary.)
3. Set the **Data type** (see below).
4. Leave **Connector key** empty.
5. Tap **Save**. The device record is now stored.

**Pass 2 — match keys to rows after data is flowing:**
6. Confirm your device is publishing — for Z2M, check that the container is running and the device has reported at least once. Easy way: drag the slider in the Z2M web UI for the device, or send a `/get` poll. Either generates a publish.
7. Reopen the device record. The **Connector key** dropdown now lists the actual keys received from your device.
8. Match a key to each mapping row.
9. Tap **Save** again.

After the second save, future incoming readings for those mapped keys will populate the Logs tab and be available for dashboards, alarms, and the AI assistant.

## Reported State vs Telemetry vs Device Metadata

The **Data type** column is where you tell Chirp what kind of value is coming in:

- **Reported State** — controllable device properties. Things the device can also be commanded to change: a bulb's `state` (ON/OFF), `brightness`, `color_temp`, a smart plug's `power_state`. These describe what the device *is* right now.
- **Telemetry** — read-only measurements. Things the device only reports, never commanded: `temperature`, `humidity`, `linkquality`, `battery`, `pressure`. These describe what the device *observes*.
- **Device Metadata** — values that describe the device itself rather than its readings. Firmware version, hardware model. Less commonly needed.

Pick the type by what the value *means* operationally — not by the metric template type (Integer/Float/String/Boolean), which is fixed by the template.

## A note on `state`: it's a string, not a boolean

For Zigbee2MQTT devices that have an on/off field, the payload sends `"ON"` or `"OFF"` as **strings**, not booleans. That means:

- The metric template Type for `state` must be **String**, not Boolean.
- If you use `+ Add new metric` to create a "State" metric, pick String as the type.
- If you accidentally pick Boolean, you'll see null values in the Mapping tab — Chirp can't parse `"ON"`/`"OFF"` strings into a boolean field.

The full Z2M-feature-type → Chirp-Type mapping:

| Z2M feature type | Chirp Type |
|------------------|-----------|
| `binary` | **String** (values are `"ON"`/`"OFF"` strings) |
| `numeric` | **Number** |
| `enum` | **String** |
| `text` | **String** |

## Why the Mapping tab Value column updates but the Logs tab is empty

Final concept worth understanding before you finish your first device. After Pass 2, you save, and:

- The **Value** column in the Mapping tab fills in immediately with whatever the device's most recent payload contained.
- The **Logs** tab is still empty.

This isn't a bug. The Value column is a live snapshot of the latest payload — it's there as soon as the topic match works, regardless of whether you've finished setting up Connector keys. The Logs tab is per-sensor history, and it's populated only by publishes that arrive *after* you save Connector keys.

So if your last publish was before Pass 2, that publish doesn't appear in Logs. The fix is to generate a fresh publish: drag a control in the Z2M web UI, send a `/get` poll, or wait for the device's next scheduled report. From that publish onwards, every reading flows into the Logs tab.

## Where to go next

- [Troubleshooting](troubleshooting.md) — When the topic match isn't working, when Logs stay empty after a fresh publish, and how to force a publish on a device that isn't reporting on its own.
- [Setting up Zigbee2MQTT](zigbee2mqtt.md) — If you haven't installed Z2M yet, this is the source of the topics you're matching here.
