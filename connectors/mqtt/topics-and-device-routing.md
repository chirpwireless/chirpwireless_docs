---
description: Configure Chirp MQTT topic segments, payload identifiers, topic-value extraction and measurement mapping, with examples and validation.
---

# Topics and device routing

When an MQTT message arrives, Chirp has to answer two questions: which digital device sent it, and which readings are inside it. A **topic** is the named channel the message travels on, and the **payload** is the content it carries. You answer both questions on the device's **Connection** tab, and then you link the fields you receive to measurement templates on **Mapping**.

If this is your first MQTT device, begin with [MQTT Devices](../../devices/mqtt-devices.md). Come back here for the routing controls in detail, including identifiers that travel in the payload and readings that sit inside the topic name itself. Setting up the broker is covered in [Cloud MQTT](cloud-mqtt.md) and [External MQTT](external-mqtt.md).

## Topic shape after broker-side processing {#the-shape-of-an-incoming-mqtt-topic}

With Cloud MQTT, every topic a publisher uses starts with the connection's **Topic prefix**, for example `iot/{org}/{connection}`. The editor shows that prefix as a locked first segment, so your device-level pattern starts right after it. Typing the prefix a second time would break the match.

With External MQTT there is no Cloud prefix to account for. Instead, write a pattern that mirrors the topic your equipment publishes to your own broker. A message on `meters/EM-4492/data` matches the pattern `meters/{{deviceId}}/data` when the Device ID is `EM-4492`.

Under the pattern, a read-only **Resolved preview** shows the finished topic: the Cloud prefix (when there is one) followed by your pattern with the Device ID filled in. Treat it as a spelling check for the pattern; it does not tell you that a message has actually been received.

## Building the Device ID Topic {#the-device-id-topic-field-is-a-pattern-not-a-value}

On **Connection**, the **MQTT Topic for device ID** field is a builder made of segments, and a slash separates one segment from the next.

| Control | Behavior |
| --- | --- |
| **+ → Text segment** | Adds a fixed piece of the topic, such as `meters`, `zigbee2mqtt`, or `data`. Spell it exactly as the publisher does. |
| **+ → Device ID** | Marks where the identifier sits in the topic. Only one Device ID segment is allowed, so this choice is greyed out once it exists. |
| Drag handle | Moves a segment so the order matches your topic, for instance placing Device ID between `meters` and `data`. |
| Segment remove control | Deletes a text segment you added. In Topic mode the Device ID segment cannot be removed; change to Payload mode first if the identifier will come from somewhere else. |
| Locked prefix | The connection prefix of Cloud MQTT. It is fixed and cannot be edited or deleted from this field. |
| **Resolved preview** | Displays the topic that results from the Device ID you entered. In telemetry patterns, a value placeholder shows as `value` rather than as a real number. |

### Available placeholders

Two placeholders exist: `{{deviceId}}` and `{{value}}`. In the examples on this page, `{{deviceId}}` stands for the identifier position and is never a literal device name. Topic templates are case-sensitive, so the segments and their positions have to match what the publisher sends. Telemetry templates are refused if they contain `#`, a placeholder Chirp does not know, or a placeholder that is missing its closing braces.

## Read the identifier from a payload

The **Where to get the device ID** setting has two options, **Topic** and **Payload**. New devices start on Topic, which pulls the identifier out of the Device ID segment. To take it from the JSON body instead:

1. Choose **Payload**.
2. Build the message topic with no Device ID segment in it, such as `building/readings`.
3. In **Payload template**, type a dot-separated path to the identifier, for example `deviceInfo.deviceId`.
4. Look at **Payload preview**, which draws the JSON object around that path so you can confirm it.
5. Enter the value found at that path as the device's **Device ID**, then save.

A message on `building/readings` like the one below identifies the device `room-1`:

```json
{"deviceInfo": {"deviceId": "room-1"}, "temperature": 21.4}
```

Whichever mode you pick, the topic cannot be empty. The two modes ask for different things: Payload mode requires the JSON path and keeps the Device ID placeholder out of every topic pattern, while Topic mode requires that placeholder in the device pattern and in every telemetry row you configure. After switching, check that the selector and the segments tell the same story.

## Device ID input must match the extracted segment byte-for-byte {#the-device-id-field-must-match-the-device-level-segment-exactly}

A **Device ID** can be 1–64 characters long and may use ASCII letters, digits, spaces, periods, underscores and hyphens. For MQTT devices, capitals and spaces are kept as typed. The publisher and Chirp must therefore spell the identifier identically: `room-1` and `Room-1` are two different devices.

With Zigbee2MQTT, the identifier is the device's friendly name, and a short one such as `LivingRoomSensor` keeps things easy. Should the physical hardware change after binding, follow [device replacement](../../devices/sensor-details.md) on the existing twin. That keeps the twin and its measurement associations intact, which deleting it would not.

## Topic Telemetry {#topic-telemetry}

### When to use telemetry topics {#telemetry-topics-when-to-use-them-when-to-skip-them}

If the message body already holds your measurements as JSON, leave **Topic Telemetry** empty. The body `{"temperature":21.4,"battery":92}` supplies two data keys, `temperature` and `battery`, and nested objects turn into dot-separated paths, so `{"vibration":{"rms":0.42}}` supplies `vibration.rms`.

Reach for the topic telemetry editor when the **number itself is written inside the topic**. Take a publisher that sends on `meters/EM-4492/voltage/230.5`:

