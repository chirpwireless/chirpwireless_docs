---
description: Follow your car's recorded locations on a Chirp dashboard and keep its history together when you replace the GPS tracker.
---

# Tracking What Matters

Chirp's **Map** widget lets you follow your car's reported positions on a dashboard. It shows the last known location and lets you choose a date range to see a route drawn from recorded coordinates. The same digital device can keep that location history when you replace the tracker installed in the car.

For example, name the digital device **Family Car**, connect its GPS tracker, and map the reported latitude and longitude. If the tracker later malfunctions, keep Family Car and those measurements when connecting the replacement. You can then review recorded locations from both trackers on the same map, within your retention period.

## Where to find tracking

1. Connect your car through the [Tracker Connector](../connectors/tracker-connector.md) and map its location readings. A LoRaWAN GPS device uses the [LNS Connector](../connectors/lns-connector/README.md) instead.
2. Add a [Map widget](adding-widgets/map-widget.md) to a dashboard and select the digital device, such as Family Car.
3. Use latitude and longitude measurements with recognizable names: `lat` or `latitude`, and `lon`, `longitude`, or `lng`. The widget uses these measurements to find the coordinates.
4. Save the dashboard and leave edit mode. The map displays the last known position as the tracker reports.

<figure><img src="../.gitbook/assets/map-widget.jpg" alt="Chirp Map widget settings with a device position shown in the map preview"><figcaption><p>Connect the Map widget to the car's digital device. Retain its coordinate measurements when replacing the tracker.</p></figcaption></figure>

You can also select one additional measurement, such as speed or battery level, for the current-position marker. Only readings the tracker actually supplies can be displayed.

## Picking a date range

Select **History** on the Map widget and choose the dates you want to review. The map draws a line connecting the recorded positions for that period. Once history is open, use the date range button to choose another period or **Clear data range** to return to the current-position view.

The **Snap to roads** switch adjusts the displayed route to roads where matching is available. Turn it off to view the line between reported coordinates. A drawn line between positions is not a recording of every point travelled between them.

Choose a shorter date range for a busy tracker if the route appears incomplete. The widget loads a limited batch of coordinate readings for each selected range. It needs both latitude and longitude at a matching timestamp to form a position.

## Replacing a tracker while keeping location history

Open the existing **Family Car** digital device and replace its physical connection. Keep its latitude and longitude measurement rows, then map the replacement tracker's fields onto those same rows. The Map widget continues using those measurements, so its history can include positions recorded before and after the change.

Follow [Replace your car's tracker](../devices/sensor-details.md#replace-your-cars-tracker) for the connection and mapping steps. Creating another digital device with the same name does not join the histories.

## Checking an unexpected route or missing position

- **The position is old:** open the device's **Mapping** tab and check the values and **Last update** for both coordinates. A last known position does not mean the tracker is reporting now.
- **New positions stopped after replacement:** reconnect `position.latitude` and `position.longitude` to the existing coordinate measurements and check [Connection Diagnostics](../devices/connection-diagnostics.md).
- **The history is empty:** choose a period with recorded data inside your [retention window](../account/subscription.md#keeping-your-data-history). Open **Logs** to inspect the stored coordinate values and timestamps.
- **There is a gap:** the tracker may have been disconnected, out of coverage, or not reporting during that period. Replacing it cannot recreate positions it never sent.

## What's next

- [Map Widget](adding-widgets/map-widget.md) — configure the map and its additional reading.
- [Sensor Details](../devices/sensor-details.md) — manage the digital device and replace its hardware.
- [Maps and Device Placement](maps-and-device-placement.md) — organize stationary devices by where they are installed.
