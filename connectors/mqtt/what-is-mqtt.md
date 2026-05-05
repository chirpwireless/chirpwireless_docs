# What MQTT is

MQTT is the messaging protocol that ties most of the modern smart home together. If you've ever watched a Zigbee sensor's reading appear on a dashboard, or asked your home automation to turn off the kitchen lights, MQTT was almost certainly carrying the message under the hood. It was designed in the late 1990s for satellite oil pipeline monitoring — devices with tiny radios, intermittent connectivity, and no patience for protocol overhead — and that pedigree is exactly why it works so well for battery-powered home sensors today.

If you already understand publish/subscribe messaging and just want to see how Chirp's MQTT connector fits in, skip ahead to [Cloud MQTT](cloud-mqtt.md) or [External MQTT](external-mqtt.md). If MQTT is new to you, the rest of this page is the orientation that will make those next pages click.

## The mental model

Three things are involved in any MQTT setup:

- A **broker** — the central post office that everything connects to. Devices don't talk to each other directly; they all talk to the broker, and the broker forwards messages to whoever asked for them.
- **Publishers** — anything that sends messages. A Zigbee2MQTT bridge publishing temperature readings, an ESP32 publishing soil moisture, a smart plug publishing its on/off state.
- **Subscribers** — anything that listens for messages. Chirp's MQTT connector is a subscriber; so is your home automation hub if you have one.

The same device can be both a publisher (it tells the broker about its temperature) and a subscriber (it listens for commands telling it to change a setpoint). The broker is the one constant — every message goes through it.

```
Living room sensor  →  publish  →
                                   Broker  →  forward  →  Chirp
Kitchen sensor      →  publish  →
```

Chirp's MQTT connector subscribes to messages the broker is forwarding. When you register a device, you're telling Chirp which messages from the broker belong to which device record.

## Topics: the address of every message

Every MQTT message has a **topic** — a slash-separated path that identifies what the message is about. The broker uses topics to route messages: subscribers say "I'm interested in topics that look like `home/+/temperature`," and the broker delivers anything matching that pattern.

Topics are not predefined. Whoever publishes a message decides the topic — there's no central registry. Conventions vary by software:

- **Zigbee2MQTT** publishes each device's data to `zigbee2mqtt/{friendlyName}` — for example, `zigbee2mqtt/LivingRoomSensor`. Below this device-level topic, the bridge also publishes status, command-acknowledgements, and per-device subtopics for actions like `/set` and `/get`.
- **Tasmota** smart plugs publish to `tele/{deviceName}/SENSOR` for periodic telemetry, `stat/{deviceName}/RESULT` for state changes, and several other topics.
- **Custom firmware** can use whatever topic scheme you write into it. A common pattern is `home/{location}/{deviceName}/{metric}`.

When you register a device in Chirp, the **Device ID Topic** field is where you tell the connector what the topic *shape* looks like. You write the pattern with `{{deviceId}}` standing in for the part of the topic that names the device — for Zigbee2MQTT, that's `zigbee2mqtt/{{deviceId}}`. Chirp matches incoming topics against the pattern and pulls the device identifier out of the placeholder position.

## Payloads: usually JSON, sometimes not

The body of an MQTT message is the **payload**. MQTT itself doesn't care what's in there — bytes are bytes — but in practice almost every modern device publishes JSON.

A typical Zigbee temperature/humidity sensor publishes something like:

```json
{
  "temperature": 21.4,
  "humidity": 58,
  "battery": 92,
  "linkquality": 115
}
```

That single message contains four sensor metrics, all delivered together as a flat object. Chirp's Mapping tab reads the keys from this JSON and maps them to your sensor's metric templates — `temperature` becomes the temperature reading, `humidity` becomes humidity, and so on.

Some devices publish each measurement to its own topic with just a number as the payload:

```
home/garden/soil-01/moisture     →  payload: 42
home/garden/soil-01/temperature  →  payload: 18.2
```

For that style, you add per-topic rows on the **Telemetry topics** section so Chirp knows which topic carries which metric. The flat-JSON case (one topic, all metrics in the payload) is more common and is the default path.

## QoS, retained messages, and other details that usually don't matter for setup

MQTT has features beyond the basics: three quality-of-service levels (QoS 0/1/2), retained messages that the broker keeps and replays to new subscribers, last-will messages that the broker publishes when a device disconnects unexpectedly. For a home setup with Chirp, you almost never need to think about these. Zigbee2MQTT picks reasonable defaults; Tasmota does too; Chirp's broker accepts what it's given.

The one detail that comes up: when Zigbee2MQTT first connects, it publishes a "bridge online" retained message. Chirp's connector will see that as the first incoming traffic — that's a signal the connection is healthy, even before any device has reported.

## Why MQTT and not something else

MQTT is the lingua franca of the smart home for three reasons:

- **Tiny overhead.** A temperature reading is a few bytes of header plus the JSON. This matters on battery-powered sensors that wake up every few minutes.
- **Loose coupling.** Devices don't need to know about each other. Add a new sensor and the broker just routes its messages — no other device has to be reconfigured.
- **It already works.** Zigbee2MQTT, Tasmota, ESPHome, Theengs, OpenMQTTGateway, and dozens of other projects all speak MQTT. Most off-the-shelf "smart home compatible" hardware can be made to publish MQTT with a small bridge.

When you're ready, continue to [Cloud MQTT](cloud-mqtt.md) for the simpler setup, or [External MQTT](external-mqtt.md) if you already run your own broker.