| Row field or action | How it works |
| --- | --- |
| **Add new topic** | Creates a row with a pinned **value** segment. Add text and Device ID segments until the row mirrors the publisher's topic. |
| **MQTT Topic for telemetry** | For this example, build `meters/{{deviceId}}/voltage/{{value}}`. The last segment stands for the reading `230.5`, not for the word `voltage`. |
| **value** segment | Optional. A caption beneath the row states which mode is active: **The value is read from the value segment of the topic** or **No value segment: the value is read from the message payload**. Drag the segment into place, delete it when the number travels in the message body, or put it back later. |
| **Device data key** | Required on every row, with or without a value segment; without one the row says **Device data key is required** and cannot be saved. Type the name the reading should carry from now on, such as `voltage`, and then connect that name to a measurement on **Mapping**. |
| Row remove control | Takes the telemetry rule out of the configuration you are editing. Save to make the removal final. |
| **Apply all** | Rewrites every row's topic pattern to the device-ID topic followed by a value segment, skipping any pattern that already has one, and keeps each row's data key. Afterwards, go through the rows and put back literal segments such as `voltage` or `current` where they belong. It adds no rows and does not save the device. |

Many gadgets publish a single reading per topic and put the number in the body. A smart plug that sends `0` or `1` to `device/260/ap/5/upload` is typical. For that case, build the topic without a value segment and give the row a data key like `outlet_state`; Chirp stores the body under that name. The web page used to make this impossible, and re-saving a device configured another way could quietly break it. Patterns now display exactly as they are stored.

With Payload as the identifier source, telemetry rows leave out the Device ID, yet each message must still carry the identifier at the JSON path you set. If a value from the topic and a payload field share a key, the topic's value wins.

The parser behind the scenes can also take JSON fields or raw payload data, but the topic editor does not expose every protocol format that implies. When a plain, non-JSON message has no telemetry extraction row, look at the incoming `raw` key and map it only if it really holds the value you want. Binary vendor formats must be converted before they reach Chirp, because recognizing a topic hierarchy does not decode Sparkplug or any other binary payload.

## Connection and Mapping have different jobs {#the-mapping-tab-has-two-sub-tabs-and-they-have-the-same-name}

**Connection** holds routing and identity. **Mapping** holds the measurement rows. They are separate tabs, and a saved topic pattern does not by itself create a measurement for every field in the message.

Press the device's **Save** button once the routing is right: segment previews and **Apply all** only change the form on screen. A telemetry row that is left blank is not a finished extraction rule, so either complete its pattern and data key or remove it. Members with read-only access cannot change routing.

## Connector key dropdown: the two-pass save flow {#connector-key-dropdown-is-empty-until-your-device-publishes-once}

The **Device data key** dropdown fills with the fields Chirp has actually received from the bound source, so it starts empty. Save the connection, wait for one message, then finish the mappings and save a second time. Template rows you created before that first message can stay; just fill in their data keys when the options appear.

The [MQTT Devices](../../devices/mqtt-devices.md#map-messages-to-retained-measurements) page walks through this, and [mapping controls](../../devices/sensor-details.md#metrics) explains every column and action.

## Mapping data type {#reported-state-vs-telemetry-vs-device-metadata}

The device-mapping form offers one data type, **Telemetry**, for measurements and reported states you want to keep. The metadata and attribute categories of the wider metric catalog are not selectable here, and the **Data type** setting is separate from the template's value **Type**.

## Match the metric type to the actual value {#a-note-on-state-its-a-string-not-a-boolean}

| Incoming value | Appropriate template Type |
| --- | --- |
| Decimal reading such as `21.4` | Float |
| Whole-number count such as `12` | Integer |
| `"ON"`, `"OFF"`, an enum or free text | String |
| JSON `true` or `false` | Boolean |

Zigbee2MQTT may describe a feature as binary and still publish true/false or configured text values, so read the real payload before picking a type. Strings that hold numbers convert to numeric templates; for integers, any decimals are cut off toward zero. Booleans accept true/false and 0/1, but `"ON"` and `"OFF"` are not accepted. A reading that cannot be converted is rejected on its own rather than saved as an empty value. The [metric conversion rules](../../devices/data-templates.md) have the details.

## Mapping tab Value column vs Logs tab history {#why-the-mapping-tab-value-column-updates-but-the-logs-tab-is-empty}

On **Mapping**, **Value** and **Last update** reflect the newest snapshot of each received field. **Logs** only lists measurements recorded after valid mappings were saved, so wait for a new message once the mapping is in place; older messages are not re-processed.

MQTT history is stamped with the moment Chirp receives the message. Fields called `timestamp`, `ts`, or `time` stay ordinary payload fields and do not move the stored measurement back in time, which also means messages a device buffered during an outage are not placed at their original device time.

### Iterative mapping refinement {#mapping-is-iterative-return-after-data-arrives}

Mapping is not a one-off job. When firmware changes or you need new readings, open **Mapping** again, look at the new keys, add templates for them with compatible types, save, and let a fresh message arrive. If you swap out the hardware, leave the existing measurement rows alone so the twin keeps its history.

## Where to go next

- [MQTT Devices](../../devices/mqtt-devices.md) — first-device walkthrough and configuration checklist.
- [MQTT Troubleshooting](troubleshooting.md) — broker, routing and missing-history problems.
- [Creating Commands](../../devices/commands/creating-commands.md) — outbound MQTT topics and command payloads.
