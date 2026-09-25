---
description: Learn how Chirp digital twins keep your car or home device's readings together when you replace its tracker or sensor.
---

# Sensors

Every device you add to Chirp has a lasting digital record called a **digital twin**. It can stand for something you care about—your family car, the living room's temperature, or a garden watering valve. The physical tracker or sensor sends readings to that record. Its hardware can change while the digital device stays in place.

For example, you want to know where your car has been, not maintain a separate history for every tracker you have fitted to it. Name the digital device **Family Car** and connect your GPS tracker to it. If the tracker fails, you can attach its replacement to Family Car and keep the location readings already stored on that device.

<figure><img src="../.gitbook/assets/chirpdevicelist.jpg" alt="Chirp Devices list with named digital devices and their connection status"><figcaption><p>Name a device for what you want to follow, such as Family Car, so it remains recognizable when hardware changes.</p></figcaption></figure>

## Your car and its tracker have different roles

The **digital device** is Family Car. It holds the name, photo, measurement settings, and recorded readings. The **physical tracker** is the box installed in the car. The **Tracker connector** receives the messages it sends over the mobile network.

A tracker can report several readings, such as latitude, longitude, and speed. Each reading is mapped to a metric, which gives it a consistent meaning and unit in Chirp. What the tracker reports depends on its model and configuration.

One digital device has one connected source at a time, and that source can supply several measurements. Other sources include LoRaWAN sensors, equipment connected through MQTT, and the [Emulator](pretend-sensors.md), which generates readings for you.

## Keep the car's record when its tracker changes

Suppose your car's tracker stops working. Instead of adding a second device called Family Car, open the existing one and replace its physical connection. The car's digital twin and existing measurement channels remain in place.

After entering the replacement tracker's **Unique ID** and **Device model**, configure it to send to the displayed **Url for GPS tracker**. Map its location fields to the existing latitude and longitude measurements, then check that new readings arrive. The dashboard **Map** widget can show the car's retained location history from before and after the replacement. Select **History** and a date range spanning the change. The **Logs** tab lets you inspect the coordinate readings themselves.

This preserves the car's recorded location measurements without starting a separate device history. It cannot recover positions the failed tracker never sent. Keep the same measurement rows and change their source fields; removing a measurement and adding it again does not reconnect its old history.

The step-by-step guide is [Replace your car's tracker](sensor-details.md#replace-your-cars-tracker). For the first installation, start with the [Tracker Connector](../connectors/tracker-connector.md). [Tracking What Matters](../dashboards/tracking-what-matters.md) explains viewing the car's route on a dashboard.

## The same idea around your home

A living-room temperature sensor may need replacing, while the room and the comfort settings you use stay the same. Keep the room's digital device, attach the new sensor, and map its temperature reading to the existing measurement. Your dashboard and automations can keep referring to that measurement.

For a controllable device, such as a garden valve, the twin can also hold [commands](commands/README.md). Check command settings when fitting a different model: a saved action still needs a payload and connection that the new hardware understands.

You can create a digital device before the hardware arrives. [Pretend Sensors](pretend-sensors.md) explains how to generate readings to prepare your setup. Those generated readings also enter history, so keep them separate from real observations when reviewing what happened at home.

## History and your subscription

Keeping the same twin preserves the link to its stored readings; your subscription determines how far back you can access them. Hardware replacement does not restart the retention period. See [Keeping your data history](../account/subscription.md#keeping-your-data-history) for details and how to discuss a longer period.

## Choose the source for your digital twin

| Source | Start here |
| --- | --- |
| LoRaWAN sensor | [LoRaWAN Devices](lorawan-devices.md) — profiles, radio identity, decoding and first readings |
| MQTT publisher or bridged sensor | [MQTT Devices](mqtt-devices.md) — connect messages to a twin and its measurements |
| GPS tracker | [Tracker Connector](../connectors/tracker-connector.md) — tracker identity, model and reporting endpoint |
| Generated readings | [Pretend Sensors](pretend-sensors.md) — prepare dashboards before the sensor arrives |

## What's in this section

* [Adding Sensors](adding-sensors.md) — register a sensor and map what it measures
* [Pretend Sensors](pretend-sensors.md) — get set up before your hardware arrives
* [Data Templates](data-templates.md) — what your readings mean, with the right units
* [What Your Device Is Sending](what-your-device-is-sending.md) — see the fields your sensor reports, and what they say
* [Sensor Details](sensor-details.md) — replace hardware, reconnect readings, and review retained history
* [Connection Diagnostics](connection-diagnostics.md) — added a sensor but nothing's showing up?
* [Rooms](rooms.md) — make devices easy to recognize by room
* [Favorite Devices](favorite-devices.md) — star the ones you check most
* [Controlling Your Devices](commands/README.md) — turn things on and off, not just watch them
* [Tested Device Guides](tested-device-guides/README.md) — sensors we've paired end-to-end ourselves
